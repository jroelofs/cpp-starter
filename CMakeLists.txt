cmake_minimum_required(VERSION 3.5)

project(calc)

set(FUZZER OFF CACHE BOOL "Fuzzer")

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")

include_directories(${PROJECT_SOURCE_DIR}/include)

add_subdirectory(lib)
add_subdirectory(tools)

if(FUZZER)
  add_subdirectory(fuzzer)
endif()

enable_testing()
add_subdirectory(unittests)
add_test(NAME unittests COMMAND ${CMAKE_BINARY_DIR}/bin/unittests)
add_custom_target(check COMMAND ${CMAKE_CTEST_COMMAND} DEPENDS unittests)
