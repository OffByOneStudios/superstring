cmake_minimum_required(VERSION 3.7)
Project(PCRE C)

set(iconv "")

include_directories(
  ${CMAKE_SOURCE_DIR}/include
  ${CMAKE_SOURCE_DIR}/10.23/src
)

file(GLOB_RECURSE includes
  ${CMAKE_SOURCE_DIR}/include/*.h
  ${CMAKE_SOURCE_DIR}/10.23/src/*h
)


file(GLOB_RECURSE sources
  ${CMAKE_SOURCE_DIR}/10.23/src/*.c
)

add_library(PCRE STATIC
  ${sources}
  ${includes}
  ${iconv}
)
target_compile_definitions(PCRE PRIVATE PCRE2_CODE_UNIT_WIDTH=16)
set_target_properties(PCRE PROPERTIES LINKER_LANGUAGE C)