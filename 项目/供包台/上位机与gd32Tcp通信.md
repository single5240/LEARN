1. test


```c
uint8_t testCtr = 0;
uint8_t count = 0;


if(testCtr == 1)
    	{
    		count++;
    		LOG_RAW("[%d]-[%d]",TIMER_COMM_CNT_READ, count);
			TIMER_COMM_RESET
    	}

extern uint8_t testCtr;
if(testCtr == 1)
	{
		testCtr = 0;
	} else
	{
		testCtr = 1;
	}

```
