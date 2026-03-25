## 1. 定义模块类型与数据结构

在 `SSC-9252Objects.h` 中，为新模块建立“内存模型”。
- **定义宏 ID**：分配一个唯一的 `M_TYPE` 标识符。
- **内存对齐**：结构体必须符合 **2 字节（Word）对齐**。若原始数据位宽为奇数字节（如 24 位），必须手动添加 `u8Padding` 凑成偶数，否则 LAN9252 硬件会报 `0x0017` 错误。
```c
// 示例：添加 16路输入 + 16路输出混合模块 (16DI16DO)
#define M_TYPE_16DI16DO    0x12 

typedef struct OBJ_STRUCT_PACKED_START {
    UINT16 u16SubIndex0;
    UINT16 u16Data;       // 16位输出数据
} OBJ_STRUCT_PACKED_END T16DO_Data;

typedef struct OBJ_STRUCT_PACKED_START {
    UINT16 u16SubIndex0;
    UINT16 u16Data;       // 16位输入数据
} T16DI_Data;
```
## 2. 创建对象字典描述符与名称表

描述符是“万能映射函数”动态提取位宽（BitLength）的唯一数据源。
- **asED 描述符**：`BitLength` 必须与实际物理位宽（8, 16, 24, 32）严格一致。
- **aName 名称表**：使用 `\000` 分隔子索引名，以 `\377` 结束。
```c
// 输出数据描述符 (0x70n0)
OBJCONST TSDOINFOENTRYDESC OBJMEM asED16Ox6_70n0[] = {
    {DEFTYPE_UNSIGNED8, 0x8, ACCESS_READWRITE},  // Sub 0: 条目数
    {DEFTYPE_UNSIGNED16, 0x10, ACCESS_READWRITE} // Sub 1: 16位数据长度
};

// 输出映射描述符 (0x16n0)
OBJCONST TSDOINFOENTRYDESC OBJMEM asED16Ox16_An0[] = {
    {DEFTYPE_UNSIGNED8, 0x8, ACCESS_READWRITE},  // Sub 0
    {DEFTYPE_UNSIGNED32, 0x20, ACCESS_READWRITE} // Sub 1: 映射目标
};

// 名称字符串定义
OBJCONST UCHAR OBJMEM aName16DO[] = "16DO Outputs\000Ch0-15\000\377";
OBJCONST UCHAR OBJMEM aName16DOMAP[] = "16DO RxPDO-Map\000\377";
```
## 3. 配置槽位安装逻辑
在 `plug_slot_to_ecatdic` 的 `switch(m_type)` 中添加分支。**只需“填表”描述参数，无需编写调用函数。**
```c
case M_TYPE_16DI16DO:
    has_out = 1; has_in = 1; // 声明该模块拥有输入和输出
    
    // 输出参数填充
    out_sub_cnt = 1; 
    out_map_size = sizeof(T16OBJ_Map); out_data_size = sizeof(T16DO_Data);
    pOutMapDesc = asED16Ox16_An0; pOutMapName = aName16DOMAP;
    pOutDataDesc = asED16Ox6_70n0; pOutDataName = aName16DO;
    
    // 输入参数填充
    in_sub_cnt = 1;
    in_map_size = sizeof(T16OBJ_Map); in_data_size = sizeof(T16DI_Data);
    pInMapDesc = asED16Ix16_An0; pInMapName = aName16DIMAP;
    pInDataDesc = asED16Ix6_70n0; pInDataName = aName16DI;

    configName = ModuleConfig16DI16DO; 
    break;
```
## 4. 实现过程数据映射 (Mapping)
在 `APPL_InputMapping` 和 `APPL_OutputMapping` 中处理硬件缓冲区与过程数据区的搬运。
> **核心计算公式**：
> 指针偏移量 $L_{offset} = \frac{\text{DataStructureSize}}{2}$ (由于 `pTmpData` 类型为 `UINT16*`)。
```c
// APPL_OutputMapping 示例
case M_TYPE_16DI16DO:
    if(module_ctr[slot_index].outdata != NULL) {
        // 将主站过程数据拷贝至从站局部缓冲区
        module_ctr[slot_index].outdata[0] = (*pTmpData) & 0xFF;
        module_ctr[slot_index].outdata[1] = (*pTmpData) >> 8;
        pTmpData += 1; // 16位数据移动 1 个 UINT16
    }
    break;
```
## 5. 编写 ESI (XML) 文件

确保 XML 的物理描述与代码逻辑 **100% 同步**。（参考已有模块，在其基础上修改）
1. **ModuleIdent**：必须匹配代码中的 `moduleId`。
2. **RxPdo/TxPdo 配置**：
    - `BitLen` 必须严格匹配 `asED` 中的位宽定义。
    - **关键点**：若代码结构体中为了对齐补了 `Padding`，XML 必须显式增加一个 8 位的 `Entry` 以凑齐偶数字节长度。否则状态机切换会卡在 `PREOP -> SAFEOP`。