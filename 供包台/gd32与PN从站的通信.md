### 通信协议
#### gd32发给PLC的数据（data_to_PLC）
1. 帧头：`data_to_PLC[0] = 0xAA`
2. 数据长度：`data_to_PLC[1] = 0x40`
3. 数据：`data_to_PLC[2] --- data_to_PLC[65]`
4. crc校验：`data_to_PLC[66] = crc8`

#### gd32通过TCP发给上位机（data_to_TCP）
1. 帧头：`data_to_TCP[0] = 0xBB
2. 数据长度：`data_to_TCP[1] = data_len`
3. 数据：`data_to_TCP[2] --- data_to_PLC[1+len]`
4. crc校验：`data_to_TCP[len+2] = crc8`
