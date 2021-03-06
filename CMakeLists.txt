cmake_minimum_required(VERSION 3.0)

project(getodac)

set(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/externals/sanitizers-cmake/cmake" ${CMAKE_MODULE_PATH})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin )
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib/getodac/plugins)

option(ENABLE_TRACE_LOG "Enabe tracing log" OFF)
option(ENABLE_DEBUG_LOG "Enable debugging log" OFF)

find_package(Sanitizers)

if (ENABLE_TRACE_LOG)
    add_definitions(-DENABLE_TRACE_LOG)
endif ()
if (ENABLE_DEBUG_LOG)
    add_definitions(-DENABLE_DEBUG_LOG)
endif ()

add_subdirectory(conf)
add_subdirectory(src)

find_package(GTest)
if (GTEST_FOUND)
    enable_testing()
    add_subdirectory(tests)
endif()
