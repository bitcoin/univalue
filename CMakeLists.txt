cmake_minimum_required(VERSION 3.5)

set(CMAKE_CXX_STANDARD 11)

set(libunivalue_major_version 1)
set(libunivalue_minor_version 0)
set(libunivalue_micro_version 3)
set(libunivalue_interface_age 1)
# If you need a modifier for the version number.
# Normally empty, but can be used to make "fixup" releases.
set(libunivalue_extraversion)

# libtool versioning from libunivalue
math(EXPR libunivalue_binary_age "100 * ${libunivalue_minor_version} + ${libunivalue_micro_version}")
math(EXPR libunivalue_current "${libunivalue_binary_age} - ${libunivalue_interface_age}")
set(libunivalue_age ${libunivalue_current})
set(libunivalue_revision ${libunivalue_interface_age})
set(libunivalue_version "${libunivalue_major_version}.${libunivalue_minor_version}.${libunivalue_micro_version}${libunivalue_extraversion}")

project(libunivalue
    VERSION "${libunivalue_major_version}.${libunivalue_minor_version}.${libunivalue_micro_version}"
    LANGUAGES CXX)

set(LIBUNIVALUE_MAJOR_VERSION libunivalue_major_version)
set(LIBUNIVALUE_MINOR_VERSION libunivalue_minor_version)
set(LIBUNIVALUE_MICRO_VERSION libunivalue_micro_version)
set(LIBUNIVALUE_INTERFACE_AGE libunivalue_interface_age)

# ABI version
# http://www.gnu.org/software/libtool/manual/html_node/Updating-version-info.html
set(LIBUNIVALUE_CURRENT libunivalue_current)
set(LIBUNIVALUE_REVISION libunivalue_revision)
set(LIBUNIVALUE_AGE libunivalue_age)

if ((MINGW OR WIN32 OR MSYS OR CYGWIN) AND BUILD_SHARED_LIBS)
    message(FATAL_ERROR "Not supported if host is Windows/MinGW")
endif()

include_directories(include)

# Use -DBUILD_SHARED_LIBS=ON to generate SHARED library

add_subdirectory(lib)

set_target_properties(univalue PROPERTIES VERSION ${libunivalue_version})
set_target_properties(univalue PROPERTIES PUBLIC_HEADER include/univalue.h)
set_target_properties(univalue PROPERTIES OUTPUT_NAME univalue)
