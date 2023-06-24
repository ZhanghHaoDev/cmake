add_library(tools OBJECT
        tool.h
        tool.cpp
)

target_include_directories(tools PUBLIC .)