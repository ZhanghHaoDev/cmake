cmake_minimum_required(VERSION 3.25)
project(01_target)

set(CMAKE_CXX_STANDARD 11)

add_executable(01_target main.cpp code/tool.cpp)

add_subdirectory(code)
target_link_libraries(01_target PRIVATE tool)