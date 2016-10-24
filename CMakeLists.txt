cmake_minimum_required (VERSION 3.0)
cmake_policy(VERSION 3.0)

project (Bundler C CXX)


list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")

if(CMAKE_CL_64)  
    set(PLATFORM "x64")      
else(CMAKE_CL_64)  
    set(PLATFORM "WIN32")
endif(CMAKE_CL_64)

# set output directories
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin/${PLATFORM})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib/${PLATFORM})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib/${PLATFORM})
# Set postfixes for generated libraries based on buildtype.
set(CMAKE_RELEASE_POSTFIX "")
set(CMAKE_DEBUG_POSTFIX "")

# The version number.
set(STOCKER_VERSION_MAJOR 1)
set(STOCKER_VERSION_MINOR 0)
set(STOCKER_VERSION_PATCH 0)
set(STOCKER_VERSION
  ${STOCKER_VERSION_MAJOR}.${STOCKER_VERSION_MINOR}.${STOCKER_VERSION_PATCH})

# set path
set(BUNDLER_SRC_PATH ${CMAKE_SOURCE_DIR}/src)
set(BUNDLER_LIB_PATH ${CMAKE_SOURCE_DIR}/lib)
set(BUNDLER_INCLUDE_PATH ${CMAKE_SOURCE_DIR}/include)

# set MD to MT
set(CompilerFlags
    CMAKE_CXX_FLAGS
    CMAKE_CXX_FLAGS_DEBUG
    CMAKE_CXX_FLAGS_RELEASE
    CMAKE_C_FLAGS
    CMAKE_C_FLAGS_DEBUG
    CMAKE_C_FLAGS_RELEASE
  )
foreach(CompilerFlags ${CompilerFlags})
  string(REPLACE "/MD" "/MT" ${CompilerFlags} "${${CompilerFlags}}")
endforeach()

# use unicode
ADD_DEFINITIONS(-DUNICODE)
ADD_DEFINITIONS(-D_UNICODE)

option(5point "5point" on)
option(ann_1.1_char "ann" on)
option(cblas "cblas" on)
option(clapack "clapack" on)
option(cminpack "cminpack" on)
option(f2c "f2c" on)
option(getopt "getopt" on)
option(imagelib "imagelib" on)
option(jpeg "jpeg" on)
option(matrix "matrix" on)
option(minpack "minpack" off)
option(sba-1.5 "sba" on)
option(sfm-driver "sfm-driver" on)
option(zlib "zlib" off)
option(BUNDLERAPP "Bundler" on)
option(BUNDLE2PMVS "Bundle2PMVS" on)
option(RADIALUNDISTORT "RadialUndistort" on)
option(KEYMATCHFULL "KeyMatchFull" on)
option(BUNDLE2VIS "Bundle2Vis" on)

# only build debug and release
set(CMAKE_CONFIGURATION_TYPES Debug Release CACHE TYPE INTERNAL FORCE)

# include the UpdateCacheVariable
include(UpdateCacheVariable)

# configure a file
configure_file(${CMAKE_SOURCE_DIR}/cmake/config.h.in
  ${CMAKE_BINARY_DIR}/cmake/config.h)

include_directories(BEFORE ${CMAKE_BINARY_DIR}/cmake)

add_subdirectory(src)
add_subdirectory(lib)