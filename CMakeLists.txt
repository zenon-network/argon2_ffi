cmake_minimum_required(VERSION 3.14)

project(argon2_ffi)

enable_language(CXX)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_CXX_STANDARD 17)

if(${CMAKE_SYSTEM_NAME} MATCHES "Windows")
set(CMAKE_CXX_FLAGS "-Wall -static -static-libstdc++")
set(CMAKE_C_FLAGS "-Wall -static -static-libgcc")
else()
set(CMAKE_CXX_FLAGS "-Wall -Wextra -O3")
set(CMAKE_C_FLAGS "-Wall -Wextra -O3")
endif()

set(SOURCE_DIR "src/")

set(LIB_PATH "${CMAKE_CURRENT_SOURCE_DIR}/build")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${LIB_PATH})

set(public_headers "${CMAKE_CURRENT_SOURCE_DIR}/src/argon2.h")

set(CMAKE_OSX_ARCHITECTURES "arm64;x86_64" CACHE STRING "" FORCE)

add_library(argon2_ffi
    SHARED
    argon2_ffi.c
    src/argon2.c
    src/core.c
    src/encoding.c
    src/genkat.c
    src/ref.c
    src/thread.c
    src/blake2/blake2b.c
)

set_target_properties(argon2_ffi PROPERTIES
    FRAMEWORK TRUE
    FRAMEWORK_VERSION C
    MACOSX_FRAMEWORK_IDENTIFIER network.zenon.argon2
    VERSION 0.0.1
    SOVERSION 1.0.0
    PUBLIC_HEADER "${public_headers}"
)