project(VtkBasics)
cmake_minimum_required(VERSION 2.6)

find_package(VTK)

IF(NOT VTK_FOUND)
  message(FATAL_ERROR "VTK not found. VTK is not installed or cmake can not find it. Install VTK first and then try again.
If VTK is installed but cmake can not find it, set the VTK_DIR entry to the folder which contains the file VTKConfig.cmake")
ENDIF(NOT VTK_FOUND)


FILE(GLOB _VTK_GEOM_    VtkGeometry/*.cpp)
FILE(GLOB _VTK_IO_      VtkIO/*.cpp)
FILE(GLOB _VTK_SRC_     VtkSource/*.cpp)
FILE(GLOB _VTK_         *.cpp)

include_directories(
	${VTK_INCLUDE_DIRS}
	..
)

if(CMAKE_COMPILER_IS_GNUCXX)
    set(CMAKE_CXX_FLAGS "-Wno-deprecated -mfpmath=sse -msse -msse2 -msse3 -mssse3 -msse4.1 -O3")
endif()

add_library(VtkBasics STATIC
	@_VTK_GEOM_@
	@_VTK_IO_@
	@_VTK_SRC_@
	@_VTK_@
)

