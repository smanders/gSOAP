cmake_minimum_required(VERSION 2.8.5)
project(gsoap)
include(flags OPTIONAL)
set(lib_name gsoap)
#######################################
# library sources
set(${lib_name}_libsrcs
  gsoap/stdsoap2.cpp
  gsoap/stdsoap2.h
  )
source_group("" FILES ${${lib_name}_libsrcs})
#######################################
# library
add_library(${lib_name} STATIC ${${lib_name}_libsrcs})
#######################################
# install
install(TARGETS ${lib_name} DESTINATION lib${NUMBITS})
install(FILES gsoap/stdsoap2.h DESTINATION include/gsoap)
