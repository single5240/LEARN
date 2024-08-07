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
