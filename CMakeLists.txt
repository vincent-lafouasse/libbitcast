cmake_minimum_required(VERSION 3.16)

project(bitcast VERSION 1.0.0)

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")

option(BITCAST_BUILD_TESTS "Build and run tests using CTest" ON)

add_library(${PROJECT_NAME})
target_sources(${PROJECT_NAME} PRIVATE src/bitcast.c)

target_include_directories(${PROJECT_NAME} PUBLIC ./include)

target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -pedantic
                                               -fdiagnostics-color=always)

if(BITCAST_BUILD_TESTS)
  set(CMAKE_CXX_STANDARD 20)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)

  include(FetchContent)
  include(cmake/fetch_gtest.cmake)

  include(CTest)
  enable_testing()

  add_subdirectory(test)
endif()
