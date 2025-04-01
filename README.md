### 简介
- 暂时没有
```c
			/* event : PLC组态的模块数量与实际安装的数量不一致 */
			if(CONNECTED_PLC_NUMS && (Get_device_pluged() + 4) != ArNumOfPluggedSub)
			{
				if (iomaster_event_list[IOMASTER_EVENT_SLOT_INCONSISTENT].callback != NULL)
				{
					iomaster_event_list[IOMASTER_EVENT_SLOT_INCONSISTENT].callback();
				}
			}
```

```c
#include "common/iobus_pu_protol.h"
case 6:
{

if(PU_comm_count.PU_RX_link_err_count > 200)

{

PU_comm_count.PU_RX_link_err_count = 0;

pu_reinit_callback();

}

}
```

```c
if(PU_comm_count.PU_RX_link_err_count < 0xff)
{
    PU_comm_count.PU_RX_link_err_count++;
}

```