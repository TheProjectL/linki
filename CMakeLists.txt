# Linki Cmake file
cmake_minimum_required(VERSION 3.10)
project(linki)

# C language
set(CMAKE_C_STANDARD 11)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_C_FLAGS "-Wall -Wextra -pedantic")
set(CMAKE_C_FLAGS_DEBUG "-D DEBUG -O0")
set(CMAKE_C_FLAGS_RELEASE "-O3")

add_library(linki SHARED)
target_include_directories(linki PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/cross/include/" "${CMAKE_CURRENT_SOURCE_DIR}/native/${CMAKE_SYSTEM_NAME}/include/")


file(GLOB_RECURSE LINKI_SRC "native/${CMAKE_SYSTEM_NAME}/src/*.c")
target_sources(linki PRIVATE ${LINKI_SRC})
if (WIN32)
    target_link_libraries(linki PRIVATE -static -lws2_32)
endif()