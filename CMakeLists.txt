
# Author: TheFrenchLeaf https://github.com/TheFrenchLeaf

cmake_minimum_required(VERSION 2.6)

project(CXSparse C)

include_directories(./
./Include)

file(GLOB CXSparse_SRCS "Source/*.c")
set(CXSparse_HEADERS
  Include/SuiteSparse_config.h
  Include/cs.h
  )

set_source_files_properties(${CXSparse_SRCS} PROPERTIES LANGUAGE C)
add_definitions(-DNCOMPLEX)

add_library(cxsparse STATIC ${CXSparse_SRCS})
if(UNIX)
  target_link_libraries(cxsparse m)
  set_target_properties(cxsparse PROPERTIES COMPILE_FLAGS -fPIC)
endiF(UNIX)

option(BUILD_DEMO "Enable Demo." OFF)
if(BUILD_DEMO)
  add_subdirectory(Demo)
endif()

install(TARGETS cxsparse DESTINATION lib)
install(FILES ${CXSparse_HEADERS} DESTINATION include/suitesparse)
