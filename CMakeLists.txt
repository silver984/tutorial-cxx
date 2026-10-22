cmake_minimum_required(VERSION 3.31.6)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_SCAN_FOR_MODULES OFF)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

project(
  my_cxx_proj
  VERSION 1.0.0
  LANGUAGES C CXX
)

add_executable(my_app)

set_target_properties(
  my_app PROPERTIES
  OUTPUT_NAME "My App"
)

file(GLOB SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/src/*.c*)
target_sources(my_app PRIVATE ${SOURCES})
target_include_directories(my_app PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)

include(${CMAKE_CURRENT_SOURCE_DIR}/cmake/CPM.cmake)

CPMAddPackage(
  NAME fmt
  GITHUB_REPOSITORY fmtlib/fmt
  GIT_TAG 12.1.0
  GIT_SHALLOW TRUE
)

target_link_libraries(my_app PRIVATE fmt::fmt)