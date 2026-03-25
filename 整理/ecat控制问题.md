### PP 模式下“中途反向”目标位置不响应
- 单点运动，ControlWord 写入 `0x3F`
```c
outputs[slave_id]->controlWord = 0x3F; 
if ((status & 0x1000) == 0x1000) // 等待驱动器接收新指令的应答
{
	run_flag[slave_id] = 4;
}
else
{
	timeout_cnt[slave_id]++;
	if(timeout_cnt[slave_id] >= 1000)
	{
		timeout_cnt[slave_id] = 0;
		run_flag[slave_id] = 0xfe;
	}
}
break;
```
#### 同向中途修改 —— 表现正常
- 电机在左位（1500），主站下发目标到中位（3000），电机开始正向运行
- **干预**：在运行到半路时，把 Target Position 更新为右位（4500），并重新走了一遍 `0x0F -> 0x3F` 的握手时序
- **结果**：驱动器正常响应，电机无感、无停顿地直接加速/平滑运行到了右位（4500）
#### 反向中途修改 —— 驱动器不响应
- 电机在左位（2000），主站下发目标到中位（5000）。电机开始正向运行
- **干预**：在运行到半路时，把 Target Position 设回左位（2000），并重新走了一遍 `0x0F -> 0x3F` 的握手时序
- **结果**：**电机无任何响应，既没有减速也没有反向，而是坚持跑完了原来的目标（中位 5000）才停下**
### 问题
- 不能中途修改反向运动，是配置问题还是流程不对？亦或不支持这个操作
### PP模式控制流程
```c
uint8_t slave_running(uint8_t slave_id)
{
    uint16_t status = inputs[slave_id]->statusWord;

    switch (run_flag[slave_id])
    {
    // ==========================================
    // 阶段 0~1：模式切换与使能状态确认
    // ==========================================
    case 0:
        timeout_cnt[slave_id] = 0;
        outputs[slave_id]->modeOfOperation = 1; // 切换至 Mode 1 (PP 轮廓位置模式)止重复使能，浪费时间
        if(enable_flag[slave_id] == 1)
        {
            run_flag[slave_id] = 1;
        }
        else
        {
            outputs[slave_id]->controlWord = 0x06; // 准备使能 (Shutdown)
            run_flag[slave_id] = 1;
        }
        break;

    case 1: 
        // 确认驱动器已成功切入 PP 模式 (Mode Display == 1)
        if (inputs[slave_id]->modeDisplay == 1) 
        {
            if(enable_flag[slave_id] == 1)
            {
                run_flag[slave_id] = 2; // 已使能，直接进入发指令阶段
            }
            else
            {
                outputs[slave_id]->controlWord = 0x06;
                // 等待 StatusWord 回复 Ready to switch on (0x0021)
                if ((status & 0x006F) == 0x0021)
                {
                    run_flag[slave_id] = 2;
                    enable_flag[slave_id] = 1;
                    delay_cnt[slave_id] = 0; 
                }
            }
        }
        break;

    // ==========================================
    // 阶段 2~4： CiA 402 PP模式握手时序
    // ==========================================
    case 2:
        // 【第一步：制造下降沿并等待驱动器清除旧状态】
        // 下发 ControlWord = 0x0F (Bit 4 New set-point = 0)
        outputs[slave_id]->controlWord = 0x0F; 

        // 检查 StatusWord：
        // 1. 处于 Operation Enabled (0x0027)
        // 2. 驱动器应答位 Bit 12 (Set-point Acknowledge) == 0，表示驱动器已准备好接收新目标
        if (((status & 0x006F) == 0x0027) && ((status & 0x1000) == 0))
        {
            delay_cnt[slave_id]++;
            // 延时保持 0x0F 若干周期，确保驱动器底层 PLC 扫描周期能捕捉到 Bit 4 的低电平
            if (delay_cnt[slave_id] >= 50) 
            {
                delay_cnt[slave_id] = 0;
                run_flag[slave_id] = 3;
            }
        }
        break;

    case 3: 
        // 【第二步：触发新目标位置】
        // 下发 ControlWord = 0x3F 
        // 包含 Bit 4 = 1 (New set-point 上升沿触发)
        // 包含 Bit 5 = 1 (Change set immediately，要求立即抢占覆盖旧目标)
        outputs[slave_id]->controlWord = 0x3F; 

        // 等待驱动器应答：StatusWord Bit 12 (Set-point Acknowledge) 变为 1
        // 代表驱动器已经成功接收新的 Target Position
        if ((status & 0x1000) == 0x1000) 
        {
            run_flag[slave_id] = 4;
        }
        break;

    case 4:
        // 【第三步：撤销触发信号，完成一次完整的握手】
        if(timeout_cnt[slave_id] > 10) // 保持 0x3F 状态 10 个周期，防止短脉冲丢失
        {
            // 将 ControlWord 退回 0x0F，为下一次可能的中途换向做准备
            outputs[slave_id]->controlWord = 0x0F;

            // 等待驱动器释放应答位 (Bit 12 降为 0)
            if ((status & 0x1000) == 0)
            {
                run_flag[slave_id] = 5;
                timeout_cnt[slave_id] = 0;
            }
        }
        else
        {
            timeout_cnt[slave_id]++;
        }
        break;

    // ==========================================
    // 阶段 5：等待电机物理运行到位
    // ==========================================
    case 5:
        // 检查 StatusWord Bit 10 (Target Reached) 是否为 1
        // 表示电机已经物理到达目标位置，且速度降为 0
        if (status & 0x0400)
        {
            run_flag[slave_id] = 0;
            return 0x40; // 返回 0x40 表示动作彻底完成
        }

        // 持续监控错误位 Bit 3 (Fault)
        if (status & 0x0008)
        { 
            run_flag[slave_id] = 0xfe; // 跳转到错误处理
        }
        break;
    }
    
    return run_flag[slave_id];
}
```
###### 正常流程
1. 先发 ControlWord = 0x0F，并等待贵司驱动器回复 StatusWord Bit 12 == 0；
2. 然后下发 ControlWord = 0x3F（开启了 Bit 5 立即生效），制造 New set-point 的上升沿，并等待贵司驱动器回复 Bit 12 == 1；
3. 握手完成后再将控制字恢复为 0x0F。
###### 中途修改流程
1. **更新位置字典**：将新的目标位置写入 `Target Position (0x607A)` 的 PDO 中。
2. 然后**强制制造下降沿**，就是上面的case 2，继续按正常流程走

### 参数计算（主要是确认）
##### 电机一圈对应指令数![[Pasted image 20260316202952.png]]
##### 参数单位及其计算
![[Pasted image 20260316203309.png]]
1. 这些参数单位都是一致的吗，都是指令单位？
2. 607Fh最大轮廓速度和6080h最大电机速度可以修改吗？有必要修改吗？修改的依据是什么？
