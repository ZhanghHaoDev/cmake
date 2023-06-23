# 使用cmake 构建一个hello cmake项目
# 主要输出 hello cmake即可

cmake_minimum_required(VERSION 3.25)
project(01hellocmake)

set(CMAKE_CXX_STANDARD 17)

add_executable(01hellocmake main.cpp)
