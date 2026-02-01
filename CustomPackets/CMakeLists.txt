# CustomPackets static library
FILE(GLOB CustomPackets-sources
    ${CMAKE_CURRENT_SOURCE_DIR}/*.h
    ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp
)

add_library(CustomPackets STATIC ${CustomPackets-sources})
target_include_directories(CustomPackets PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
set_property(TARGET CustomPackets PROPERTY CXX_STANDARD 17)

if(MSVC)
    target_compile_options(CustomPackets PRIVATE /MT$<$<CONFIG:Debug>:d>)
endif()
