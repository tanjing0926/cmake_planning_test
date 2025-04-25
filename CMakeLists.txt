cmake_minimum_required(VERSION 3.29.0)
project(planning)
set(CMAKE_CXX_STANDARD 17)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin) #动态库和exe都指定到bin目录下面
#CMAKE_LIBRARY_OUTPUT_DIRECTORY   linux下面指定动态库
#CMAKE_ARCHIVE_OUTPUT_DIRECTORY   linux下面指定静态库

aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LISTS)
#生产动态库
add_library(common SHARED ${SRC_LISTS})

#包含动态库所依赖的头文件目录
target_include_directories(common
PUBLIC
    ${PROJECT_SOURCE_DIR}/include
)


#可执行文件
add_executable(planning_main planning_main.cpp)

target_include_directories(planning_main
PUBLIC
${PROJECT_SOURCE_DIR}/include)

#链接动态库
target_link_libraries(planning_main
PUBLIC
common
)