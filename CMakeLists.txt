cmake_minimum_required(VERSION 3.26)
project(psnetlib)

set(CMAKE_CXX_STANDARD 20)
option(BUILD_SHARED_LIBS "build shared libraries" OFF)

set(BOOST_ROOT "C:/Users/psdab/Downloads/boost_1_84_0/boost_1_84_0")
set(ASIO_ROOT "C:/Users/psdab/Downloads/asio-1.30.2/asio-1.30.2")
find_package(Boost 1.84.0 REQUIRED)
include_directories(${ASIO_ROOT}/include)
file(GLOB_RECURSE ASIO_HEADERS ${ASIO_ROOT}/include/asio/*.hpp)

add_library(psnetlib STATIC ${ASIO_HEADERS}
        net_tsqueue.h
        ps_net.h
        net_server.h
        net_message.h
        net_connection.h
        net_common.h
        net_client.h
        ps_net.cpp)

target_include_directories(psnetlib PUBLIC ${Boost_INCLUDE_DIRS})
target_link_libraries(psnetlib ${Boost_LIBRARY_DIRS} wsock32 ws2_32)
