cmake_minimum_required(VERSION 3.20)
project(itch-book LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug)
endif()

add_executable(itch-book src/main.cpp)

target_compile_options(itch-book PRIVATE
    -Wall -Wextra -Wpedantic -Wconversion -Wshadow
    $<$<CONFIG:Debug>:-g -O0 -fsanitize=address,undefined -fno-omit-frame-pointer>
    $<$<CONFIG:Release>:-O3 -march=native>
)

target_link_options(itch-book PRIVATE
    $<$<CONFIG:Debug>:-fsanitize=address,undefined>
)