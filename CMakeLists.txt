cmake_minimum_required(VERSION 3.31)
project(sphere_gen)

set(CMAKE_CXX_STANDARD 17)

include_directories("/Users/kkats/dev/libraries/Include/")

add_executable(sphere-gen main.cpp glad.c)

target_link_libraries(sphere-gen PRIVATE "/Users/kkats/dev/libraries/Libs/libglfw.3.dylib")