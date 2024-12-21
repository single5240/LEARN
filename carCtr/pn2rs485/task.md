### `Init_SU_UARTcomm_App();`监控线程
#### 
### `Init_PU_UARTcomm_App();`
#### `PE1637_slot_flow_Loop();`
- 串口发送控制循环，包含两个串口
#### `PE1637_ack_dispose_Loop();`
- 接收轮询接收轮询处理
* Note: 该函数的接收处理是根据预设的驱动器类型进行指定数据长度的接收与校验
* 发送与接收的同步通过`CommAction_toget`控制，发送之后将其置1
* 