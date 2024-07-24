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

### 变量
#### 系统常量（可用make -p 查看）
~~~
AS： 汇编程序的名称，默认为 as；  
CC： C编译期名称，默认为 cc；  
CPP： C预编译期名称，默认为 cc -E；  
CXX： C++编译器名称，默认为 g++；  
RM： 文件删除程序别名，默认为 rm -f；
~~~
#### 自定义变量
定义：变量名=变量值  
使用：$(变量名)， ${变量值}
~~~
OBJ=add.o sub.o multi.o calc.o
TARGET=calc

$(TARGET):$(OBJ)
	gcc $(OBJ) -o $(TARGET)

add.o:add.cpp
	gcc -c add.cpp -o add.o

sub.o:sub.cpp
	gcc -c sub.cpp -o sub.o

multi.o:multi.cpp
	gcc -c multi.cpp -o multi.o

calc.o:calc.cpp
	gcc -c calc.cpp -o calc.o

clean:
	rm -rf *.o calc
~~~
#### 系统变量
~~~
$*：不包括扩展名的目标文件名称；
$+：所以的依赖文件，以空格分隔；
$<：表示规则中的第一个条件；
$?：所有时间戳比目标文件晚的依赖文件，以空格分隔；
$@：目标文件的完整名称；
$^：所有不重复的依赖文件，以空格分隔；
$%：如果目标是归档成员，则该变量表示目标的归档成员名称；
~~~
#### 优化
~~~
OBJ=add.o sub.o multi.o calc.o
TARGET=calc

$(TARGET):$(OBJ)
	$(CXX) $^ -o $@
	
add.o:add.cpp
	$(CXX) -c $^ -o $@

sub.o:sub.cpp
	$(CXX) -c $^ -o $@

multi.o:multi.cpp
	$(CXX) -c $^ -o $@

calc.o:calc.cpp
	$(CXX) -c $^ -o $@

clean:
	$(RM) *.o $(TARGET)
~~~

#### 伪目标

#### 模式匹配
1. `%.o:%.cpp`： .o依赖于对应的.cpp，也就是说`add.o:add.cpp`，都是add，就可以使用`%.o:%.cpp`。**也就是目标和依赖相同部分，可以用%来通配。** `%`就是通配符。
2. `wildcard`：``；
3. `patsubst`：`$ (patsubst %.cpp,%.o,./*.cpp)将当前目录下的对应的cpp文件名替换成.o文件名`；