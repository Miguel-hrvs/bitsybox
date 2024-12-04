cmake_minimum_required(VERSION 3.10)
project(bitsybox LANGUAGES C)

set(APP_NAME bitsybox)

# Set source files
file(GLOB_RECURSE SRC_FILES src/bitsybox/*.c src/bitsybox/duktape/*.c)

# Set SDL2 flags
find_package(SDL2 REQUIRED)
include_directories(${SDL2_INCLUDE_DIRS})

if(MINGW)
set(SDL2_LIB_DIR C:/SDL/lib)
set(SDL2_INCLUDE_DIR C:/SDL/include)
set(SDL2_LIBRARY C:/SDL/bin)
endif

# Define the application executable
add_executable(${APP_NAME} ${SRC_FILES})

# Link SDL2 libraries
target_link_libraries(${APP_NAME} ${SDL2_LIBRARIES} m)
