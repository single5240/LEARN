
### SLOTS

- 通过对象0 xf030 (配置的模块ident列表) 在基本应用表中定义插槽，图11: 指定插槽。
- 生成的ESI槽元素如图12所示: ESI文件中的槽描述。
![[Pasted image 20250716095007.png]]
![[Pasted image 20250716094324.png]]![[Pasted image 20250716094353.png]]
#### 参数分析
1. a-如果在对象行中将访问设置为 “rw”，则DownloadModuleIdentList为true
2. b-PDO索引增量是根据相关的表头信息设置的 (图10: 模块表的模块Ident字段，第5行)
3. c-对象索引增量是根据相关的表头信息设置的 (图10: 模块表的模块Ident字段，第4行)
4. d-插槽名称可以通过描述中的语法 “*\[Slotname: name\]*” 设置，如果未定义名称，则插槽仅根据相关子索引设置
5. e-可分配模块由description列中的语法 “*\[ModuleIds: id\]*” 指定。id应设置为前缀为 “0x” 的十六进制值。多个模块id应以 “;” 分隔，或多次使用语法 (见条目4)。
6. f-默认分配的模块由“Default”列的值设定
7. g-若要将槽位的MinInstances设置为0，则不应设置默认数据，或将[最小值](https://so.csdn.net/so/search?q=%E6%9C%80%E5%B0%8F%E5%80%BC&spm=1001.2101.3001.7020)显式设为0