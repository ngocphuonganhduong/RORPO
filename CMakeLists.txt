project(RORPO)
cmake_minimum_required(VERSION 3.2)

option(BUILD_PYRORPO "Enable pyRORPO" OFF)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

if(UNIX)
	SET(LIB_TYPE SHARED)
else()
	SET(LIB_TYPE STATIC)
endif()

# Build Type
if(NOT CMAKE_BUILD_TYPE)
   SET(CMAKE_BUILD_TYPE Release
       CACHE STRING "Choose the type of build : Debug or Release."
       FORCE)
endif()
message("Build Type: " ${CMAKE_BUILD_TYPE})

include_directories(
            libRORPO/include
            Image/include
            docopt
            pyRORPO)

if (NOT ${CMAKE_BUILD_TYPE} STREQUAL "Release")
	enable_testing()
endif()

add_subdirectory(libRORPO)

if (NOT BUILD_PYRORPO)
	add_subdirectory(docopt)
	add_subdirectory(RORPO_multiscale_Usage)
endif()

if (BUILD_PYRORPO)
	message("BUILD_PYRORPO is ON")
	add_subdirectory(pyRORPO)
endif ()
