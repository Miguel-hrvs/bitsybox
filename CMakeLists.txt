cmake_minimum_required(VERSION 3.10)
project(bitsybox)

set(APP_NAME bitsybox)

# Set source files
file(GLOB_RECURSE SRC_FILES src/bitsybox/*.c src/bitsybox/duktape/*.c)

# Set SDL2 flags
find_package(SDL2 REQUIRED)
include_directories(${SDL2_INCLUDE_DIRS})

# Detect platform
if(MINGW)
    set(PLATFORM WIN)
    set(APP_EXTENSION .exe)
    set(RELEASE_FLAGS ${SDL2_LIB} ${SDL2_INCLUDE_DIRS} -mconsole)
elseif(WIN32)
    set(PLATFORM WIN)
    set(APP_EXTENSION .exe)
    set(SDL2_LIB SDL2.dll)
    set(RELEASE_FLAGS ${SDL2_LIB} ${SDL2_INCLUDE_DIRS} -mconsole)
elseif(APPLE)
    set(PLATFORM MAC)
    set(SDL2_LIB SDL2.framework)
    set(RELEASE_FLAGS ${SDL2_LIB} ${SDL2_INCLUDE_DIRS})
    set(BUILD_RELEASE_BINARY_SUBDIR ${APP_NAME}.app/Contents/MacOS)
    set(BUILD_RELEASE_GAMES_SUBDIR ${APP_NAME}.app/Contents/Resources/games)
elseif(UNIX AND CMAKE_SYSTEM_PROCESSOR MATCHES "x86_64")
    set(PLATFORM LIN)
    set(SDL2_PATH /usr/lib/x86_64-linux-gnu/)
    set(SDL2_LIB libSDL2-2.0.so)
    set(RELEASE_FLAGS ${SDL2_LIB} ${SDL2_INCLUDE_DIRS} -lm)
    set(RELEASE_FLAGS_DYNAMIC ${SDL2_LIB} ${SDL2_INCLUDE_DIRS} -lm)
    set(BUILD_RELEASE_GAMES_SUBDIR games)
elseif(UNIX AND CMAKE_SYSTEM_PROCESSOR MATCHES "arm")
    set(PLATFORM RPI)
    set(SDL2_PATH /lib/arm-linux-gnueabihf/)
    set(SDL2_LIB libSDL2-2.0.so)
    set(RELEASE_FLAGS ${SDL2_LIB} ${SDL2_INCLUDE_DIRS} -lm)
    set(RELEASE_FLAGS_DYNAMIC ${SDL2_LIB} ${SDL2_INCLUDE_DIRS} -lm)
    set(BUILD_RELEASE_GAMES_SUBDIR games)
endif()

# Define the application executable
add_executable(${APP_NAME} ${SRC_FILES})

# Add compiler definitions
target_compile_definitions(${APP_NAME} PRIVATE PLATFORM_${PLATFORM})

# Link SDL2 libraries
target_link_libraries(${APP_NAME} ${SDL2_LIBRARIES} m)