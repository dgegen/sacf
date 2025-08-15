cmake_minimum_required(VERSION 3.8)
project(sacf)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_REQUIRED_FLAGS ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(PYBIND11_CPP_STANDARD -std=c++14)

# Find pybind11 package
find_package(pybind11 REQUIRED)

include_directories(${CMAKE_SOURCE_DIR}/include)

file(GLOB DATASTRUCTURE ${CMAKE_SOURCE_DIR}/datastructure/*.cpp)
file(GLOB CORRELATOR ${CMAKE_SOURCE_DIR}/correlator/*.cpp)

message(STATUS "source directory ${CMAKE_SOURCE_DIR} yeet")

if(CMAKE_COMPILER_IS_GNUCC AND CMAKE_CXX_COMPILER_VERSION VERSION_LESS 4.7)
    message(FATAL_ERROR "Require at least gcc-4.7, version used:" ${CMAKE_CXX_COMPILER})
endif()

# Use the found pybind11 package to add modules
pybind11_add_module(datastructure ${DATASTRUCTURE})
pybind11_add_module(correlator ${CORRELATOR})

set_target_properties(datastructure PROPERTIES LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR})
set_target_properties(correlator PROPERTIES LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR})
