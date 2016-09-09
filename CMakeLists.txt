cmake_minimum_required (VERSION 3.5)
project (HelloCMake)

set (EXECUTABLE_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/build)
set (LIBRARY_OUTPUT_PATH ${EXECUTABLE_OUTPUT_PATH})

add_subdirectory (libgreeter)
include_directories (libgreeter)

set (PROJECT_SOURCE_DIR ${CMAKE_SOURCE_DIR}/src)
file (GLOB HELLO_SOURCE ${PROJECT_SOURCE_DIR}/*.c)
add_executable (hello ${HELLO_SOURCE})
target_link_libraries (hello greeter)

