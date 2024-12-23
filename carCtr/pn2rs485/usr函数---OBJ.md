### `ertec_board_init`


### `MID00B1_IO_PortCommIOData`
- io数据交换，主要是将`InData`和`OutData`数据**处理并更新**到小车控制结构体
	- todo:  做通用化处理
- 在[[task#`PE1637_slot_flow_Loop();`]]中调用，周期数据处理
### `MID00B1_IO_PortCommIOData_flag`
1. 在[[pn函数#`PnUsr_cbf_IoDatXch`]]  中调用，用以提高小车启动信号响应的实时性

### `slot_index_mid00b1`
- 非周期数据在`Solt0RecodParam_dispose`中调用，用以配置小车的参数

### `MID00B1_IO_PortCommIOData_upload`
- 在[[task#`PE1637_slot_flow_Loop();`]]中调用，更新`InData`数据，但是功能貌似与[[usr函数---OBJ#`MID00B1_IO_PortCommIOData`]]中部分重复

