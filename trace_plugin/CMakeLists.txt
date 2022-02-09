cmake_minimum_required(VERSION 3.0.0)

project(TRACEPLUGIN CXX)

include_directories( . ../metamod ../hlsdk/ ../hlsdk/common/ ../hlsdk/dlls/ ../hlsdk/engine/ ../hlsdk/pm_shared/ )

file(GLOB PLUGIN_SRC api_info.cpp
	dllapi.cpp
	dllapi_post.cpp
	engine_api.cpp
	engine_api_post.cpp
	h_export.cpp
	log_plugin.cpp
	meta_api.cpp
	plugin.cpp
	sdk_util.cpp
	trace_api.cpp
	vdate.cpp
)

if(NOT WIN32)
	add_compile_options(-Wall -Wno-unknown-pragmas -Wno-attributes -Wno-write-strings -std=gnu++98 -Wno-c++11-compat -fno-permissive)
endif()

set(PLUGIN_LIB_NAME "traceplugin_${CMAKE_SYSTEM_PROCESSOR}")
message("${PLUGIN_LIB_NAME}")
add_library(${PLUGIN_LIB_NAME} SHARED ${PLUGIN_SRC})
