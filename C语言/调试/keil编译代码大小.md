1. RO data是 （Read Only ）只读常量的大小，如const
2. RW data是（Read Write） 初始化了的可读写变量的大小。
3. ZI data是（Zero Initialize） 没有初始化的可读写变量的大小，ZI-data不会被算做代码里因为不会被初始化。
4. FLASH中的被占用的空间为：Code+RO Data+RW Data
5. 芯片内部RAM使用的空间为： RW Data + ZI Data