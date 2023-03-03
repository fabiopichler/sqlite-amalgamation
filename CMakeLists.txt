
project(sqlite3 LANGUAGES C)

set(SRC_FILES
    include/sqlite3.h
    src/sqlite3.c
)

add_library(sqlite3 STATIC ${SRC_FILES})

if(UNIX)
    set_property(TARGET sqlite3 PROPERTY POSITION_INDEPENDENT_CODE TRUE)
endif()
