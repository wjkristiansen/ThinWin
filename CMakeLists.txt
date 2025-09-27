# ThinWin - Thin Windows wrapper library
cmake_minimum_required(VERSION 3.24)

# ThinWin appears to be a submodule - create its own CMakeLists
project(ThinWin VERSION 1.0.0)

# Add the main library subdirectory
add_subdirectory(Lib)

# Optionally add the sample if it exists
if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/ThinWinSample/CMakeLists.txt")
    add_subdirectory(ThinWinSample)
endif()

# Installation of include files
install(DIRECTORY Inc/
    DESTINATION include/ThinWin
    FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp"
)