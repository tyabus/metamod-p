project(METAMOD CXX)

cmake_minimum_required(VERSION 3.0.0)

message("Compiling metamod-p for ${CMAKE_SYSTEM_NAME} ${CMAKE_SYSTEM_PROCESSOR}")

#disable 'lib' prefix
set(CMAKE_SHARED_LIBRARY_PREFIX "")

if("${CMAKE_BUILD_TYPE}" STREQUAL "Release")
	message("Release build type is set. Setting special defines for it")
	add_definitions(-D__INTERNALS_USE_REGPARAMS__ -DOPT_TYPE="optimized")
elseif("${CMAKE_BUILD_TYPE}" STREQUAL "FastRelease")
	message("FastRelease build type is set. Setting special defines for it")
	add_definitions(-D__INTERNALS_USE_REGPARAMS__ -D__BUILD_FAST_METAMOD__ -DOPT_TYPE="optimized+meta_debug-disabled")
else()
	add_definitions(-DOPT_TYPE="debugging")
endif()

add_subdirectory(metamod)
add_subdirectory(stub_plugin)
add_subdirectory(trace_plugin)
