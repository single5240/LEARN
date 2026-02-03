### 脉冲控制函数
#### 1.绝对位置 `uint8_t plan_buffer_line(float *target, plan_line_data_t *pl_data)`
#### 2.速度控制 `uint8_t jog_execute(plan_line_data_t *pl_data, parser_block_t *gc_block)`
#### 3.回零循环 `void limits_go_home(uint8_t cycle_mask)`
