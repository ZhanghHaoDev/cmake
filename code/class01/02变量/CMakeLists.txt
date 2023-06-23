# 在cmake构建过程中定义一个变量，并输出

cmake_minimum_required(VERSION 3.25)
project(02)

set(CMAKE_CXX_STANDARD 17)

# 定义一个hello的变量，赋值200
set(HELLO 200)
# 在构建过程中输出hello的值
message(STATUS ${HELLO})

list(APPEND my_list aa)
list(APPEND my_list bb)
list(APPEND my_list cc ss)
message(STATUS ${my_list})

# 使用foreach循环来输出list的值
foreach (ite IN LISTS my_list)
    message(STATUS ${ite})
endforeach ()

# cmake宏
macro(MyMacro myVar)
    set(myVar "new value")
    message("argument: ${myVar}")
endmacro()
set(myVar "first value")
message("myVar is now: ${myVar}")
MyMacro("called value")
message("myVar is now: ${myVar}")

# cmake函数
function(MyFunction FirstArg)
    message("Function: ${CMAKE_CURRENT_FUNCTION}")
    message("File: ${CMAKE_CURRENT_FUNCTION_LIST_FILE}")
    message("FirstArg: ${FirstArg}")
    set(FirstArg "new value")
    message("FirstArg again: ${FirstArg}")
    message("ARGV0: ${ARGV0} ARGV1: ${ARGV1} ARGC: ${ARGC}")
endfunction()
set(FirstArg "first value")
MyFunction("Value1" "Value2")
message("FirstArg in global scope: ${FirstArg}")

add_executable(02 main.cpp)
