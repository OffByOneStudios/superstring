cmake_minimum_required(VERSION 3.7)
Project(Superstring CXX)

set(iconv "")

if (WIN32)
	SET(iconv  ${CMAKE_SOURCE_DIR}/vendor/win-iconv/win_iconv.c)
endif()

set(PCRE2_BUILD_PCRE2_8 OFF CACHE BOOL "enable X functionality")
set(PCRE2_BUILD_PCRE2_16 ON CACHE BOOL "enable X functionality")
add_subdirectory(${CMAKE_SOURCE_DIR}/vendor/pcre/10.30/)

include_directories(
  ${PROJECT_BINARY_DIR}/vendor/pcre/10.30
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

target_link_libraries (Superstring pcre2-16)



if(${CMAKE_SYSTEM_NAME} STREQUAL "Linux")
endif()
if(${CMAKE_SYSTEM_NAME} STREQUAL "Darwin")
	target_link_libraries (Superstring iconv)
	list(APPEND CMAKE_CXX_FLAGS "-std=c++1z -stdlib=libc++ -Wc++11-extensions")
endif()
if(${CMAKE_SYSTEM_NAME} STREQUAL "Windows")
endif()


target_compile_definitions(Superstring PRIVATE PCRE2_STATIC=1 PCRE2_CODE_UNIT_WIDTH=16 )
set_target_properties(Superstring PROPERTIES LINKER_LANGUAGE CXX)
