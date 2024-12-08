cmake_minimum_required(VERSION 3.5)

set(SQLITE_VERSION 3.41.0)

project(sqlite3 LANGUAGES C VERSION ${SQLITE_VERSION})

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

if(NOT CMAKE_INSTALL_INCLUDEDIR)
    set(CMAKE_INSTALL_INCLUDEDIR include)
endif()

if(NOT CMAKE_INSTALL_LIBDIR)
    set(CMAKE_INSTALL_LIBDIR lib)
endif()

set(INCLUDE_FILES
    include/sqlite3.h
    include/sqlite3ext.h
)

set(SRC_FILES
    ${INCLUDE_FILES}
    src/sqlite3.c
)

add_library(sqlite3 SHARED ${SRC_FILES})

target_include_directories(sqlite3 PRIVATE include)

if(UNIX)
    set_property(TARGET sqlite3 PROPERTY POSITION_INDEPENDENT_CODE TRUE)
endif()

set(prefix ${CMAKE_INSTALL_PREFIX})
set(includedir "${CMAKE_INSTALL_INCLUDEDIR}")
set(libdir "${CMAKE_INSTALL_LIBDIR}")

set(PACKAGE_VERSION ${SQLITE_VERSION})
set(LIBS_PUBLIC )
set(LIBS_PRIVATE "-lm -pthread")

configure_file(sqlite3.pc.in sqlite3.pc @ONLY)

install(TARGETS sqlite3)
install(
    FILES
        ${INCLUDE_FILES}
    DESTINATION
        "${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_INCLUDEDIR}"
)
install(
    FILES
        ${CMAKE_CURRENT_BINARY_DIR}/sqlite3.pc
    DESTINATION
        ${CMAKE_INSTALL_LIBDIR}/pkgconfig
)
