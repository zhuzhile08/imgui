############################################################
# ==========================================
# IMPORTANT!
# ==========================================
# This file is NOT part of the origninal ImGui project at:
# https://github.com/ocornut/imgui
# 
# Please refer to the official GitHub repository for any
# questions on the original Library
# 
# This file is ONLY responsible for the compilation of 
# ImGui for the use case of this particular project
############################################################

cmake_minimum_required(VERSION 3.22.0)
project(ImGui VERSION 1.8.8)

# set default to debug
set(CMAKE_BUILD_TYPE DEBUG)
set(CMAKE_CXX_STANDARD 20)

# find path to libraries
find_package(Vulkan REQUIRED)

include_directories(ImGui Private
	${CMAKE_CURRENT_SOURCE_DIR}
	${LIBRARY_PATH}/sdl2/include
	Vulkan::Headers
)

# compile libraries
add_library(ImGui STATIC
	"imgui.cpp"
	"imgui_demo.cpp"
	"imgui_draw.cpp"
	"imgui_tables.cpp"
	"imgui_widgets.cpp"
	"backends/imgui_impl_vulkan.cpp"
	"backends/imgui_impl_sdl2.cpp"
	"backends/imgui_impl_sdlrenderer2.cpp"
)

target_link_libraries(ImGui 
PRIVATE 
	Vulkan::Vulkan
	SDL2
)

target_precompile_headers(ImGui
PRIVATE
	<vector>
	<iostream>
	<fstream>
	<deque>
	<string>
	<map>
	<unordered_map>
	<array>
	<functional>
	<cmath>
	<algorithm>
	<limits.h>
	<utility>
	<stdint.h>
	<ctype.h>
	<stdio.h>
	<stdlib.h>
	<stddef.h>
	<stdint.h>
	<math.h>
)
