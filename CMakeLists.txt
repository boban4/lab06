cmake_minimum_required(VERSION 3.10)

project(lab6)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(PRINT_VERSION_MAJOR 0)
set(PRINT_VERSION_MINOR 1)
set(PRINT_VERSION_PATCH 1)
set(PRINT_VERSION_TWEAK 0)
set(PRINT_VERSION ${PRINT_VERSION_MAJOR}.${PRINT_VERSION_MINOR}.${PRINT_VERSION_PATCH}.${PRINT_VERSION_TWEAK})
message(STATUS "Project version: ${PRINT_VERSION}")

option(BUILD_TESTS "Build tests" OFF)

add_subdirectory(banking)

if(BUILD_TESTS)
  enable_testing()

  add_subdirectory(googletest/gtest)

  file(GLOB LAB6_TEST_SOURCES tests/*.cpp)

  add_executable(check ${LAB6_TEST_SOURCES})
  target_link_libraries(check banking gmock_main)

  add_test(NAME check COMMAND check)
endif()

include(CPackConfig.cmake)
