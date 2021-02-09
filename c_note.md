# gcc编译

## gcc编译4步骤

预处理: gcc -E、展开宏，头文件，替换条件编译，删除注释、空白、空行

编译: gcc -S、检查语法规范（此阶段消耗时间和系统资源最多）

汇编: gcc -c、将汇编指令翻译成机器指令

链接: 无参数、数据段合并、地址回填

## gcc常用参数

-I 	（大写i）指定头文件目录

-c		只做预处理,编译,和汇编。得到二进制文件

-g		编译时添加调试语句，使之支持gdb调试

-Wall	显示所有警告

-D		向程序中“动态”注册宏定义。（例如：gcc hello.c -D HELLO 10）

# 静态库和共享库（动态库）

静态库：对空间要求较低，对时间要求较高

共享库：和静态库相反

## 静态库制作及使用

1. 将.c 文件生成.o文件

```
gcc -c xxxx.c -o xxxx.o
```

2. 使用ar rsc命令生成静态库.a文件，其中xxx是可以自己命名的部分

```
ar rsc libxxx.a file1.o
```

gcc编译生成可执行程序时报错主要出现在两个地方：1.编译，2.链接。编译阶段报错会有行号，链接阶段报错没有行号，存在collect2。

使用静态库，编译静态库到可执行文件中，注意顺序，源码在前，库在后

```
gcc test.c libxxx.a -o test
```

另外，静态库应该配合头文件使用，头文件结构可以如下

```
#ifndef _HEAD_H_
#define _HEAD_H_
int func1(int, char);
char func2(int);
...
#endif
```

## 动态库制作

1. 将.c 文件生成.o文件，生成与位置无关的代码（-fPIC）

```
gcc -c xxxx.c -o xxxx.o -fPIC
```

2. 使用gcc -shared命令制作动态库，其中xxx是可以自己命名的部分

```
gcc -shared -o libxxx.so file.o
```

3. 编译可执行程序时，指定所用的动态库。-l：指定库名，-L：指定库的路径

```
gcc test.c -o a.out -l mylib -L
```

至此，直接执行./a.out会出错，原因：

动态链接器：	工作于程序运行阶段，工作时需要提供动态库所在目录位置（通过环境变量中的LD_LIBRARY_PATH提供）

```
export LD_LIBRARY_PATH=./lib
```

链接器：			工作与链接阶段，工作时需要 -l和 -L
