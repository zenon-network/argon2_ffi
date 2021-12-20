cmake_minimum_required(VERSION 3.4.1)  # for example

# compile options
set(CMAKE_CXX_STANDARD 17)
if(${CMAKE_SYSTEM_NAME} MATCHES "Windows")
    set(CMAKE_CXX_FLAGS "-Wall -static -static-libstdc++")
    set(CMAKE_C_FLAGS "-Wall -static -static-libgcc")
else()
    set(CMAKE_CXX_FLAGS "-Wall -Wextra -O3")
    set(CMAKE_C_FLAGS "-Wall -Wextra -O3")
endif()

# generate in build/
set(LIB_PATH "${CMAKE_CURRENT_SOURCE_DIR}/build")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${LIB_PATH})

add_library(argon2_ffi

        # Sets the library as a shared library.
        SHARED

        # Provides a relative path to your source file(s).
        argon2_ffi.c

        src/argon2.c
        src/core.c
        src/encoding.c
        src/genkat.c
        src/ref.c
        src/thread.c
        src/blake2/blake2b.c
        )
#set_target_properties(argon2_ffi PROPERTIES IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI}/argon2_ffi.so)
