# 第四章 cmake开发

## 4.1 cmake 语法特性介绍

1. 基本语法

    __指令（参数1，参数2。。。）__

    + 参数使用括弧括起来
    + 参数之间使用空格或分号分开

2. 指令大小写无关，参数和变量是大小写相关的

3. 变量使用${}方式取值，但是在IF控制语句中是直接使用变量名的

## 4.2 重要指令和cmake常用变量

中括号代表可选项

1. 指定cmake最小版本要求
    语法：cmake_minimum_required(VERSION 版本号[FATAL_ERROR])
    要求写在文件的最开头
    ```cmake {.line-numbers}
    # cmake 最小版本要求为2.8.2
    cmake_minimum_required(VERSION 2.8.2)
    ```

2. 定义工程名称，指定工程支持的语言
    语法：project(工程名称 [语言])
    ``` cmake {.line-numbers}
    # 指定工程名称为HELLO
    project(HELLO)
    ```

3. 显式的定义变量
    语法：set(VAR [变量1] [变量2]。。)
    ``` cmake {.line-numbers}
    # 定义SRC变量，其值为hello.c
    set(SRC hello.c)
    ```

4. 头文件指定搜索路径
    语法：include_directories(路径)
    ```cmake {.line-numbers}
    # 将 ./include 添加到头文件搜索路径
    include_directories(./include)
    ```

5. 生成库文件
    语法：add_library(libname [SHARED|STATIC] source1,source2...)
    SHARED:动态库，STATIC:静态库
    ```cmake{.line-numbers}
    # 通过变量SRC生成libhello.so 动态库
    add_library(hello SHARED ${src})
    ```

6. 添加编译参数
    语法：add_compile_options(...)
    ``` cmake{.line-numbers}
    # 提交编译参数 -wall -std=c++11
    add_compile(-wall -std=c++11 -o2)
    ```

7. 生成可执行文件
    语法：add_executable(exename soure1,sou2...)
    ```cmake{.line-numbers}
    # 编译main.cpp 生成main可执行文件
    add_executable(main main.cpp)
    ```

8. 添加需要链接的共享库
    语法：target_link_libraries(target libary1...)
    ```cmake {.line-numbers}
    # 将hello动态库链接到可执行文件main
    target_link_libraries(main hello)
    ```

9. 向当前工程添加存放源文件的子目录，并可以指定中间二进制和目标二进制存放的位置
    语法：add_subdirectory(siourd_dir)
    ```cmake {.line-numbers}
    # 添加src子目录，src子目录中需要有一个CMakeList.txt
    add_subdirectory(src)
    ```

10. 发现一个目录下的所有源代码文件并将列表存储在一个变量中，这个指令临时被用来自动构建源文件
    语法：aux_source_directory(dir VARIABLE)
    ``` cmake {.line-numbers}
    # 定义SRC变量，其中值为当前目录下所有的源文件
    aux_source_directory(. SRC)
    # 编译SRC变量所代表的源代码文件，生成main可执行文件
    add_executable(main ${SRC})
    ``` 

## 4.3 CMake常用变量

CMAKE_C_FLAGS   gcc编译选项

CMAKE_CXX_FLAGS  g++编译选项

``` cmake {.line-numbers}
# 在CMAKE_CXX_FLAGS编译选项后追加-std=c++11
set( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
```

CMAKE_BUILD_TYPE  编译类型(Debug, Release)

``` cmake {.line-numbers}
# 设定编译类型为debug，调试时需要选择debug
set(CMAKE_BUILD_TYPE Debug) 
# 设定编译类型为release，发布时需要选择release
set(CMAKE_BUILD_TYPE Release) 
```

CMAKE_BINARY_DIR

PROJECT_BINARY_DIR

\<projectname>__BINARY_DIR

这三个变量指代的内容是一致的。
+ 如果是 in source build，指的就是工程顶层目录。
+ 如果是 out-of-source 编译,指的是工程编译发生的目录。
+ PROJECT_BINARY_DIR 跟其他指令稍有区别，不过现在，你可以理解为他们是一致的。

CMAKE_SOURCE_DIR

PROJECT_SOURCE_DIR
\<projectname>__SOURCE_DIR

这三个变量指代的内容是一致的,不论采用何种编译方式,都是工程顶层目录。
也就是在 in source build时,他跟 CMAKE_BINARY_DIR 等变量一致。

+ PROJECT_SOURCE_DIR 跟其他指令稍有区别,现在,你可以理解为他们是一致的。
+ CMAKE_C_COMPILER：指定C编译器
+ CMAKE_CXX_COMPILER：指定C++编译器
+ EXECUTABLE_OUTPUT_PATH：可执行文件输出的存放路径
+ LIBRARY_OUTPUT_PATH：库文件输出的存放路径

## 4.4 CMake编译工程

CMake目录结构：项目主目录存在一个CMakeLists.txt文件

两种方式设置编译规则：

1. 包含源文件的子文件夹包含CMakeLists.txt文件，主目录的CMakeLists.txt通过add_subdirectory添加子目录即可；

2. 包含源文件的子文件夹未包含CMakeLists.txt文件，子目录编译规则体现在主目录的CMakeLists.txt中；


### 4.4.1 编译流程

在 linux 平台下使用 CMake 构建C/C++工程的流程如下:

手动编写 CmakeLists.txt。
执行命令 cmake PATH生成 Makefile ( PATH 是顶层CMakeLists.txt 所在的目录 )。
执行命令make 进行编译。

``` cmake {.line-numbers}
# important tips
..      # 表示当前目录
/       # 表示当前目录

..      # 表示上级目录
../     # 表示上级目录
```

### 4.4.2 两种构建方式

1. __内部构建(in-source build)：不推荐使用__

内部构建会在同级目录下产生一大堆中间文件，这些中间文件并不是我们最终所需要的，和工程源文件放在一起会显得杂乱无章。

``` cmake {.line-numbers}
## 内部构建

# 在当前目录下，编译本目录的CMakeLists.txt，生成Makefile和其他文件
cmake .
# 执行make命令，生成target
make
```

2. __外部构建(out-of-source build)：==推荐使用==__

将编译输出文件与源文件放到不同目录中

``` cmake {.line-numbers}
## 外部构建

# 1. 在当前目录下，创建build文件夹
mkdir build 
# 2. 进入到build文件夹
cd build
# 3. 编译上级目录的CMakeLists.txt，生成Makefile和其他文件
cmake ..
# 4. 执行make命令，生成target
make
```
