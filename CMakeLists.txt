#
# This file is part of the Simutrans project under the artistic licence.
# (see licence.txt)
#

cmake_minimum_required(VERSION 3.8)

# Disable in-source builds
if (CMAKE_SOURCE_DIR STREQUAL CMAKE_BINARY_DIR)
	message(FATAL_ERROR "Building Simutrans in-source is not supported. "
		"Please delete ${CMAKE_SOURCE_DIR}/CMakeCache.txt and configure in a different "
		"(preferrably empty) directory.")
endif (CMAKE_SOURCE_DIR STREQUAL CMAKE_BINARY_DIR)

set(CMAKE_WARN_DEPRECATED ON)
list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake/")


find_package(CCache)
if (CCache_FOUND)
	option(SIMUTRANS_ENABLE_CCACHE "Enable CCache build cache" ON)
	if (SIMUTRANS_ENABLE_CCACHE)
		set_property(GLOBAL PROPERTY RULE_LAUNCH_COMPILE "${CCache_EXECUTABLE}")
		set_property(GLOBAL PROPERTY RULE_LAUNCH_LINK    "${CCache_EXECUTABLE}")
	endif (SIMUTRANS_ENABLE_CCACHE)
endif (CCache_FOUND)


project(simutrans VERSION 120.4 LANGUAGES C CXX)

include(simutrans-revision)

include(TestBigEndian)
TEST_BIG_ENDIAN(SIMUTRANS_BIG_ENDIAN)

#
# Dependencies
#
find_package(ZLIB REQUIRED)
find_package(PNG REQUIRED)
find_package(BZip2 REQUIRED)
find_package(Freetype)
find_package(MiniUPNP)

set(CMAKE_THREAD_PREFER_PTHREAD ON)
find_package(Threads)


#
# Configuration options
#
include(simutrans-backend)

if (CMAKE_USE_PTHREADS_INIT)
	option(SIMUTRANS_MULTI_THREAD "Use multiple threads for drawing" ON)
else (CMAKE_USE_PTHREADS_INIT)
	set(SIMUTRANS_MULTI_THREAD OFF)
endif (CMAKE_USE_PTHREADS_INIT)

if (NOT CMAKE_SIZEOF_VOID_P EQUAL 4)
	option(SIMUTRANS_BUILD_32BIT "Build 32 or 64 bit executable" OFF)
endif ()


option(SIMUTRANS_BUILD_MAKEOBJ "Build makeobj pakset tool" OFF)
option(SIMUTRANS_BUILD_NETTOOL "Build command-line tool for server administration" OFF)
option(SIMUTRANS_VALGRIND_SUPPORT  "Add support for valgrind \"memcheck\" tool" OFF)

if (Freetype_FOUND)
	option(SIMUTRANS_USE_FREETYPE "Use freetype library for font rendering" ON)
endif (Freetype_FOUND)

if (MiniUPNP_FOUND)
	option(SIMUTRANS_USE_UPNP "Use MiniUPNP" ON)
endif (MiniUPNP_FOUND)

option(SIMUTRANS_ENABLE_PROFILING "Enable profiling code" OFF)

#
# output directory
#
file(MAKE_DIRECTORY ${CMAKE_BINARY_DIR}/simutrans)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/simutrans)

add_subdirectory(src)

