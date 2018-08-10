cmake_minimum_required(VERSION 3.9)
project(math)

option(tests "tests" ON)

set(CMAKE_CXX_STANDARD 11)

include_directories(${PROJECT_SOURCE_DIR}/include)

set(SOURCES
        ${PROJECT_SOURCE_DIR}/src/main.cpp
        ${PROJECT_SOURCE_DIR}/src/functions.cpp
        )

add_executable(${PROJECT_NAME} ${SOURCES})

if (tests MATCHES ON)
    include(CTest)
    add_subdirectory(tests)
endif ()
