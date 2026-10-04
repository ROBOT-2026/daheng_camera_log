cmake_minimum_required(VERSION 3.16)
project(daheng_camera_log CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(OpenCV REQUIRED)
find_package(Threads REQUIRED)

add_executable(daheng_camera_log
    src/main.cpp
    third_party/rm_log/src/rm_log.cpp)

target_include_directories(daheng_camera_log PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}/include                      # 大恒 SDK 头文件 (include/sdk)
    ${CMAKE_CURRENT_LIST_DIR}/third_party/spdlog           # spdlog 头文件
    ${CMAKE_CURRENT_LIST_DIR}/third_party/rm_log/inlcude   # rm_log 头文件
    ${OpenCV_INCLUDE_DIRS})

# 大恒安装包会把 libgxiapi.so 装进系统路径 /lib, 直接按名字链接
target_link_libraries(daheng_camera_log PRIVATE
    gxiapi
    ${OpenCV_LIBS}
    Threads::Threads)
