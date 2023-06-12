cmake_minimum_required (VERSION 3.10.2)

cmake_policy(SET CMP0048 NEW)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Choose the type of build, options are: Debug, Release, or MinSizeRel." FORCE)
    message(STATUS "CMAKE_BUILD_TYPE not set, defaulting to Release.")
endif()

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

if(NOT BUILD_NUMBER)
    set(BUILD_NUMBER 1.0.0)
endif()

project (rpi-vulkan-driver
	VERSION ${BUILD_NUMBER}
	DESCRIPTION "Driver for Broadcom Videocore IV GPU"
	LANGUAGES C CXX
)

include(options)
include(sysroot)
include(global)
#include(vulkan)

add_subdirectory(brcm)
add_subdirectory(QPUassembler)
add_subdirectory(driver)

include(packaging)

include(CTest)

if(BUILD_TESTING)
    add_subdirectory(test)
endif()

add_custom_target(uninstall 
    "${CMAKE_COMMAND}" -P "${CMAKE_SOURCE_DIR}/cmake/uninstall.cmake"
)
