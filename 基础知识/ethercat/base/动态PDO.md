
动态PDO映射的基本原理是操作对象字典的0x1C12和0x1C13对象，这两个对象分别管理输出和输入的PDO映射。过程如下：
- 将Ethercat状态机切换到PreOP状态，此状态可以用SDO来配置PDO映射；
- 清除PDO指定对象的PDO映射对象，即设置0x1C12-00,与0x1C13-00为0；
- PDO映射对象无效，即对0x1600-0x1603/0x1A00-0x1A01的子索引设置为0；
- 重新配置PDO映射内容；0x1600-01开始的是RxPDO内容，0x1A00-01开始的是TxPDO；
- 设置PDO映射对象总数；
- 写有效的PDO映射对象

### 修改xml
- 通过ssc工具生成新的代码时，只需要替换
#### eeprom
- `800E00CC8813f000000000800000`
#### 同步管理器映射（0x1C12/0x1C13）读写权限


### 修改从站源码

#### `SDOS_SdoInd`
1. 该函数接收到主站的sdo数据会和本地静态数据比较，再写入ESC
2. 需要将收到与本地不同的数据时，检查配置参数，然后将其加载
3. 增加标志位，通知主程序重新映射
4. 动态pdo一般只修改0x1C12/0x1C13（同步管理器映射），指向不同的PDO映射参数（比如0x1600/0x1A00）
5. 修改完同步管理器映射后，需要重新加载PDO映射参数，新配置需在从站从 Pre-Op/Safe-Op状态切换到Op状态 时激活
6. 暂时不支持动态修改PDO映射参数
##### 新的sdo数据
###### 确定是否与本地存储的sdo数据不一样 
1. 每个参数逐一比较，0x1C12/0x1C13
2. 如果是新的，加载到flash中，并设置相关标志位
3. 需要从链表中将不需要的对象拉出来
##### 构建并发送SDO响应报文到主站
```c
if(abort != ABORTIDX_WORKING)
{
	/*  type cast was added because of warning */
	SdoRes(abort, command, (UINT8) (sdoHeader & SDOHEADER_COMPLETEACCESS), (UINT16) dataSize, objLength, pSdoInd);
}
```
#### 字典操作
##### 清空字典对象 `void COE_ClearObjDictionary(void)` 
##### 返回字典对象指针`OBJCONST TOBJECT OBJMEM * COE_GetObjectDictionary(void)` 
##### 添加对象到字典 `UINT16 COE_AddObjectToDic(TOBJECT OBJMEM * pNewObjEntry)`
##### 从字典移除对象 `void COE_RemoveDicEntry(UINT16 index)`
##### 批量添加对象到字典 `UINT16 AddObjectsToObjDictionary(TOBJECT OBJMEM * pObjEntry)`
##### 静态初始化字典 `UINT16 COE_ObjDictionaryInit(void)`
- **修改为动态加载，实现掉电保存主站sdo配置**

