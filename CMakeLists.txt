cmake_minimum_required(VERSION 3.9)
project(readerwriterqueue VERSION 1.0.0)

include(GNUInstallDirs)

add_library(${PROJECT_NAME} INTERFACE)

target_include_directories(readerwriterqueue INTERFACE ${CMAKE_CURRENT_SOURCE_DIR})

install(FILES atomicops.h readerwriterqueue.h readerwritercircularbuffer.h LICENSE.md
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME})


option(WITH_TESTS "Whether to build tests" OFF)
if (WITH_TESTS)
        add_library(simple_thread tests/common/simplethread.cpp tests/common/simplethread.h)
        target_include_directories(simple_thread PUBLIC tests/common)

        add_executable(unittests tests/unittests/unittests.cpp)
        target_link_libraries(unittests PUBLIC simple_thread ${PROJECT_NAME})
endif()