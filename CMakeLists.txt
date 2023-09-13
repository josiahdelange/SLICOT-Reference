# CMake build script for SLICOT based on Seth Morton's template
# for Fortran projects.  See license file in cmake/ directory.
cmake_minimum_required(VERSION 3.10)
project(SLICOT Fortran)

# Set the SLICOT version
set(VERSION 5.8.1)

# Add our local modules to the module path
set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake/Modules/")

# Configure user-specified compiler flags for DEBUG, RELEASE, or TESTING.
# Should review this file manually to ensure flags are set appropriately.
#include(${CMAKE_MODULE_PATH}/SetFortranFlags.cmake)

# Find/configure LAPACK (note: also finds/configures BLAS)
include(${CMAKE_MODULE_PATH}/SetUpLAPACK.cmake)

# There is an error in CMAKE with this flag for pgf90.  Unset it
get_filename_component(FCNAME ${CMAKE_Fortran_COMPILER} NAME)
if(FCNAME STREQUAL "pgf90")
    unset(CMAKE_SHARED_LIBRARY_LINK_Fortran_FLAGS)
endif(FCNAME STREQUAL "pgf90")

# Build main SLICOT and auxillary lpkaux libraries.  Note: CMake automatically
# provides an option flag BUILD_SHARED_LIBS (default value: OFF) to determine
# whether to build shared object libraries (.dll on Windows, .so on Linux) or
# static libraries (.lib on Windows, .a on Linux).  By using shared libraries,
# the size on disk of compiled applications smaller.  However, this introduces
# runtime linker dependencies - for example, Linux systems must install the
# libraries to a standard location (e.g. /usr/lib/) and/or set an environment
# variable like LD_LIBRARY_PATH so that application code may find them when run.
add_subdirectory(src) # builds main SLICOT library
add_subdirectory(src_aux) # builds auxillary subroutines

# Build test cases
#TODO
