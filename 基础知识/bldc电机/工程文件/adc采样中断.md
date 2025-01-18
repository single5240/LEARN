### 处理函数
1. 获取adc电流采样值
2. Clark变换 adc采样值
3. cos sin计算
4. park变换
5. 拿到速度pid的输出 iq 
6. 设置id = 0
7. 将iq、id进行电流pid计算
8. 将电流pid输出的Vd、Vq进行反park变换
9. 然后将反park变换的Voltage_Alpha_Beta进行SVPWM
10. 进行PLL算法
11. 更新电机的码盘计数值
### 采样方案
![[Pasted image 20240611110402.png]]
1. 采样要与 PWM 周期同步
2. 对电流采样进行精确定时，以便在波形的中点进行采样。在波形的中点，瞬时电流等于 PWM 周期的平均值，测量结果不包括任何 PWM 开关纹波电流。