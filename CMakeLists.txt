cmake_minimum_required(VERSION 3.10)
project(bitsybox LANGUAGES C)

set(APP_NAME bitsybox)

# Set source files
file(GLOB_RECURSE SRC_FILES src/bitsybox/*.c src/bitsybox/duktape/*.c)

# Set SDL2 flags
find_file(SDL2_INCLUDE_DIR NAME SDL.h HINTS SDL2)
find_package(SDL2)
find_library(SDL2_LIBRARY NAME SDL2)

# Define the application executable
add_executable(${APP_NAME} ${SRC_FILES})

# Link SDL2 libraries
target_link_libraries(${APP_NAME} ${SDL2_LIBRARY} m)

include(cmake/FindSDL2.cmake)
