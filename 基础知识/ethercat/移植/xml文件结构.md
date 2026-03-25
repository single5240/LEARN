# 文件结构
## 1-Vendor
- **Vendor（厂商信息）**：定义设备制造商的唯一身份，包含 ETG 分配的 **Vendor ID**、厂商名称及图标。
### 1.1-ID
- 是一个由 EtherCAT 技术协会（ETG）分配的唯一数值（例如倍福的 ID 是 `0x2`）。主站扫描总线时，会读取从站硬件寄存器中的 Vendor ID 与此匹配，即代码中的宏定义`VENDOR_ID`
### 1.2-Name
- 厂商的文本名称
### 1.3- ImageData16x14
- 十六进制格式的图标数据。导入 XML 后，你在主站配置界面看到的厂商 Logo 就来自这里。
## 2-Descriptions

- **Descriptions（设备描述）**：定义具体的硬件型号、通信参数（PDO/SDO）、内存分配（SM/FMMU）以及分布式时钟（DC）配置。
### 2.1-Groups
- 设备分组，即公司旗下不同产品线，比如 “I/O模块”组和“驱动器”组
### 2.2-Devices
- 每个 `<Device>` 标签对应一个具体的硬件产品，每一个都包含以下信息
#### 2.2.1-**Type (Product Code & Revision)**：
- **Product Code**：产品型号代码
- **Revision Number**：版本号
- 主站靠这两个值锁定唯一的硬件定义。
#### 2.2.2-Name
- 设备的**唯一显示名称**
#### 2.2.3-Info
- 提供**人类可读的额外信息**
#### 2.2.4-GroupType
- 将设备**归类到特定的文件夹**下
#### 2.2.5-Profile
- 定义设备遵循的 **应用层协议规范** 以及其**对象字典（Object Dictionary）**
##### 2.2.5.1-ChannelInfo
```html
<ChannelInfo><ProfileNo>5001</ProfileNo></ChannelInfo>
```
- 用于定义设备的**通道元数据**
- 这里必须加上5001，TwinCAT 才会自动显示 **"Slots"（插槽）** 选项卡，允许用户动态添加/删除子模块
- `ProfileNo`该通道遵循的**设备规范编号**。对于 `5001` 这个特定数字，它代表的是 **EtherCAT 模块化设备规范 (Modular Device Profile, MDP)**。让主站（如 TwinCAT）知道：“这个设备遵循 ETG.5001 标准，请开启模块化解析模式”。
##### 2.2.5.2 Dictionary
- 对象字典的容器，包含了从站所有的可访问参数
###### 2.2.5.2.1-DataTypes
- 相当于 C 语言中的 `typedef` 或 `struct` 定义。它不占用内存，只定义规则。
- 有一些标准的类型，比如BOOL、UINT等，也可以自己定义一些复杂的
- 每个类型基本包括`name`和`bitsize`，复杂类型多一些描述对应的标签（主要注意偏移是否正确）
###### 2.2.5.2.2-Objects
1. 存放所有字典对象的实例，必须出现在这里，主站（Master）才能通过 SDO 访问它，才能在图形界面中对其进行配置。
	- 模块化设备略有不同，但本质是一样的·，后续分享module时会解释
2. 关键属性说明：
	- **`<Index>`**：十六进制地址（如 `#x6040`）。
	- **`<Name>`**：对象的文本描述（如 `Controlword`）。
	- **`<Type>`**：指向 `<DataTypes>` 中定义好的类型名称。
	- **`<BitSize>`**：该对象的总长度。
	- **`<Flags>`（标志位）**：**极其重要**，它决定了主站如何对待这个对象：
		- **`<Access>`**：访问权限（`ro` 只读, `wo` 只写, `rw` 读写）。
		- **`<Pdo>`**：决定该对象是否可以被映射进 PDO（`TR` 代表可映射进 TxPDO，`RW` 代表可映射进 RxPDO，`n` 代表不可映射）。
		- **`<Backup>`**：决定该参数是否需要掉电保存。
#### 2.2.6-RxPdo/TxPdo
- 这里主要分析模块化设备，详细分析在后面module中
#### 2.2.7-FMMU
- 3个FMMU，分别是Outputs、Inputs、MBoxState
- 其中，**FMMU 0** 通常关联 **SM 2**（输出），**FMMU 1** 通常关联 **SM 3**（输入）
#### 2.2.8-SM
- 4个SM，分别是MBoxOut、MBoxIn、Outputs、Inputs
#### 2.2.9-Mailbox
```html
<Mailbox DataLinkLayer="true"><CoE SdoInfo="true" SegmentedSdo="true" CompleteAccess="true" PdoAssign="true" /></Mailbox>
```
- **基础使能**：开启了基于数据链路层的信箱服务。
- **字典查询 (`SdoInfo`)**：允许主站在线读取从站的字典列表及描述。
- **大数据传输 (`SegmentedSdo`)**：支持传输超过信箱缓冲区长度的数据（如长字符串）。
- **批量访问 (`CompleteAccess`)**：支持一次性读写某个对象的所有子索引。
- **动态配置 (`PdoAssign`)**：**动态 PDO 的开关**，允许主站重新分配 PDO。
#### 2.2.10-DC
```html
<Dc>
	<OpMode>
		<Name>Synchron</Name>
		<Desc>SM-Synchron</Desc>
		<AssignActivate>#x0</AssignActivate>
		<CycleTimeSync0 Factor="1">0</CycleTimeSync0>
		<ShiftTimeSync0>0</ShiftTimeSync0>
		<CycleTimeSync1 Factor="1">0</CycleTimeSync1>
	</OpMode>
	<OpMode>
		<Name>DC</Name>
		<Desc>DC-Synchron</Desc>
		<AssignActivate>#x300</AssignActivate>
		<CycleTimeSync0 Factor="1">0</CycleTimeSync0>
		<ShiftTimeSync0>0</ShiftTimeSync0>
		<CycleTimeSync1 Factor="1">0</CycleTimeSync1>
	</OpMode>
</Dc>
```
- 同步模式，主要分为三种，SM同步、DC同步、free run
- 直接删掉整个DC标签，扫描后发现没有 DC 描述，会自动切换到 Free Run
#### 2.2.11-Slots
- 定义从站**所有插槽**相关参数
- **`SlotIndexIncrement`**：定义相邻插槽之间**对象字典索引**（如 $0\text{x}6000, 0\text{x}7000$）的跳变步长，代码中的宏定义是`SlotIndexIncrement`。
- **`SlotPdoIncrement`**：定义相邻插槽之间 **PDO 映射对象索引**（如 $0\text{x}1600, 0\text{x}1\text{A}00$）的跳变步长，代码中的宏定义是`SlotPdoIncrement`。
- **`IdentifyModuleBy`**：规定主站通过什么“证据”来确认物理插槽里的模块是正确的（通常是 ID 匹配）。
- **`DownloadModuleIdentList`**：指令开关，让主站在启动时把“预期的模块清单”下载给从站，以便从站自检。
###### 2.2.5.5.1-Slot
```html
	<Slots SlotIndexIncrement="#x40" SlotPdoIncrement="8" IdentifyModuleBy="ModuleIdent" DownloadModuleIdentList="1">
				<Slot MinInstances="1" MaxInstances="32" SlotIndexIncrement="#x1" SlotPdoIncrement="#x1">
```
- 定义单个插槽类型相关参数，设定和**Slots相同参数**，会覆盖对应参数
	- 比如上面`Slots`中的`SlotIndexIncrement`会被`Slot`中的`SlotIndexIncrement`覆盖掉
- `name`定义在看到的名称
- `moduleclass`展示不同的`module`分类，后续`module`定义中会用到
#### 2.2.12-Eeprom
- `ByteSize`：规定 EEPROM 的**物理容量**，决定了从站能存储多少配置信息
- `ConfigData`：一组**十六进制字节流**，直接映射到 ESC 的核心硬件寄存器（如 PDI 类型、同步脉冲长度等），需要参考esc芯片手册
### 2.3-Modules
#### 2.3.1-Module
- 一个完整的 `<Module>` 定义就像是一个微缩版的 `<Device>`
- 将具体的功能逻辑（如 16 路输入、4 路模拟量）从主设备定义中抽离出来，形成独立的组件。
- 每个模块包含了自己专属的**对象字典（SDO）**、**过程数据映射（PDO）以及安全校验码（ModuleIdent）**
- 本身不占用总线地址，只有当它被主站软件“拖拽”进某个 `<Slot>`（插槽）时，它才会根据插槽的偏移量生成真正的物理地址，所以可以看到地址都是0x6000、0x7000等，当生成实体到插槽中时，具体地址才会自动加上具体的偏移
- 定义一次可以重复使用，比如你只需要定义一次“8通道输入模块”，就可以在同一个耦合器上挂载 10 个这样的模块，而不是为这10个模块都编写对应的字典。
##### 2.3.1.2-type
- `ModuleClass`就是上面`slot`中定义的`moduleclass`
- `ModuleIdent`是模块唯一 ID。主站会读取从站对象字典 0xF030 来比对硬件是否匹配。从站也有主动识别模块将对应模块ID更新到对象字典0xF050 
- `ModulePdoGroup="1"`将此模块的 PDO 归类，便于主站进行同步管理
##### 2.3.1.2-RxPdo/TxPdo
- 在非模块化设备中，应该在device下，定义与主站交换数据的名单
- RxPdo 是主站发给从站的指令（接收）；TxPdo 是从站回传给主站的状态（发送）
- `Fixed="1"` (静态映射)，`Fixed="0"` (动态映射)
- `Sm="2"`RxPdo绑定到sm2，`Sm="3"`TxPdo绑定到sm3，**不能写错**
- `Index`：PDO 映射对象的索引。RxPdo 通常在 $0\text{x}1600$ 到 $0\text{x}17\text{FF}$；TxPdo 在 $0\text{x}1\text{A}00$ 到 $0\text{x}1\text{B}\text{FF}$
- `DependOnSlot="1"`：- **模块化设备特有**。它告诉主站：“请根据插槽编号给我的索引加上偏移量（Increment）”
- `<Entry>` 是 PDO 里的最小单位，它定义了具体哪块内存被搬运
	- **`<Index>` & `<SubIndex>`**：指向对象字典中存储实际数据的地址（如 $0\text{x}7000:01$）
	- **`<BitLen>`**：定义传输的长度，必须与对象字典里对应数据类型的长度**严格一致**
##### 2.3.1.3-Profile
- 和device中的`Profile`基本一样，但是一般只定义模块独有的类型和实例
