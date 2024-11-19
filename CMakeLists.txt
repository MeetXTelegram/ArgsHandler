cmake_minimum_required(VERSION 3.5)

project(ArgsHandler LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(spdlog REQUIRED)

include(GNUInstallDirs)
message(STATUS "Library will be installed in ${CMAKE_INSTALL_LIBDIR}; header files will be installed in ${CMAKE_INSTALL_INCLUDEDIR}/ArgsHandler")

include_directories(include)

add_library(ArgsHandler SHARED
    include/Args.hpp
    src/getArg.cpp
    include/Exception.hpp
    src/processWithQemuStyle.cpp
    src/processWithCmakeStyle.cpp
)

install(TARGETS ArgsHandler
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
)
install(FILES include/Args.hpp include/Exception.hpp DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/ArgsHandler)

target_link_libraries(ArgsHandler PRIVATE spdlog::spdlog)
