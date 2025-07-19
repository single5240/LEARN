### `0x1000` - Device Type
### `0x1001` - Error register
### `0x1008` - Device name
### `0x1009` - Hardware version
### `0x100a` - Software version
### `0x1C00` - Sync manager type
### `0x1018` - Identity
### `0x10F1` - Error setting
### `0x1C32` - SM output parameter
### `0x1C33` - SM input parameter
### `0x1C12` - RxPDO assgin
### `0x1C13` - TxPDO assgin
### `0x8000` - Error Module

### `0xf000` - Modular device profile
```c
<Object>
	<Index>#xf000</Index>
	<Name>Modular device profile</Name>
	<Type>DTF000</Type>
	<BitSize>48</BitSize>
	<Info>
	  <SubItem>
		<Name>SubIndex 000</Name>
		<Info>
		  <DefaultData>02</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>Module index distance</Name>
		<Info>
		  <DefaultData>0800</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>Maximum number of modules</Name>
		<Info>
		  <DefaultData>02</DefaultData>
		</Info>
	  </SubItem>
	</Info>
	<Flags>
	  <Access>ro</Access>
	  <Category>o</Category>
	</Flags>
</Object>

```
- 模块化设备配置文件对象包含解释模块的功能区域中的对象的所有信息。该对象是只读的，不能进行PDO映射。
#### Entries
![[Pasted image 20250719101928.png]]
1. 模块之间的间隔（0x7000和0x6000）
2. 模块最大数
3. 32位，模块化设备配置对象0x8nn0（模块标识）的子索引可用性定义
4. 32位，模块化设备配置对象0x9nn0（模块标识）的子索引可用性定义
5. 暂时不用
### `0xF010` - Module profile list
```xml
<Object>
	<Index>#xf010</Index>
	<Name>Module profile list</Name>
	<Type>DTF010</Type>
	<BitSize>1040</BitSize>
	<Info>
	  <SubItem>
		<Name>SubIndex 000</Name>
		<Info>
		  <DefaultData>01</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 001</Name>
		<Info>
		  <DefaultData>001a</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 002</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 003</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 004</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 005</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 006</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 007</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 008</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 009</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 010</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 011</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 012</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 013</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 014</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 015</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 016</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 017</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 018</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 019</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 020</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 021</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 022</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 023</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 024</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 025</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 026</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 027</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 028</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 029</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 030</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 031</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 032</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	</Info>
	<Flags>
	  <Access>ro</Access>
	  <Category>o</Category>
	</Flags>
</Object>
```
#### Entries
![[Pasted image 20250719110111.png]]
### `0xF030` - Configured module Ident list
```xml
<Object>
	<Index>#xf030</Index>
	<Name>Configured module Ident list</Name>
	<Type>DTF030</Type>
	<BitSize>1040</BitSize>
	<Info>
	  <SubItem>
		<Name>SubIndex 000</Name>
		<Info>
		  <DefaultData>01</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 001</Name>
		<Info>
		  <DefaultData>001a</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 002</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 003</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 004</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 005</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 006</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 007</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 008</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 009</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 010</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 011</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 012</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 013</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 014</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 015</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 016</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 017</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 018</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 019</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 020</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 021</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 022</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 023</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 024</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 025</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 026</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 027</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 028</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 029</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 030</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 031</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 032</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	</Info>
	<Flags>
	  <Access>ro</Access>
	  <Category>o</Category>
	</Flags>
</Object>
```
#### Entries
![[Pasted image 20250719110426.png]]
- 数据 - {插入模块数量}{第1个槽位模块ID}{第2个槽位模块ID}........
### `0xF050` - Module detected list
```xml
<Object>
	<Index>#xf050</Index>
	<Name>Module detected list</Name>
	<Type>DTF050</Type>
	<BitSize>1040</BitSize>
	<Info>
	  <SubItem>
		<Name>SubIndex 000</Name>
		<Info>
		  <DefaultData>01</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 001</Name>
		<Info>
		  <DefaultData>001a</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 002</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 003</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 004</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 005</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 006</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 007</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 008</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 009</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 010</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 011</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 012</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 013</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 014</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 015</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 016</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 017</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 018</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 019</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 020</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 021</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 022</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 023</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 024</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 025</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 026</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 027</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 028</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 029</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 030</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 031</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	  <SubItem>
		<Name>SubIndex 032</Name>
		<Info>
		  <DefaultData>0000</DefaultData>
		</Info>
	  </SubItem>
	</Info>
	<Flags>
	  <Access>ro</Access>
	  <Category>o</Category>
	</Flags>
</Object>
```
#### Entries
![[Pasted image 20250719113219.png]]
- **模块标识号（Module Ident）**：
	- 通常由两部分组成：高16位为厂商ID（Vendor ID），低16位为产品代码（Product Code）。
	- 示例：0x00020001（厂商ID=0x0002，产品代码=0x0001）。
### 各种设备是否需要配置对应参数（M-必须；C-可选）

![[Pasted image 20250719100156.png]]
- 主要分析模块化设备（主设备基座）和模块设备（可插拔子模块）
- **模块设备本身不生成独立ESI文件**。其配置信息被整合到所属模块化设备的ESI文件中，通过`<Module>`标签描述
#### 热插拔流程参考
```
模块插入->>基座： 检测物理连接 
基座->>模块： 读取SII (0x0000-0x00FF) 
基座-->>ESI数据库： 查询ProductCode=0xB201的配置 
ESI数据库-->>基座： 返回PDO映射/参数定义 
基座->>主站： 发送AL Event(Module Changed) 
主站->>基座： SDO下载新PDO映射
```
