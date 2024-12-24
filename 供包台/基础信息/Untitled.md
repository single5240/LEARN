```
void Stepper::isr() {

  

  static hal_timer_t nextMainISR = 0;  // Interval until the next main Stepper Pulse phase (0 = Now)

  

  #ifndef __AVR__

    // Disable interrupts, to avoid ISR preemption while we reprogram the period

    // (AVR enters the ISR with global interrupts disabled, so no need to do it here)

    hal.isr_off();

  #endif

  

  // Program timer compare for the maximum period, so it does NOT

  // flag an interrupt while this ISR is running - So changes from small

  // periods to big periods are respected and the timer does not reset to 0

  HAL_timer_set_compare(MF_TIMER_STEP, hal_timer_t(HAL_TIMER_TYPE_MAX));

  

  // Count of ticks for the next ISR

  hal_timer_t next_isr_ticks = 0;

  

  // Limit the amount of iterations

  uint8_t max_loops = 10;

  

  #if ENABLED(FT_MOTION)

    static uint32_t ftMotion_nextAuxISR = 0U;  // Storage for the next ISR of the auxilliary tasks.

    const bool using_ftMotion = ftMotion.cfg.active;

  #else

    constexpr bool using_ftMotion = false;

  #endif

  

  // We need this variable here to be able to use it in the following loop

  hal_timer_t min_ticks;

  do {

    // Enable ISRs to reduce USART processing latency

    hal.isr_on();

  

    hal_timer_t interval = 0;

  

    #if ENABLED(FT_MOTION)

  

      if (using_ftMotion) {

        if (!nextMainISR) {               // Main ISR is ready to fire during this iteration?

          nextMainISR = FTM_MIN_TICKS;    // Set to minimum interval (a limit on the top speed)

          ftMotion_stepper();             // Run FTM Stepping

          // Define 2.5 msec task for auxilliary functions.

          if (!ftMotion_nextAuxISR) {

            TERN_(BABYSTEPPING, if (babystep.has_steps()) babystepping_isr());

            ftMotion_nextAuxISR = (STEPPER_TIMER_RATE) / 400;

          }

        }

        interval = _MIN(nextMainISR, ftMotion_nextAuxISR);

        nextMainISR -= interval;

        ftMotion_nextAuxISR -= interval;

      }

  

    #endif

  

    if (!using_ftMotion) {

  

      TERN_(HAS_ZV_SHAPING, shaping_isr());               // Do Shaper stepping, if needed

  

      if (!nextMainISR) pulse_phase_isr();                // 0 = Do coordinated axes Stepper pulses

  

      #if ENABLED(LIN_ADVANCE)

        if (!nextAdvanceISR) {                            // 0 = Do Linear Advance E Stepper pulses

          advance_isr();

          nextAdvanceISR = la_interval;

        }

        else if (nextAdvanceISR > la_interval)            // Start/accelerate LA steps if necessary

          nextAdvanceISR = la_interval;

      #endif

  

      #if ENABLED(BABYSTEPPING)

        const bool is_babystep = (nextBabystepISR == 0);  // 0 = Do Babystepping (XY)Z pulses

        if (is_babystep) nextBabystepISR = babystepping_isr();

      #endif

  

      // ^== Time critical. NOTHING besides pulse generation should be above here!!!

  

      if (!nextMainISR) nextMainISR = block_phase_isr();  // Manage acc/deceleration, get next block

  

      #if ENABLED(BABYSTEPPING)

        if (is_babystep)                                  // Avoid ANY stepping too soon after baby-stepping

          NOLESS(nextMainISR, (BABYSTEP_TICKS) / 8);      // FULL STOP for 125µs after a baby-step

  

        if (nextBabystepISR != BABYSTEP_NEVER)            // Avoid baby-stepping too close to axis Stepping

          NOLESS(nextBabystepISR, nextMainISR / 2);       // TODO: Only look at axes enabled for baby-stepping

      #endif

  

      // Get the interval to the next ISR call

      interval = _MIN(nextMainISR, uint32_t(HAL_TIMER_TYPE_MAX));         // Time until the next Pulse / Block phase

      TERN_(INPUT_SHAPING_X, NOMORE(interval, ShapingQueue::peek_x()));   // Time until next input shaping echo for X

      TERN_(INPUT_SHAPING_Y, NOMORE(interval, ShapingQueue::peek_y()));   // Time until next input shaping echo for Y

      TERN_(INPUT_SHAPING_Z, NOMORE(interval, ShapingQueue::peek_z()));   // Time until next input shaping echo for Z

      TERN_(LIN_ADVANCE, NOMORE(interval, nextAdvanceISR));               // Come back early for Linear Advance?

      TERN_(BABYSTEPPING, NOMORE(interval, nextBabystepISR));             // Come back early for Babystepping?

  

      //

      // Compute remaining time for each ISR phase

      //     NEVER : The phase is idle

      //      Zero : The phase will occur on the next ISR call

      //  Non-zero : The phase will occur on a future ISR call

      //

  

      nextMainISR -= interval;

      TERN_(HAS_ZV_SHAPING, ShapingQueue::decrement_delays(interval));

      TERN_(LIN_ADVANCE, if (nextAdvanceISR != LA_ADV_NEVER) nextAdvanceISR -= interval);

      TERN_(BABYSTEPPING, if (nextBabystepISR != BABYSTEP_NEVER) nextBabystepISR -= interval);

  

    } // standard motion control

  

    /**

     * This needs to avoid a race-condition caused by interleaving

     * of interrupts required by both the LA and Stepper algorithms.

     *

     * Assume the following tick times for stepper pulses:

     *   Stepper ISR (S):  1 1000 2000 3000 4000

     *   Linear Adv. (E): 10 1010 2010 3010 4010

     *

     * The current algorithm tries to interleave them, giving:

     *  1:S 10:E 1000:S 1010:E 2000:S 2010:E 3000:S 3010:E 4000:S 4010:E

     *

     * Ideal timing would yield these delta periods:

     *  1:S  9:E  990:S   10:E  990:S   10:E  990:S   10:E  990:S   10:E

     *

     * But, since each event must fire an ISR with a minimum duration, the

     * minimum delta might be 900, so deltas under 900 get rounded up:

     *  900:S d900:E d990:S d900:E d990:S d900:E d990:S d900:E d990:S d900:E

     *

     * It works, but divides the speed of all motors by half, leading to a sudden

     * reduction to 1/2 speed! Such jumps in speed lead to lost steps (not even

     * accounting for double/quad stepping, which makes it even worse).

     */

  

    // Compute the tick count for the next ISR

    next_isr_ticks += interval;

  

    /**

     * The following section must be done with global interrupts disabled.

     * We want nothing to interrupt it, as that could mess the calculations

     * we do for the next value to program in the period register of the

     * stepper timer and lead to skipped ISRs (if the value we happen to program

     * is less than the current count due to something preempting between the

     * read and the write of the new period value).

     */

    hal.isr_off();

  

    /**

     * Get the current tick value + margin

     * Assuming at least 6µs between calls to this ISR...

     * On AVR the ISR epilogue+prologue is estimated at 100 instructions - Give 8µs as margin

     * On ARM the ISR epilogue+prologue is estimated at 20 instructions - Give 1µs as margin

     */

    min_ticks = HAL_timer_get_count(MF_TIMER_STEP) + hal_timer_t(TERN(__AVR__, 8, 1) * (STEPPER_TIMER_TICKS_PER_US));

  

    #if ENABLED(OLD_ADAPTIVE_MULTISTEPPING)

      /**

       * NB: If for some reason the stepper monopolizes the MPU, eventually the

       * timer will wrap around (and so will 'next_isr_ticks'). So, limit the

       * loop to 10 iterations. Beyond that, there's no way to ensure correct pulse

       * timing, since the MCU isn't fast enough.

       */

      if (!--max_loops) next_isr_ticks = min_ticks;

    #endif

  

    // Advance pulses if not enough time to wait for the next ISR

  } while (TERN(OLD_ADAPTIVE_MULTISTEPPING, true, --max_loops) && next_isr_ticks < min_ticks);

  

  #if DISABLED(OLD_ADAPTIVE_MULTISTEPPING)

  

    // Track the time spent in the ISR

    const hal_timer_t time_spent = HAL_timer_get_count(MF_TIMER_STEP);

    time_spent_in_isr += time_spent;

  

    if (next_isr_ticks < min_ticks) {

      next_isr_ticks = min_ticks;

  

      // When forced out of the ISR, increase multi-stepping

      #if MULTISTEPPING_LIMIT > 1

        if (steps_per_isr < MULTISTEPPING_LIMIT) {

          steps_per_isr <<= 1;

          // ticks_nominal will need to be recalculated if we are in cruise phase

          ticks_nominal = 0;

        }

      #endif

    }

    else {

      // Track the time spent voluntarily outside the ISR

      time_spent_out_isr += next_isr_ticks;

      time_spent_out_isr -= time_spent;

    }

  

  #endif // !OLD_ADAPTIVE_MULTISTEPPING

  

  // Now 'next_isr_ticks' contains the period to the next Stepper ISR - And we are

  // sure that the time has not arrived yet - Warrantied by the scheduler

  

  // Set the next ISR to fire at the proper time

  HAL_timer_set_compare(MF_TIMER_STEP, next_isr_ticks);

  

  // Don't forget to finally reenable interrupts on non-AVR.

  // AVR automatically calls sei() for us on Return-from-Interrupt.

  #ifndef __AVR__

    hal.isr_on();

  #endif

}
```