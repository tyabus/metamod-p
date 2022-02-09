project(METAMOD_DLL CXX)

include_directories( . ../metamod ../hlsdk/ ../hlsdk/common/ ../hlsdk/dlls/ ../hlsdk/engine/ ../hlsdk/pm_shared/ )

file(GLOB METAMOD_SRC api_hook.cpp
	api_info.cpp
	commands_meta.cpp
	conf_meta.cpp
	dllapi.cpp
	engine_api.cpp
	engineinfo.cpp
	game_autodetect.cpp
	h_export.cpp
	linkplug.cpp
	log_meta.cpp
	meta_eiface.cpp
	metamod.cpp
	mlist.cpp
	mplayer.cpp
	mplugin.cpp
	mreg.cpp
	mutil.cpp
	osdep.cpp
	osdep_p.cpp
	reg_support.cpp
	sdk_util.cpp
	support_meta.cpp
	vdate.cpp
	game_support.cpp
)
file(GLOB METAMOD_SRC_LINUX osdep_detect_gamedll_linux.cpp osdep_linkent_linux.cpp)
file(GLOB METAMOD_SRC_WIN32 osdep_detect_gamedll_win32.cpp osdep_linkent_win32.cpp)

if(WIN32)
	list(APPEND METAMOD_SRC "${METAMOD_SRC_WIN32}")
else()
	list(APPEND METAMOD_SRC "${METAMOD_SRC_LINUX}")
endif()

if(NOT MSVC)
	add_compile_options(-Wall -Wno-unknown-pragmas -Wno-attributes -Wno-write-strings -std=gnu++98 -Wno-c++11-compat -fno-permissive)
endif()

if(WIN32 AND ${CMAKE_COMPILER_IS_GNUCXX})
	file(GLOB LINK_SCRIPT i386pe.merge)
	add_link_options(-Xlinker --script -Xlinker ${LINK_SCRIPT})
endif()

if(CYGWIN)
	add_compile_options(-mno-cygwin)
endif()

set(METAMOD_LIB_NAME "metamod_${CMAKE_SYSTEM_PROCESSOR}")
message("${METAMOD_LIB_NAME}")
add_library(${METAMOD_LIB_NAME} SHARED ${METAMOD_SRC})

add_definitions(-D__METAMOD_BUILD__)

if(XASH3D)
	add_definitions(-DXASH_DLSYM_META)
endif()
