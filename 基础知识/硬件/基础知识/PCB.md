1. [PCB板layout的12个细节，千万要注意！_元器件 (sohu.com)](https://www.sohu.com/a/375798947_100281310)
2. [PCB布局布线规则_pcb布线规则-CSDN博客](https://blog.csdn.net/chenhuanqiangnihao/article/details/113936533?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522171997488916800188569105%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=171997488916800188569105&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-113936533-null-null.142^v100^pc_search_result_base5&utm_term=pcb%E5%B8%83%E5%B1%80&spm=1018.2226.3001.4187)
### 细节
#### 贴片之间的间距（推荐）
- 贴片之间器件距离要求：
	同种器件：≥0.3mm
	异种器件：≥0.13\*h+0.3mm（h为周围近邻元件最大高度差）
	只能手工贴片的元件之间距离要求：≥1.5mm.
![[Pasted image 20240703110234.jpg]]
#### 直插器件与贴片的距离
![[Pasted image 20240703110301.jpg]]
- 直插式电阻器件与贴片之间应保持足够的距离，建议在1-3mm之间
#### 对于IC的去耦电容的摆放
![[Pasted image 20240703110343.png]]
- 每个IC的电源端口附近都需要摆放去耦电容，且位置尽可能靠近IC的电源口，当一个芯片有多个电源口的时候，每个口都要布置去耦电容。
#### 元件焊盘两边引线宽度要一致
![[Pasted image 20240703110914.png]]