cmake_minimum_required(VERSION 3.10)
project(bitsybox LANGUAGES C)

set(APP_NAME bitsybox)

# Set source files
file(GLOB_RECURSE SRC_FILES src/bitsybox/*.c)

# Define the application executable
add_executable(${APP_NAME} ${SRC_FILES})

# Set SDL2 flags
find_package(SDL2 REQUIRED)
target_include_directories(${APP_NAME} PRIVATE ${SDL2_INCLUDE_DIRS})

# Link SDL2 libraries
target_link_libraries(${APP_NAME} ${SDL2_LIBRARIES} m)

# Disable windows terminal output
if(MSYS)
set_target_properties(${APP_NAME} PROPERTIES
    LINK_FLAGS "-Wl,-subsystem,windows"
)
endif()
