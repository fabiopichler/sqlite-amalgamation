cmake_minimum_required(VERSION 3.5)

project(sqlite3 LANGUAGES C)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

set(SRC_FILES
    include/sqlite3.h
    src/sqlite3.c
)

add_library(sqlite3 STATIC ${SRC_FILES})

target_include_directories(sqlite3 PRIVATE include)

if(UNIX)
    set_property(TARGET sqlite3 PROPERTY POSITION_INDEPENDENT_CODE TRUE)
endif()
