cmake_minimum_required(VERSION 3.1)

add_definitions(-std=c++0x)

project(S)

include_directories(solver_lib)
include_directories(formatter_ex_lib)

add_subdirectory(solver_lib)

add_subdirectory(formatter_ex_lib)

add_executable(solver equation.cpp)

target_link_libraries(solver solver_lib)
target_link_libraries(solver formatter_ex)
