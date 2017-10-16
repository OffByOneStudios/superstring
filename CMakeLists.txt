cmake_minimum_required(VERSION 3.7)
Project(Superstring CXX)

set(iconv "")

if (WIN32)
	SET(iconv  ${CMAKE_SOURCE_DIR}/vendor/win-iconv/win_iconv.c)
endif()


include_directories(
  ${CMAKE_SOURCE_DIR}/vendor/pcre/include
  ${CMAKE_SOURCE_DIR}/vendor/libcxx
  ${CMAKE_SOURCE_DIR}/vendor/win-iconv
)

file(GLOB_RECURSE includes
  src/core/*.h
  src/core/*.hpp
)

file(GLOB_RECURSE sources
  src/core/*.cc
)

add_library(Superstring STATIC
  ${sources}
  ${includes}
  ${iconv}
)

set_target_properties(Superstring PROPERTIES LINKER_LANGUAGE CXX)