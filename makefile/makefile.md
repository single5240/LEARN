- [Makefile（详细教程）_makefile教程-CSDN博客](https://blog.csdn.net/weixin_45604295/article/details/134283631?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_utm_term~default-0-134283631-blog-123187908.235^v43^pc_blog_bottom_relevance_base8&spm=1001.2101.3001.4242.1&utm_relevant_index=3)
### 基本语法
~~~makefile
目标:依赖  
TAB 命令
~~~
### make
`make [-f file] [options] [target]`
- Make 默认在当前目录中寻找文件名为 GUNmakefile，Makefile，makefile 的文件作为 make 的输入文件。
1. -f 可以指定除上述文件名之外的文件作为输入文件；
2. -v 显示版本号；
3. -n 只输出命令，但并不执行，一般用来测试；
4. -s 只执行命令，但不显示具体命令，此处可在命令中用@符抑制命令输出；
5. -w 显示执行前执行后的路径
6. -C dir 指定 makefile 所在的目录
- 没有指定目标时，默认使用第一个目标。如果指定，则执行对应的命令。
### 注释
`# 注释`



