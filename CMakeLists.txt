cmake_minimum_required(VERSION 3.22)

#Configuration du projet

project(mlx_gl)

if (CMAKE_BUILD_TYPE STREQUAL "")
	# CMake defaults to leaving CMAKE_BUILD_TYPE empty. This screws up
	# differentiation between debug and release builds.
	set(CMAKE_BUILD_TYPE "Debug" CACHE STRING "Choose the type of build, options are: None (CMAKE_CXX_FLAGS or CMAKE_C_FLAGS used) Debug Release." FORCE)
endif ()

#set(CMAKE_DEBUG_POSTFIX "_d")
#set(CMAKE_INSTALL_PREFIX "${CMAKE_CURRENT_BINARY_DIR}/dist")

set(CMAKE_LIBRARY_OUTPUT_DIRECTORY lib/${CMAKE_BUILD_TYPE})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY bin/${CMAKE_BUILD_TYPE})

link_directories(${CMAKE_SOURCE_DIR}/lib)
link_directories(${CMAKE_SOURCE_DIR}/../sojotz/build/lib/Debug/)
link_directories(${CMAKE_SOURCE_DIR}/../sojotz/build/cmake.linuxtools.linux.x86_64/lib/Debug/)
link_directories(${CMAKE_SOURCE_DIR}/../sojotz/build/default/lib/Debug/)
link_directories(${CMAKE_SOURCE_DIR}/../sojotz/build/cmake.debug.linux.x86_64/lib/Debug/)

#SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -std=c++17") #c++11

INCLUDE(FindPkgConfig)

#PKG_SEARCH_MODULE(SDL2 REQUIRED sdl2)
#PKG_SEARCH_MODULE(SDL2NET REQUIRED SDL2_net>=2.0.0)

include_directories(
	./
	../minilibx-linux/
	#${SDL2_INCLUDE_DIRS}
	)

file(
        GLOB_RECURSE
        mlxgl_files
        src/*
	)

add_executable(
        mlx_gl
        ${mlxgl_files}
	)

target_link_libraries(
        mlx_gl
        ${CMAKE_SOURCE_DIR}/../minilibx-linux/libmlx_Linux.a
        ${CMAKE_SOURCE_DIR}/../minilibx-linux/libmlx.a
        Xext X11 m
        #sojotz
        #${SDL2_LIBRARIES}
        #${SDL2NET_LIBRARIES}
	)

