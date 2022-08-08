# Common constants
set(PROJECT_NAME cppboilerplate)
set(PROJECT_LIB_NAME cppboilerplatelibname)
set(PROJECT_MAIN_TARGET cppboilerplateexec)
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_FLAGS "-g -Wall")

project(${PROJECT_NAME})

# Gather include and source files in variables.
include_directories(${PROJECT_NAME} ${CMAKE_SOURCE_DIR}/include)
file(GLOB SRC_FILES ${CMAKE_SOURCE_DIR}/src/*.cpp)


# Define library such that main target and tests can link against it.
add_library(${PROJECT_LIB_NAME} ${SRC_FILES})


# Add main target and link against the library.
add_executable(${PROJECT_MAIN_TARGET} main.cpp)
target_link_libraries(${PROJECT_MAIN_TARGET} ${PROJECT_LIB_NAME})


# From the command line one can specify "cmake -DBUILD_TESTS=ON"
# to build testsuite.
option(BUILD_TESTS "Build all tests." OFF)
if (BUILD_TESTS)
    add_subdirectory(ext/googletest)
    enable_testing()
    message(STATUS "GOOGLE-TEST found at: ${gtest_SOURCE_DIR}")
    include_directories(${gtest_SOURCE_DIR}/include ${gtest_SOURCE_DIR})
    file(GLOB TEST_SRC_FILES ${CMAKE_SOURCE_DIR}/test/*.cpp)

    add_executable(runUnitTests ${TEST_SRC_FILES})
    target_link_libraries(runUnitTests gtest gtest_main)
    target_link_libraries(runUnitTests ${PROJECT_LIB_NAME})

    add_test(UnitTests runUnitTests)
endif()