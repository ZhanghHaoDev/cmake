# 第一章 cmake介绍

## 1.1 cmake介绍
CMake是一个跨平台的安装（编译）工具，可以用简单的语句来描述所有平台的安装(编译过程)。
他能够输出各种各样的makefile或者project文件，CMake 的组态档取名为 CMakeLists.txt。
也就是在CMakeLists.txt这个文件中写cmake代码。 
一句话：cmake就是将多个cpp、hpp文件组合构建为一个大工程的语言。

## 1.2 cmake安装

cmake支持多个平台，包括Windows，macOS，Linux

1. Windows 安装

官网
```
https://cmake.org
```

2. macOS安装

通过brew 安装
```
brew install cmake
```

3. Linux安装

通过yum/apt-get安装
```
yum install cmake

apt-get install cmake
```

4. 查看软件是否安装成功
在终端输入 version 来查看版本，检查cmake是否安装成功
```
cmake -version  
```

## 1.3 安装GCC，GDB

gcc：编译器
gdb：调试器

1. Windows

2. macOS

通过brew安装
```
// 安装 gcc
brew install gcc
// 安装gdb
brew install gdb
```

3. linux

通过yum或apt安装

``` bash
// yum 安装
yum install gcc
yum install gdb

// apt安装
apt-get install gcc
apt-get install gdb
```

4. 查看是否安装成功

在终端输入 -v来查看软件版本，检查是否安装成功
```bash
gcc -v 
gdb -v 
```