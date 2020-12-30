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

if(NOT EXISTS ${CMAKE_SOURCE_DIR}/media/superbible7-media.zip)
  set(URL  "http://openglsuperbible.com/files/superbible7-media.zip")
  set(HASH "bdf3f67aff21054bd69f39e9908603beeffaaecf877d6738d00804ab0af5976c7fc1c2e723600e589638e708abe726ae41786c7be1db3adc43ba24d8db428df2")
  file(
    DOWNLOAD
    ${URL}
    ${CMAKE_SOURCE_DIR}/media/superbible7-media.zip
    SHOW_PROGRESS
    EXPECTED_HASH SHA512=${HASH}
  )
endif()

if(NOT EXISTS ${CMAKE_BINARY_DIR}/media/shaders)
  file(
    ARCHIVE_EXTRACT
    INPUT ${CMAKE_SOURCE_DIR}/media/superbible7-media.zip
    DESTINATION ${CMAKE_BINARY_DIR}/media/
  )
endif()

