project(STUBPLUGIN CXX)

include_directories( . ../metamod ../hlsdk/ ../hlsdk/common/ ../hlsdk/dlls/ ../hlsdk/engine/ ../hlsdk/pm_shared/ )

file(GLOB PLUGIN_SRC dllapi.cpp
	engine_api.cpp
	h_export.cpp
	meta_api.cpp
	sdk_util.cpp
)

if(NOT WIN32)
	add_compile_options(-Wall -Wno-unknown-pragmas -Wno-attributes -Wno-write-strings -std=gnu++98 -Wno-c++11-compat -fno-permissive)
endif()

set(PLUGIN_LIB_NAME "stubplugin_${CMAKE_SYSTEM_PROCESSOR}")
message("${PLUGIN_LIB_NAME}")
add_library(${PLUGIN_LIB_NAME} SHARED ${PLUGIN_SRC})
