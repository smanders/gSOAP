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

