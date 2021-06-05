cmake_minimum_required(VERSION 3.20)
project(lua_imgui)

# imgui

set(IMGUI_ROOT imgui)

add_library(imgui STATIC)
set_target_properties(imgui PROPERTIES
    C_STANDARD 11
    C_STANDARD_REQUIRED ON
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED ON
)
target_compile_options(imgui PRIVATE
    "/utf-8"
    "/MP"
)
target_compile_definitions(imgui PUBLIC
    _UNICODE
    UNICODE
    IMGUI_DISABLE_OBSOLETE_FUNCTIONS
    #IMGUI_USE_BGRA_PACKED_COLOR
    IMGUI_USE_WCHAR32
    #IMGUI_ENABLE_FREETYPE
)
target_include_directories(imgui PUBLIC
    ${IMGUI_ROOT}/
    ${IMGUI_ROOT}/misc/cpp
)
target_sources(imgui PRIVATE
    ${IMGUI_ROOT}/imstb_rectpack.h
    ${IMGUI_ROOT}/imstb_textedit.h
    ${IMGUI_ROOT}/imstb_truetype.h
    ${IMGUI_ROOT}/imconfig.h
    ${IMGUI_ROOT}/imgui_demo.cpp
    ${IMGUI_ROOT}/imgui_draw.cpp
    ${IMGUI_ROOT}/imgui_internal.h
    ${IMGUI_ROOT}/imgui_tables.cpp
    ${IMGUI_ROOT}/imgui_widgets.cpp
    ${IMGUI_ROOT}/imgui.cpp
    ${IMGUI_ROOT}/imgui.h
    ${IMGUI_ROOT}/misc/cpp/imgui_stdlib.cpp
    ${IMGUI_ROOT}/misc/cpp/imgui_stdlib.h
)

# lua

add_subdirectory(lua)

# binding

add_library(lua_imgui STATIC)
set_target_properties(lua_imgui PROPERTIES
    C_STANDARD 11
    C_STANDARD_REQUIRED ON
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED ON
)
target_compile_options(lua_imgui PRIVATE
    "/utf-8"
    "/MP"
)
target_include_directories(lua_imgui PUBLIC
    include
)
target_include_directories(lua_imgui PRIVATE
    src
)
target_sources(lua_imgui PRIVATE
    include/lua_imgui.hpp
    include/lua_imgui_type.hpp
    src/lua_imgui_common.hpp
    src/lua_imgui_enum.hpp
    src/lua_imgui_enum.cpp
    src/lua_imgui_hash.cpp
    src/lua_imgui_hash.hpp
    src/lua_imgui_ImGui_ColorX.inl
    src/lua_imgui_ImGui_DragX.inl
    src/lua_imgui_ImGui_InputX.inl
    src/lua_imgui_ImGui_PlotX.inl
    src/lua_imgui_ImGui_register.inl
    src/lua_imgui_ImGui_SliderX.inl
    src/lua_imgui_ImGui.hpp
    src/lua_imgui_ImGui.cpp
    src/lua_imgui_ImGuiTextBuffer.cpp
    src/lua_imgui_type.cpp
    src/lua_imgui.cpp
)
target_link_libraries(lua_imgui PUBLIC
    imgui
    lua
)
