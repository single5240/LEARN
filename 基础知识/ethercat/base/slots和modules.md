
### SLOTS

- 通过对象0 xf030 (配置的模块ident列表) 在基本应用表中定义插槽，图11: 指定插槽。
- 生成的ESI槽元素如图12所示: ESI文件中的槽描述。
![[Pasted image 20250716095007.png]]
![[Pasted image 20250716094324.png]]![[Pasted image 20250716094353.png]]
#### 参数分析
1. a-如果在对象行中将访问设置为 “rw”，则DownloadModuleIdentList为true
2. b-PDO索引增量是根据相关的表头信息设置的 (图10: 模块表的模块Ident字段，第5行)
3. 