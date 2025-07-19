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

![[Pasted image 20250719100156.png]]