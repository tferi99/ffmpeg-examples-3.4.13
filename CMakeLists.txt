﻿# CMakeList.txt : CMake project for ffmpeg-examples, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)
project ("ffmpeg-examples")

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

set(LIBRARIES_FOR_LINK
    PkgConfig::LIBAV
    m
)

find_package(PkgConfig REQUIRED)
pkg_check_modules(LIBAV REQUIRED IMPORTED_TARGET 
    libavdevice
    libavfilter
    libavformat
    libavcodec
    libswresample
    libswscale
    libavutil
)

# Add the FFmpeg include directories
include_directories(${FFMPEG_INCLUDE_DIRS})

# Add source to this project's executable.
add_executable (decode_audio "decode_audio.c")
add_executable (decode_audio_smart "decode_audio_smart.c")
add_executable (encode_audio "encode_audio.c")


# NOTE: 'm' means linking with the math library (libm)
target_link_libraries(decode_audio PRIVATE ${LIBRARIES_FOR_LINK})
target_link_libraries(decode_audio_smart PRIVATE ${LIBRARIES_FOR_LINK})
target_link_libraries(encode_audio PRIVATE ${LIBRARIES_FOR_LINK})


