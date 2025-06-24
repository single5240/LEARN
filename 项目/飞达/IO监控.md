### 输入
```c
uint8_t item_detach_home; // 分离限制
uint8_t item_detach_limit; // 分离限制
uint8_t item_send_up; // 出料触发
uint8_t item_send_down; // 出料触发
uint8_t item_reclaim_up; // 回收触发
uint8_t item_reclaim_down;  // 回收触发

uint8_t item_clip_home; // 夹膜气缸原位
uint8_t item_clip_arrival; // 夹膜气缸到位
uint8_t item_stretch_home; // 伸缩气缸原位
uint8_t item_stretch_arrival; // 伸缩气缸到位
uint8_t item_roll_arrival; // 滚轮压膜气缸到位
uint8_t new_item_arrived; // 物料到达指定位置
uint8_t send_fixed_button; // 发送轴固定物料气阀
uint8_t reclaim_fixed_button;  //回收轴固定物料气阀

uint8_t m_send_warning; // 发送步进报警
uint8_t m_reclaim_warning; // 1回收步进报警
uint8_t m_detach_warning; // 2回收步进报警
uint8_t m_roll_warning; // 刮刀脱离步进报警

uint8_t ask_for_new_item;
uint8_t ask_for_detach_item;
uint8_t reset_sign;
uint8_t run_sta; // 0: 停止，1: 运行

```