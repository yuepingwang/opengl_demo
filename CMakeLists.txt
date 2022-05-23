cmake_minimum_required(VERSION 3.21)
project(opengl_demo)

set(CMAKE_CXX_STANDARD 14)

#add_executable(opengl_demo main.cpp)

# inspect env variable
#if (NOT DEFINED ENV{GLFW_HOME})
#    message(FATAL_ERROR "found no env named GLFW_HOME")
#endif()
if (NOT DEFINED ENV{GLAD_HOME})
    message(FATAL_ERROR "found no env named GLAD_HOME")
endif()

# cache env variable
#set(GLFW_HOME $ENV{GLFW_HOME})
set(GLAD_HOME $ENV{GLAD_HOME})

# set header file directory
#include_directories("${GLFW_HOME}/include")
include_directories("${GLAD_HOME}/include")

# add GLFW pre compiler (?)
#add_library(glfw SHARED IMPORTED)
#SET_TARGET_PROPERTIES(glfw PROPERTIES IMPORTED_LOCATION "${CMAKE_CURRENT_SOURCE_DIR}/lib/glfw/3.3.7/include/")

# create executable
add_executable(opengl_demo main.cpp "lib/glad.c")

# compile glfw
find_package(glfw3 3.3 REQUIRED)
target_link_libraries(opengl_demo glfw)
find_package(OpenGL REQUIRED)
target_link_libraries(opengl_demo OpenGL::GL)


#include_directories(
#        "${CMAKE_CURRENT_SOURCE_DIR}/lib/glfw/3.3.7/include/"
#)

# link GLFW GLAD OpenGL
#target_link_libraries(opengl_demo glfw "-framework OpenGL")