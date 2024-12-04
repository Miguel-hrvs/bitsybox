cmake_minimum_required(VERSION 3.10)
project(bitsybox LANGUAGES C)

set(APP_NAME bitsybox)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")

# Set source files
file(GLOB_RECURSE SRC_FILES src/bitsybox/*.c)

# Define the application executable
add_executable(${APP_NAME} ${SRC_FILES})

# Set SDL2 flags
find_package(SDL2 REQUIRED)
include_directories(${SDL2_INCLUDE_DIRS})

# Link SDL2 libraries
target_link_libraries(${APP_NAME} ${SDL2_LIBRARIES} m)
