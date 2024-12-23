### `ertec_board_init`


### `MID00B1_IO_PortCommIOData`
- io数据交换，主要是将`InData`和`OutData`数据**处理并更新**到小车控制结构体
	- todo:  做通用化处理
### `MID00B1_IO_PortCommIOData_flag`
1. 在[[pn重要函数#`PnUsr_cbf_IoDatXch`]]  中调用，用以提高小车启动信号响应的实时性
2. 