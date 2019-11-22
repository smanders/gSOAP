cmake_minimum_required(VERSION 3.12)
project(gsoap)
include(flags OPTIONAL)
set(lib_name ${PROJECT_NAME})
#######################################
set(${lib_name}_libsrcs
  gsoap/stdsoap2.cpp
  gsoap/stdsoap2.h
  )
source_group("" FILES ${${lib_name}_libsrcs})
#######################################
set(verString "^.*define VERSION \"+([0-9]+)\\.([0-9]+)\\.([0-9]+).*$")
set(verFile gsoap/src/soapcpp2.h)
file(STRINGS ${verFile} VER REGEX "${verString}")
string(REGEX REPLACE "${verString}" "\\1.\\2.\\3" VER ${VER})
if(NOT DEFINED GSOAP_VER)
  set(GSOAP_VER ${VER})
elseif(NOT ${GSOAP_VER} STREQUAL ${VER})
  message(AUTHOR_WARNING "version passed in (${GSOAP_VER}) doesn't match version from ${verFile} (${VER})")
endif()
set(ver _${GSOAP_VER})
set(verDir /${PROJECT_NAME}${ver})
#######################################
add_library(${lib_name} STATIC ${${lib_name}_libsrcs})
target_include_directories(${lib_name} PUBLIC $<INSTALL_INTERFACE:$<INSTALL_PREFIX>/include${verDir}>
  $<INSTALL_INTERFACE:$<INSTALL_PREFIX>/include${verDir}/${PROJECT_NAME}> # for internal header includes
  )
set_target_properties(${lib_name} PROPERTIES OUTPUT_NAME ${lib_name}${ver})
#######################################
set(targetsFile ${PROJECT_NAME}${ver}-targets)
install(TARGETS ${lib_name} EXPORT ${targetsFile}
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  )
install(FILES gsoap/stdsoap2.h DESTINATION include${verDir}/${PROJECT_NAME})
if(DEFINED XP_NAMESPACE)
  set(nameSpace NAMESPACE ${XP_NAMESPACE}::)
endif()
install(EXPORT ${targetsFile} DESTINATION lib/cmake ${nameSpace})
