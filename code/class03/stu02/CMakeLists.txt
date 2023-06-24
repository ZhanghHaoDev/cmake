cmake_minimum_required(VERSION 3.25)
project(stu02)

set(CMAKE_CXX_STANDARD 11)

# 注释的使用方法
# 单行注释
#[[
    cmake中的多行注释
    cmake中的多行注释
    cmake中的多行注释
    cmake中的多行注释
]]

# 变量的使用方法
# 变量使用set()创建 第一个参数为name，第二个值为value
set(NAME "stu02")
message(STATUS ${NAME})

# list列表
set(AGE 12;13;14;15)
message(STATUS ${AGE})

# 环境变量
set(ENV{ENV_VAR} "$ENV{PATH}")
message(STATUS "Value of ENV_VAR: $ENV{ENV_VAR}")

# 条件分支
set(EMPTY_STR "")
if (NOT EMPTY_STR AND FLAG AND NUM LESS 50 AND NOT NOT_DEFINE_VAR)
    message("The first if branch...")
elseif (EMPTY_STR)
    message("EMPTY_STR is not empty")
else ()
    message("All other case")
endif()

# 列表操作
set(SLOGAN_ARR To be)   # Saved as "To;be"
set(SLOGAN_ARR To;be)
set(SLOGAN_ARR "To;be")
set(WECHAT_ID_ARR Real Cool Eengineer)
list(APPEND SLOGAN_ARR a)                # APPEND sub command
list(APPEND SLOGAN_ARR ${WECHAT_ID_ARR}) # Can append another list
list(LENGTH SLOGAN_ARR SLOGAN_ARR_LEN)   # LENGTH sub command
# Convert list "To;be;a;Real;Cool;Engineer"
# To string "To be a Real Cool Engineer"
list(JOIN SLOGAN_ARR " " SLOGEN_STR)
message("Slogen list length: ${SLOGAN_ARR_LEN}")
message("Slogen list: ${SLOGAN_ARR}")
message("Slogen list to string: ${SLOGEN_STR}\n")


add_executable(stu02 main.cpp)
