# ${CMAKE_SOURCE_DIR}/CMakeLists.txt
cmake_minimum_required (VERSION 3.16)
project(superbible7)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)

set(OpenGL_GL_PREFERENCE "GLVND")
find_package(OpenGL REQUIRED)
find_package(gl3w   REQUIRED)
find_package(GLFW   REQUIRED)

add_subdirectory(library)
add_subdirectory(examples)
