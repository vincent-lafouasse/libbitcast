cmake_minimum_required(VERSION 3.16)

project(bitcast VERSION 1.0.1 LANGUAGES C)

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")

# Tests are on by default only when libbitcast is the top-level project, so
# that consumers using add_subdirectory or FetchContent don't fetch googletest.
# (PROJECT_IS_TOP_LEVEL needs CMake 3.21, this works on 3.16.)
if(CMAKE_SOURCE_DIR STREQUAL PROJECT_SOURCE_DIR)
  set(BITCAST_IS_TOP_LEVEL ON)
else()
  set(BITCAST_IS_TOP_LEVEL OFF)
endif()

option(BITCAST_BUILD_TESTS "Build and run tests using CTest"
       ${BITCAST_IS_TOP_LEVEL})

add_library(${PROJECT_NAME})
target_sources(${PROJECT_NAME} PRIVATE src/bitcast.c)
add_library(bitcast::bitcast ALIAS ${PROJECT_NAME})

target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -pedantic
                                               -fdiagnostics-color=always)

if(BITCAST_BUILD_TESTS)
  enable_language(CXX)
  set(CMAKE_CXX_STANDARD 20)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)

  include(FetchContent)
  include(cmake/fetch_gtest.cmake)

  include(CTest)
  enable_testing()

  add_subdirectory(test)
endif()
