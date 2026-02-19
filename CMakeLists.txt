# 根据不同平台生成不同的makefile配置文件

cmake_minimum_required(VERSION 3.28)        # 指定使用cmake的最低版本
project(CXX_text C CXX)                     # 设置项目名称与可用语言列表，默认支持全部语言
set(CMAKE_CXX_STANDARD 23)                  # 指定使用的C++标准版本，默认为C++98版本
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/output)           # 指定可执行文件的创建位置
set(program "C++ program" "C++ knowledge")  # 设置变量，默认为string类型，使用${变量}来取得变量值
set(p "C++ program")
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_MODULES_STD 0)
set(CMAKE_CXX_MODULES_EXT 0)

if(CMAKE_CXX_COMPILER_ID MATCHES "GNU")
    add_compile_options(-std=c++23)
    # 明确禁用模块相关选项
    remove_compile_options(-fmodules-ts)
    remove_compile_options(-fmodule-mapper=*)
    remove_compile_options(-fdeps-format=p1689r5)
endif()

# aux_source_directory("C++ knowledge/" test1)     # 将目录下的所有文件赋值给变量
#file(GLOB_RECURSE test2 "C++ program/*.cpp")     # 递归将目录与子目录下的所有指定类型文件赋值给变量
#
#include_directories("C++ function")                  # 指定头文件的所在目录(用于头文件与源文件目录不同时)
# 编译完后生成的二进制代码需要头文件来使系统调用时知晓该文件中有哪些函数

# add_library(library_name STATIC/SHARED "C++ program/test.cpp")  # 制作库文件(static静态库与shared动态库)
# set(LIBRARY_OUTPUT_PATH "../")                   # 指定库文件的创建位置


# target_libraries(CXX_test PRIVATE/PUBLIC/INTERFACE lib1) # 指定目标文件使用的静态库文件(PRIVATE：库仅供目标内部使用；PUBLIC：目标和其使用者都需要此库；INTERFACE：仅目标的使用者需要此库)
# link_directories("/C++ function")              # 指定静态库路径
# 生成可执行文件时，静态库文件会被打包到可执行文件中，执行时被加载到内存；动态库不打包到可执行文件中，执行到相应部分时才会被加载到内存

add_executable(CXX_test                 # 设置编译后的可执行文件(executable)名与对应的源文件(多个文件用空格隔开)
#        C++ program/test.cpp
#        C++ function/fast_swap.h
        ${p}/test2.cpp
)


