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

# build options
option(IMGUI_BUILD_STATIC "Build ImGUI statically" ON)

include_directories(ImGui Private
	${CMAKE_CURRENT_SOURCE_DIR}
	${LIBRARY_PATH}/sdl/include
)

set(IMGUI_SOURCE_FILES
	"imgui.cpp"
	"imgui_demo.cpp"
	"imgui_draw.cpp"
	"imgui_tables.cpp"
	"imgui_widgets.cpp"
	"backends/imgui_impl_sdl3.cpp"
	"backends/imgui_impl_sdlrenderer3.cpp"
	"misc/cpp/imgui_stdlib.cpp"
)

# compile library
if (IMGUI_BUILD_STATIC)
	add_library(ImGui STATIC "${IMGUI_SOURCE_FILES}")
else ()
	add_library(ImGui SHARED "${IMGUI_SOURCE_FILES}")
endif ()

target_link_libraries (ImGui 
PRIVATE 
	SDL3::SDL3-static
)

target_precompile_headers(ImGui
PRIVATE
    <array>
    <string>
    <string_view>
    <vector>
    <unordered_set>
    <unordered_map>
	<set>
	<map>
	<initializer_list>
	<filesystem>
	<fstream>
	<iostream>
	<typeindex>
	<type_traits>
	<algorithm>
	<chrono>
	<cmath>
	<cstdio>
	<cstdint>
	<cstdlib>
	<functional>
	<stddef.h>
	<stdexcept>
	<stdint.h>
	<type_traits>
	<utility>
	<wchar.h>
	<memory>
    <limits>
)
