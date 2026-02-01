# WotLK Custom Packets - ClientExtensions DLL
# Based on TSWoW client-extensions (MIT License)
# https://github.com/tswow/tswow

cmake_minimum_required(VERSION 3.22)
Include(FetchContent)

# Force 32-bit build (WoW 3.3.5a is 32-bit)
set(CMAKE_GENERATOR_PLATFORM Win32)
cmake_policy(SET CMP0048 NEW)

project(WotLKCustomPackets VERSION 1.0.0)

# Force Release build if not specified
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release CACHE STRING "Build type" FORCE)
endif()

# Use static runtime linking (/MT instead of /MD) to avoid runtime DLL dependencies
set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")

# Apply to all targets
add_compile_options(
    $<$<CXX_COMPILER_ID:MSVC>:/MT$<$<CONFIG:Debug>:d>>
)

message(STATUS "Build type: ${CMAKE_BUILD_TYPE}")
message(STATUS "Using static runtime linking (no VCRUNTIME/MSVCP DLL dependencies)")

# Lua 5.1 static library
FILE(GLOB lua-sources lua-5.1/src/*.h lua-5.1/src/*.c)
add_library(lua STATIC ${lua-sources})
target_compile_options(lua PRIVATE -w)
if(MSVC)
    target_compile_options(lua PRIVATE /MT$<$<CONFIG:Debug>:d>)
endif()

# CustomPackets library
add_subdirectory(CustomPackets)

# ClientExtensions DLL
add_subdirectory(ClientExtensions)
