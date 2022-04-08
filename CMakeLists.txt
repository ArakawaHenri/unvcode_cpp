cmake_minimum_required(VERSION 3.20)
project(unvcode_cpp)

set(ENV{https_proxy} "127.0.0.1:7890")
include(FetchContent)
FetchContent_Declare(
        stb
        GIT_REPOSITORY "https://github.com/nothings/stb.git"
        GIT_TAG "af1a5bc352164740c1cc1354942b1c6b72eacb8a"
        SOURCE_DIR "../ext/stb"
)

FetchContent_MakeAvailable(stb)
set(CMAKE_CXX_STANDARD 23)

add_executable(unvcode_cpp main.cpp)
TARGET_LINK_LIBRARIES(unvcode_cpp)
add_custom_command(TARGET unvcode_cpp POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_if_different
        "${PROJECT_SOURCE_DIR}/NotoSerifSC-SemiBold.ttf"
        $<TARGET_FILE_DIR:unvcode_cpp>)
