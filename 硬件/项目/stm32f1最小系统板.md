### 原理图
#### 时钟设计
1. Crystal/Ceramic Resonator
~~~
1. 频率范围：
	F101xx->F103xx：f∈[4, 16];
	f100xx：f∈[4, 24];
	F105xx/F107xx：f∈[3, 25];
2. PCB设计：
	a. 晶振和电容PCB布线时尽可能地靠近OSC引脚；
	b. CL1和CL2的容值通常相同，官方建议容值范围在[5pF, 25pF]；
	c. CL = CL1 x CL2 / (CL1 + CL2) + Cstray，其中：
	Cstray：pin、板卡、PCB布线的typ[2pF, 7pF]，选型计算时，可以粗略认为Cstray为10pF；
	CL1和CL2：查看晶振规格书给出的CL，带入公式计算得出；
~~~
