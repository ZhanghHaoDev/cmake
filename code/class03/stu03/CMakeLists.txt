cmake_minimum_required(VERSION 3.25)
project(stu03)

# 指定版本
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_C_STANDARD 99)

# 配置编译器
add_compile_options(-Wall -Wextra -pedantic -Werror)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -pipe -std=c99")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pipe -std=c++11")

# 配置编译类型
set(CMAKE_BUILD_TYPE Debug)

# 开启优化
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -g -O0")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -g -O0")

# release优化
#set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -O2")
#set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O2")

# 设置头文件目录
include_directories(src/include)

# 编译静态库
# file(GLOB_RECURSE MATH_LIB_SRC src/c/math/*.c)
# add_library(math STATIC ${MATH_LIB_SRC})


add_executable(stu03 main.cpp )
