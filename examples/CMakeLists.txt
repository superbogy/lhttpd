cmake_minimum_required (VERSION 2.6)

set (NAME lhttpd)
project (${NAME}_examples)

set (CMAKE_C_FLAGS "-g -std=gnu99 -Wall ${CMAKE_C_FLAGS}")

set (SOURCES ${SOURCES}
        helloworld.c
        route.c
        tcp_echo.c
        static_page/main.c)

find_library(LIBTHIS lhttpd)
if (${LIBTHIS} MATCHES ".*-NOTFOUND")
    message(FATAL_ERROR "Not install lib${NAME}")
endif()

cmake_policy(SET CMP0037 OLD)

foreach (SOURCE ${SOURCES})
    string(REPLACE ".c" "" EXEC ${SOURCE})
    add_executable(${EXEC} ${SOURCE})
    target_link_libraries(${EXEC} ${NAME})
endforeach()