1. 并联 - 串口1
2. 串联 - 串口3

#### 功能
##### 并联
###### 1.向从机发送plc心跳
```c
if ((Get_device_pluged() > 0) &&

        ((Count100msBase != last_Count100msBase) || (PLC_Last_RunStatus_Reg != PLC_RunStatus_Reg))) // PLC RUN/Stop 发生改变或定时时间到,广播 PLC 运行状态

    {

        last_Count100msBase = Count100msBase;

        // 请求 非周期 异步通讯  发送队列

        // Request_PU_NCClist(&ptxbuf);

        Api_PU_comm_data_creat(&PU_TX_buff,      // 要填充的队列

                               U4_CMD_PLCSTATUS, // 广播通讯

                               PLC_RunStatus_Reg,

                               0x00 // 附加控制码 0x01=优先发送 ;0x03=FIFO 方式发送

        );

        PU_BUS_Send_data(&PU_TX_buff); // todo

    }
```
###### 每4s向从机请求错误信息
```c
if (Get_error_start && (Get_device_pluged() > 0))

        {

            /* 循环请求模块错误信息 */

            cycle_slotcallerr++;

            if (cycle_slotcallerr >= (Get_device_pluged() + SLAVE_SOLT_OFFSET))

            {

                cycle_slotcallerr = SLAVE_SOLT_OFFSET;

                Get_error_start = 0;

                Geterr_comm_time_used_store = Geterr_comm_time_used;

            }

            Api_PU_comm_data_creat(&PU_TX_buff, // 要填充的队列

                                   U4_CMD_GET_ERR,

                                   cycle_slotcallerr,

                                   0 // 附加控制码 0x01=优先发送 ;0x03=FIFO 方式发送

            );

            PU_BUS_Send_data(&PU_TX_buff); // 点对点通讯

                                           // todo 从模块异常处理

            Geterr_comm_time_used += TIMER_PULOOP_CNT_READ;

        }
```
###### 处理从机状态机
```c
if (isDeviceRunning == PNIO_TRUE)

        {

            /* 从模块高频通讯处理 // 周期通讯状态机  */

            Cyc_comm_time_used_store = TIMER_PULOOP_CNT_READ;

            TIMER_PULOOP_RESET;

            Cyc_comm_time_used = TIMER_PULOOP_CNT_READ;

            for (cycle_slotcall = SLAVE_SOLT_OFFSET; cycle_slotcall < (iobus_sulink.device_on_bus + SLAVE_SOLT_OFFSET); cycle_slotcall++) // MAX_SLOT_MODULES

            {

                run_fsm_action(&Slotlist[cycle_slotcall].fsm_h, &Slotlist[cycle_slotcall]); // 循环运行

                if ((TIMER_PULOOP_CNT_READ - Cyc_comm_time_used) > 300)                     // 执行耗时限制, 超时则分割执行

                {

                    OS_WAIT_MS(1); // 任务调度

                    Cyc_comm_time_used = TIMER_PULOOP_CNT_READ;

                    // cycle_wait_flag = PNIO_TRUE;

                }

            }

        }
```
###### 与从机交换io数据
1. 通过状态机函数执行，通过处理下面
```c
unsigned char *outdata;               // 输出数据缓存地址
unsigned char *indata;              // 输入数据缓存地址
```
2. 将需要交换的io数据存储在outdata和indata中
3. `RUN_S_CYCLE_DATA` 确定io初始化