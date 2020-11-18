cmake_minimum_required(VERSION 3.10)
project(restclient-cpp VERSION 1.0.0 DESCRIPTION "REST library for C++")

set (SOURCES
    connection.cc
    helpers.cc
    restclient.cc)

set (HEADERS
    restclient-cpp/connection.h
    restclient-cpp/helpers.h
    restclient-cpp/restclient.h)

set (INSTALL_HEADERS ${HEADERS}
                     ${CMAKE_CURRENT_BINARY_DIR}/restclient-cpp/version.h)

include_directories(
    BEFORE "${CMAKE_CURRENT_BINARY_DIR}/"
    BEFORE "${CMAKE_INSTALL_PREFIX}/${CMAKE_BUILD_TYPE}/include/")

add_library(restclient-cpp STATIC version.h.in ${HEADERS} ${SOURCES})
configure_file(version.h.in restclient-cpp/version.h)

target_compile_features(restclient-cpp PUBLIC cxx_std_17)
set_target_properties(restclient-cpp PROPERTIES
    PUBLIC_HEADER "${INSTALL_HEADERS}")

install(TARGETS restclient-cpp
    ARCHIVE       DESTINATION "${CMAKE_BUILD_TYPE}/lib"
    LIBRARY       DESTINATION "${CMAKE_BUILD_TYPE}/lib"
    PUBLIC_HEADER DESTINATION "${CMAKE_BUILD_TYPE}/include/restclient-cpp")
