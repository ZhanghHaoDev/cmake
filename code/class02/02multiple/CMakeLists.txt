cmake_minimum_required(VERSION 3.25)
project(02multiple)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)

add_executable(02multiple main.cpp tool/tool.h tool/tool.cpp)