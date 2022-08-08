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