# 外部链接
 1. [PROFINET工业以太网教程（16）-GSDML文件详解 - 知乎](https://zhuanlan.zhihu.com/p/562799047)

# 结构
![[Pasted image 20250328105554.png]]

# 细节
## profile header
![[Pasted image 20250328105516.png]]
![[Pasted image 20250328100232.png]]
## profile header
![[Pasted image 20250328100318.png]]
## profile body
![[Pasted image 20250328105654.png]]
### device identity
![[Pasted image 20250328105756.png]]
```html
<DeviceIdentity VendorID="" DeviceID="">
<!-- VendorID U16H 由PI分配 , DeviceID U16H由供应商分配 -->
<InfoText TextId="" />
<VendorName Value="" /><!--供应商名称-->
</DeviceIdentity>
```
### device function
![[Pasted image 20250328110144.png]]
```html
<DeviceFunction>            <!-- 设备功能 -->  
<Family MainFamily="I/O" ProductFamily="PN IO Device " />  
<!--PN标准设备分类：IO设备，供应商产品分类：产品系列-->  
</DeviceFunction>
```
![[Pasted image 20250328110251.png]]
### application process
- 结构图 
	- ![[Pasted image 20250328110751.png]]
#### Device Access Point List
- 结构图
	- ![[Pasted image 20250328110903.png]]
	- ![[Pasted image 20250328111240.png]]
##### Device Access PointItem
###### 1. `ID="DAP 1"`
- 作用：设备访问点的唯一标识符，用于工程工具或配置中引用此DAP。
###### 2. `PhysicalSlots="0"`
- 含义：设备在机架/背板上的物理槽位号（0表示单模块设备，无扩展槽位）。
###### **3. `ModuleIdentNumber="0x0000040"`**
- 作用：设备的模块标识号（十六进制），用于唯一标识硬件类型或固件版本。
###### 4. `MinDeviceInterval="4"`
- 含义：设备支持的最小通信周期为**4ms**，控制器需以此或更慢的周期通信。
###### 5. `ImplementationType="ERTEC200P-3"`
- 作用：硬件实现类型，此处为西门子PROFINET控制器芯片型号（ERTEC200P-3）。
###### 6. `DNS_CompatibleName="servo_driver"`
- 含义：设备的DNS兼容名称（可读名称），用于网络识别（如 `servo_driver.local`）。
###### 7. `FixedInSlots="0"`
- 作用：设备固定在物理槽位0（不可移动或插拔）。
###### 8. `ObjectUUID_LocalIndex="1"`
- 含义：设备UUID（通用唯一标识符）的本地索引，用于对象寻址。
###### 9. `MultipleWriteSupported="true"`
- 作用：设备支持同时写入多个参数（提升配置效率）。
###### 10. `SharedDeviceSupported="true"`
- 含义：设备支持被多个控制器共享（适用于冗余或分布式控制）。
###### 11. `DeviceAccessSupported="true"`
- 作用：允许通过PROFINET访问设备内部数据（如诊断、非实时数据）。
###### 12. `NumberOfDeviceAccessAR="1"`
- 含义：设备支持**1个**实时通信关系（AR，Application Relationship）。
###### 13. `MaxSupportedRecordSize="8192"`
- 作用：设备参数化数据（如GSD文件中的记录）最大支持**8KB**大小。
###### 14. `NameOfStationNotTransferable="true"`
- 含义：设备名称（如 `servo_driver`）不可通过DCP协议修改（需硬件配置）。
###### 15. `ParameterizationSpeedupSupported="false"`
- 作用：**不支持**参数化加速（设备启动时需完整参数下载）。
###### 16. `LLDP_NoD_Supported="true"`
- 含义：支持LLDP（链路层发现协议）的“网络设备发现”（NoD）功能，用于拓扑识别。
###### 17. `ResetToFactoryModes="2"`
- 作用：恢复出厂设置的模式代码（如模式2可能表示“保留部分配置”）。
###### 18. `CheckDeviceID_Allowed="true"`
- 含义：允许控制器验证设备ID是否匹配（防止错误替换设备）。
###### 19. `PowerOnToCommReady="800"`
- 作用：设备上电到通信就绪的时间为**800ms**（启动时间指标）。
###### 20. `IOXS_Required="false"`
- 含义：设备**不需要**IO数据状态扩展（IOXS），仅传输原始数据。
###### 21. `RequiredSchemaVersion="V2.35"`
- 作用：设备要求的PROFINET GSD文件架构版本（需与工程工具兼容）。
###### 22. `PNIO_Version="V2.35"`
- 含义：设备支持的PROFINET IO协议版本为**V2.35**。
###### 23. `PrmBeginPrmEndSequenceSupported="true"`
- 作用：支持参数化时的 `BeginPrm`/`EndPrm` 指令序列（确保参数完整性）。
###### 24. `CIR_Supported="true"`
- 含义：支持**CIR**（Controller Initiated Request），允许控制器主动请求数据。
###### 25. `AddressAssignment="LOCAL;DCP"`
- 作用：设备地址分配方式为：
    - LOCAL：本地手动设置（如拨码开关）
    - DCP：通过PROFINET发现协议动态分配
##### Module Info
###### 1. `<ModuleInfo> <!-- CategoryRef="CT_Category_C_Series" -->`
- 作用：定义模块（或设备）的元数据集合，包含名称、版本、厂商等信息
- 注释：引用分类标识符（如 CT_Category_C_Series），表示设备所属的类别（例如“C系列产品”），用于工程工具中的分类筛选
###### 2.` <Name TextId="" />`
- 作用：模块的显示名称，但通过 TextId 引用外部文本资源（而非直接写死名称）
- 注释说明：实际名称需从外部文本列表中根据键值解析，便于多语言支持或集中维护
###### 3. `<InfoText TextId="" />`
- 作用：模块的详细描述文本，同样通过 TextId 引用外部资源
- 典型内容：可能包含设备功能、适用场景等说明
###### 4. `<VendorName Value="Guangdong QiYuan Innovation Co.,Ltd" />`
- 作用：明确设备制造商名称，此处为广东启元创新科技有限公司
###### 5. `<OrderNumber Value="PE-1637" />`
- 作用：设备的订单号或型号标识符，用于采购、替换或文档引用
###### 6. `<HardwareRelease Value="V0.3" />`
- 作用：硬件版本号（如 V0.3），用于区分硬件修订或改进批次
###### 7.` <SoftwareRelease Value="V0.5" />`
- 作用：软件（固件）版本号（如 V0.5），标识设备当前运行的内部程序版本

##### Subslot List
```html
<SubslotItem SubslotNumber="" TextId="" />  
<SubslotItem SubslotNumber="" TextId="" />  
<SubslotItem SubslotNumber="" TextId="" />
```
##### IO Config Data
```html
   <IOConfigData MaxInputLength="" MaxOutputLength="" MaxDataLength="" />
```
##### Useable Modules
```html
<UseableModules>  
<ModuleItemRef ModuleItemTarget="MID_CD00B1" AllowedInSlots="1..4" />  
<ModuleItemRef ModuleItemTarget="MID_CD00C1" AllowedInSlots="1..4" />  
</UseableModules>
```
##### Virtual Submodule List
###### 