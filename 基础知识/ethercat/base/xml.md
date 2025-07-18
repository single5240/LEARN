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


### `0xF030` - Configured module Ident list
### `0xF050` - Module detected list
