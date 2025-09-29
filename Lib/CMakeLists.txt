# ThinWin Library
cmake_minimum_required(VERSION 3.24)

# Define the library
add_library(ThinWin STATIC
    ThinWin.cpp
    stdafx.cpp
    stdafx.h
    targetver.h
)

# Set target properties
set_target_properties(ThinWin PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED ON
    OUTPUT_NAME "ThinWin"
)

# Include directories
target_include_directories(ThinWin 
    PUBLIC 
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../Inc>
        $<INSTALL_INTERFACE:include/ThinWin>
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}
)

# Preprocessor definitions
target_compile_definitions(ThinWin PRIVATE
    $<$<CONFIG:Debug>:_DEBUG>
    $<$<CONFIG:Release>:NDEBUG>
    NOMINMAX
)

# Windows-specific settings
if(WIN32)
    target_compile_definitions(ThinWin PRIVATE
        WIN32
        _LIB
    )
    
    # Link with Windows libraries
    target_link_libraries(ThinWin PUBLIC
        kernel32
        user32
        gdi32
    )
endif()

# Use precompiled headers
target_precompile_headers(ThinWin PRIVATE stdafx.h)
