cmake_minimum_required(VERSION 3.21)
project(opengl_demo)

set(CMAKE_CXX_STANDARD 14)

# inspect env variable
if (NOT DEFINED ENV{GLAD_HOME})
    message(FATAL_ERROR "found no env named GLAD_HOME")
endif()

# GLAD
set(GLAD_HOME $ENV{GLAD_HOME})

# Libigl
#option(LIBIGL_GLFW "Build target igl::glfw" ON)
#include(libigl)

include_directories(
        "${GLAD_HOME}/include"
        "${CMAKE_CURRENT_SOURCE_DIR}/lib/eigen"
        "${CMAKE_CURRENT_SOURCE_DIR}/libigl/include"
)

# Add src to the include directories
include_directories("${CMAKE_CURRENT_SOURCE_DIR}/src")
# create executable
file(GLOB SRCFILES src/main.cpp)
add_executable(opengl_demo "${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp" "lib/glad.c")

# compile glfw
find_package(glfw3 3.3 REQUIRED)
target_link_libraries(opengl_demo glfw)
find_package(OpenGL REQUIRED)
target_link_libraries(opengl_demo OpenGL::GL)