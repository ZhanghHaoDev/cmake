# 第二章 gcc编译器

## 2.1 gcc介绍

1. gcc编译器支持编译c++，c语言等多种语言等边缘
2. Linux开发c/c++一定要学会gcc
3. 使用gcc指令编译c代码
4. 使用g++指令编译c++代码

## 2.2 编译过程

1. 预处理-Pre-Processing    // .i 文件
``` bash{.line-numbers}
# -E 选项指示编译器仅对输入文件进行预处理
g++ -E test.cpp -o test.i
```

2. 编译-Compiling       // .s文件

```bash{.line-numbers}
# -S 编译选项告诉g++在为c++代码产生汇编语言文件后停止编译
# g++产生的汇编语言文件在缺省扩展名是 .s
g++ -S test.i -o test.s
```

3. 汇编-Assembling  //.o文件
```bash{.line-numbers}
# -c 选项告诉g++仅把源代码编译为机器的目标代码
# 缺省时g++建立的目标代码文件有一个.o的扩展名称
g++ -c test.cpp -o test.o
```

4. 链接-Linking     //bin文件
```bash{.line-numbers}
# -o 编译选项来为将产生的可执行文件用指定的文件名
g++ test.o -o test
```

## 2.3 G++ 重要参数

1. -g     编译带调试信息的可执行文件
``` bash{.line-numbers}
# -g 选项告诉 GCC 产生能被 GNU 调试器GDB使用的调试信息，以调试程序。
# 产生带调试信息的可执行文件test
g++ -g test.cpp
```

2. -O[n]    优化源代码
``` bash{.line-numbers}
# 所谓优化，例如省略掉代码中从未使用过的变量、直接将常量表达式用结果值代替等等，这些操作会缩减目标文件所包含的代码量，提高最终生成的可执行文件的运行效率。
# -O 选项告诉 g++ 对源代码进行基本优化。这些优化在大多数情况下都会使程序执行的更快。 -O2 选项告诉 g++ 产生尽可能小和尽可能快的代码。 如-O2，-O3，-On（n 常为0–3）
# -O 同时减小代码的长度和执行时间，其效果等价于-O1
# -O0 表示不做优化
# -O1 为默认优化
# -O2 除了完成-O1的优化之外，还进行一些额外的调整工作，如指令调整等。
# -O3 则包括循环展开和其他一些与处理特性相关的优化工作。
# 选项将使编译的速度比使用 -O 时慢， 但通常产生的代码执行速度会更快。
# 使用 -O2优化源代码，并输出可执行文件

g++ -O2 test.cpp
```

3. -l  和  -L     指定库文件  |  指定库文件路径
``` bash{.line-numbers}
# -l参数(小写)就是用来指定程序要链接的库，-l参数紧接着就是库名
# 在/lib和/usr/lib和/usr/local/lib里的库直接用-l参数就能链接
# 链接glog库
 
g++ -lglog test.cpp

# 如果库文件没放在上面三个目录里，需要使用-L参数(大写)指定库文件所在目录
# -L参数跟着的是库文件所在的目录名
# 链接mytest库，libmytest.so在/home/bing/mytestlibfolder目录下

g++ -L/home/bing/mytestlibfolder -lmytest test.cpp
```

4. -I    指定头文件搜索目录
``` bash{.line-numbers}
# -I 
# /usr/include目录一般是不用指定的，gcc知道去那里找，
# 但是如果头文件不在/usr/icnclude里我们就要用-I参数指定了，
# 比如头文件放在/myinclude目录里，那编译命令行就要加上-I/myinclude 参数了，
# 如果不加你会得到一个”xxxx.h: No such file or directory”的错误。-I参数可以用相对路径，
# 比如头文件在当前 目录，可以用-I.来指定。上面我们提到的–cflags参数就是用来生成-I参数的。

g++ -I/myinclude test.cpp
```

5. -Wall    打印警告信息
```bash{.line-numbers}
# 打印出gcc提供的警告信息
g++ -Wall test.cpp

-w    关闭警告信息
# 关闭所有警告信息
g++ -w test.cpp
```

6. -std=c++11    设置编译标准

```bash {.line-numbers}
# 使用 c++11 标准编译 test.cpp
g++ -std=c++11 test.cpp
```

7. -o     指定输出文件名
```bash {.line-numbers}
# 指定即将产生的文件名
# 指定输出可执行文件名为test
g++ test.cpp -o test
```

8. -D     定义宏
```bash {.line-numbers}
# 在使用gcc/g++编译的时候定义宏
# 常用场景：
# -DDEBUG 定义DEBUG宏，
# 可能文件中有DEBUG宏部分的相关信息，用个DDEBUG来选择开启或关闭DEBUG
示例代码：

// -Dname 定义宏name,默认定义内容为字符串“1”
#include <stdio.h>

int main()
{
    #ifdef DEBUG
        printf("DEBUG LOG\n");
    #endif
        printf("in\n");
}
```

// 1. 在编译的时候，使用gcc -DDEBUG main.cpp
// 2. 第七行代码可以被执行
注：使用 man gcc命令可以查看gcc英文使用手册

## 2.4 g++ 命令行编译