cmake_minimum_required(VERSION 2.8.10)
project(libjansson_builder C CXX)
include(ExternalProject)

set(JANSSON_INSTALL_LIB_DIR "lib/${BITS}")

#
# get jansson
#
ExternalProject_Add(
        project_jansson
        INSTALL_DIR ${COMMON_LOCAL}
#        GIT_REPOSITORY https://github.com/akheron/jansson.git
        URL http://www.digip.org/jansson/releases/jansson-2.7.tar.gz
        SOURCE_DIR ${COMMON_SRCS}/jansson
        CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${COMMON_LOCAL} -DJANSSON_INSTALL_LIB_DIR:String=${CONFIGURE_LIBDIR}
)
ExternalProject_Get_Property(project_jansson install_dir)
add_library(jansson STATIC IMPORTED GLOBAL)
set_property(TARGET jansson PROPERTY IMPORTED_LOCATION ${CONFIGURE_LIBDIR}/libjansson${CMAKE_STATIC_LIBRARY_SUFFIX})
add_dependencies(jansson project_jansson)
