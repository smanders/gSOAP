cmake_minimum_required(VERSION 3.0)
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
install(TARGETS ${lib_name} EXPORT ${PROJECT_NAME}-targets
  RUNTIME DESTINATION bin${NUMBITS}
  LIBRARY DESTINATION lib${NUMBITS}
  ARCHIVE DESTINATION lib${NUMBITS}
  )
install(FILES gsoap/stdsoap2.h DESTINATION include/gsoap)
install(FILES usexp-${PROJECT_NAME}-config.cmake DESTINATION share/cmake)
install(EXPORT ${PROJECT_NAME}-targets DESTINATION lib${NUMBITS}/cmake)
