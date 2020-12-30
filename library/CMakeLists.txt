# ${CMAKE_SOURCE_DIR}/library/CMakeLists.txt
add_library(
  sb7
  src/sb7.cpp
  src/sb7color.cpp
  src/sb7ktx.cpp
  src/sb7object.cpp
  src/sb7shader.cpp
  src/sb7textoverlay.cpp
)

target_include_directories(
  sb7
  PUBLIC
  ${CMAKE_CURRENT_LIST_DIR}/include
)

target_link_libraries(
  sb7
  PUBLIC
  gl3w::gl3w
  GLFW::glfw3
)

target_compile_definitions(
  sb7
  PUBLIC
  $<$<PLATFORM_ID:Linux>:LINUX>
  $<$<PLATFORM_ID:Darwin>:LINUX>
  $<$<PLATFORM_ID:Windows>:WINDOWS>
)

