cmake_minimum_required(VERSION 2.8)


set(EXECUTABLE_OUTPUT_PATH   ${CMAKE_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_PATH      ${CMAKE_BINARY_DIR}/bin)
set(RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

project(ctSesam)


if(MSVC)
    add_definitions(-D_USE_MATH_DEFINES)
    #set(MSVC_W_DISABLE "/wd4522 /wd4503")
    #set(MSVC_W_DISABLE "${MSVC_W_DISABLE} /wd4244 /wd4267") # int <-> 64 bit casting
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${MSVC_W_DISABLE} /we4013")
else()
    if(UNIX)
        set(fpic -fPIC)
    endif()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${fpic} -std=c++14 -Wall -Wextra")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ")
endif()

macro(use_qt5lib lib)
    find_package(${lib} REQUIRED)
    include_directories(${${lib}_INCLUDE_DIRS})
endmacro()
use_qt5lib(Qt5Core)
use_qt5lib(Qt5Gui)
use_qt5lib(Qt5Widgets)
use_qt5lib(Qt5Network)
use_qt5lib(Qt5Concurrent)
get_target_property(qmakebin Qt5::qmake IMPORTED_LOCATION)
get_filename_component(QT_BINARY_DIR ${qmakebin} PATH)
message(STATUS "Using Qt5 from ${QT_BINARY_DIR}")
set(qtver ${Qt5Core_VERSION})

add_definitions(-DQTSESAM_VERSION="2.0.3")
add_definitions(-DCRYPTOPP_DISABLE_X86ASM -DCRYPTOPP_DISABLE_SSSE3)

add_subdirectory(cryptopp)
add_subdirectory(ctSESAM)
