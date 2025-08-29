cmake_minimum_required(VERSION 3.29.0)
project(planning)
set(CMAKE_CXX_STANDARD 17)

#变量和目录设置
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin) # 可执行文件输出目录  #.exe文件和动态库都指定到文件输出目录

#动态库
aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LISTS) # 获取src目录下的所有源文件
add_library(common SHARED ${SRC_LISTS}) # 生成动态库，并链接src目录下的所有源文件
target_include_directories(common PUBLIC ${PROJECT_SOURCE_DIR}/include) # 指定头文件目录

#可执行文件
add_executable(planning_main planning_main.cpp)  # 生成可执行文件

target_include_directories(planning_main PUBLIC ${PROJECT_SOURCE_DIR}/include) # 指定头文件目录
target_link_libraries(planning_main PUBLIC common)  # 链接动态库
