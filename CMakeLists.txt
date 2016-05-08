cmake_minimum_required(VERSION 2.8)

project(gl3w)

find_package(PythonInterp 2.6 REQUIRED)

add_custom_command(
OUTPUT
    ${CMAKE_CURRENT_SOURCE_DIR}/include/GL/glcorearb.h
    ${CMAKE_CURRENT_SOURCE_DIR}/include/GL/gl3w.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/gl3w.c
COMMAND
    ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/gl3w_gen.py
WORKING_DIRECTORY
    ${CMAKE_CURRENT_SOURCE_DIR}
)

include_directories(include)

add_library(gl3w src/gl3w.c)

if (UNIX)
  target_link_libraries(gl3w dl)
endif()
