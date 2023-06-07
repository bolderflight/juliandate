# v3.14 required for FetchContent_MakeAvailable
cmake_minimum_required(VERSION 3.14)
# Project information
project(JulianDate
  VERSION 1.0.0
  DESCRIPTION "Julian date converter"
  LANGUAGES CXX
)
# Add the library target
add_library(juliandate
  src/juliandate.h
  src/juliandate.cpp
)
# Setup include directories 
target_include_directories(juliandate PUBLIC 
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
  $<INSTALL_INTERFACE:include>
)
# Example and test if this project is built separately
if (PROJECT_NAME STREQUAL CMAKE_PROJECT_NAME)
  # Add the  example target
  add_executable(juliandate_example examples/cmake/juliandate_ex.cc)
  # Add the includes
  target_include_directories(juliandate_example PUBLIC 
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
  )
  # Link libraries to the example target
  target_link_libraries(juliandate_example
    PRIVATE
      juliandate
  )
  # Fetch google test
  include(FetchContent)
  FetchContent_Declare(
    googletest
    GIT_REPOSITORY https://github.com/google/googletest.git
    GIT_TAG release-1.12.1
  )
  FetchContent_MakeAvailable(googletest)
  enable_testing()
  include(GoogleTest)
  # Add the test target
  add_executable(juliandate_test tests/juliandate_test.cc)
  # Add the includes
  target_include_directories(juliandate_test PUBLIC 
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
  )
  # Link libraries to the test target
  target_link_libraries(juliandate_test
    PRIVATE 
      juliandate
      gtest_main 
      gtest
      gmock
  )
  # Discover unit tests
  gtest_discover_tests(juliandate_test)
endif()
