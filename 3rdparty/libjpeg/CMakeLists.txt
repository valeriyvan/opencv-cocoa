# ----------------------------------------------------------------------------
#  CMake file for libjpeg. See root CMakeLists.txt
#
# ----------------------------------------------------------------------------
project(libjpeg)

# List of C++ files:

include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}
	"${CMAKE_CURRENT_SOURCE_DIR}/../include"
	)

# The .cpp files:
file(GLOB lib_srcs *.c)
file(GLOB lib_hdrs *.h)
set(lib_ext_hdrs "../include/jconfig.h" "../include/jmorecfg.h" "../include/jpeglib.h")

# ----------------------------------------------------------------------------------
# 				Define the library target:
# ----------------------------------------------------------------------------------

set(the_target "libjpeg")

add_library(${the_target} STATIC ${lib_srcs} ${lib_hdrs} ${lib_ext_hdrs})

if(MSVC)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} /W3")
endif()

if(UNIX AND CMAKE_COMPILER_IS_GNUCXX)
     set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fPIC")
endif()

set_target_properties(${the_target}
	PROPERTIES OUTPUT_NAME "${the_target}"
	DEBUG_POSTFIX "${OPENCV_DEBUG_POSTFIX}"
	ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/3rdparty/lib
	)
