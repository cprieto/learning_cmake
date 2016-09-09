cmake_minimum_required (VERSION 3.5)
project (HelloCMake)
add_subdirectory (libgreeter)
include_directories (libgreeter)

set (PROJECT_SOURCE_DIR ${CMAKE_SOURCE_DIR}/src)
add_executable (hello ${PROJECT_SOURCE_DIR}/hello.c)
target_link_libraries (hello greeter)
