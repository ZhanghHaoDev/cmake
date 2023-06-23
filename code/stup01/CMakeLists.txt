#todo 1: 指定cmake的最低版本 3.10
#todo 2: 指定项目的名称
#todo 3: 指定cmake的c++源文件以及构建名称

cmake_minimum_required(VERSION 3.25)
project(stup01)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

include_directories(code/include)

add_executable(stup01 code/src/main.cpp)
