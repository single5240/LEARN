## 资料
1. [技术说明 | 霍尔传感器 | 产品 | 旭化成微电子 (AKM)](https://www.akm.com/cn/zh-cn/products/hall-sensor/tutorial/)
2. [三相交流异步电动机的结构与工作原理 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/506365761)
3. [SPWM基本原理详解（图文并茂+公式推导+C程序实现）-CSDN博客](https://blog.csdn.net/u010632165/article/details/110889621)
4. [写一个比SimpleFOC更好的库 (dengfoc.com)](http://dengfoc.com/#/dengfoc/%E7%81%AF%E5%93%A5%E6%89%8B%E6%8A%8A%E6%89%8B%E6%95%99%E4%BD%A0%E5%86%99FOC%E7%AE%97%E6%B3%95/%E5%BA%8F%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E5%87%BA%E8%BF%99%E7%B3%BB%E5%88%97%E8%AF%BE%E7%A8%8B.md)
5. 
### 基本概念
###### 反电动势
- 电机转速越高，反电动势越大。反电动势越大，那么电机电流也就越小
###### 级数和极对数
1. 级数---N极,S级的总数
2. 极对数---一个N和一个S为一个磁极对
###### 机械角度和电角度
1. 机械角度---恒为360°，即空间几何角度
2. 电角度---磁场每转过一对磁极为360°，电角度=极对数\*360\°
###### RPM(转/分钟)
- 电机转速一般表示方式
###### KV值
- 在1V工作电压下，无刷电机每分钟的空载转速
- 电机转速(空载) = KV\*电压

## SPWM、SVPWM
1. SPWM：SIN Pulse Width Modulation
2. SVPWM：Space Vector Pulse Width Modulation
3. 相电压最大幅值：2/3 * U-dc ≈ 1.15Udc
4. 线电压最大幅值：2/sqrt3 *  U-dc ≈ 0.866 * Udc
5. 