### PE1637_wait_slot_init
1. 小车slot相关初始化，现采用本地参数手动plug，后续改为自动plug（通过pn主站控制）
2. 小车对应串口初始化，并 更新对应标志位`PortInitStatus`

### **PE1637_ack_dispose_Loop**
1. PE1637的**接收轮询处理**
2. 该函数的接收处理是**根据预设的驱动器类型**进行指定数据长度的接收与校验
	- 预设的驱动器类型通过[[usr函数---OBJ#`slot_index_mid00b1`]]配置

### Solt0RecodParam_dispose
1. 主模块参数配置
