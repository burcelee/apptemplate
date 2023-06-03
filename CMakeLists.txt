cmake_minimum_required(VERSION 3.26.4)

project (apptemplate)

add_executable (${CMAKE_PROJECT_NAME} ${CMAKE_CURRENT_SOURCE_DIR} src/main.cpp)
target_compile_features(${CMAKE_PROJECT_NAME} PUBLIC cxx_std_17)

set (CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})
set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})

add_subdirectory(external)
