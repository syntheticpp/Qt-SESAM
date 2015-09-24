
set(srcdir ${CMAKE_CURRENT_SOURCE_DIR})
file(GLOB headers ${srcdir}/*.h)
file(GLOB sources ${srcdir}/*.cpp)
file(GLOB uifiles ${srcdir}/*.ui)

if(UNIX)
    list(REMOVE_ITEM sources ${srcdir}/dump.cpp)
endif()

set(CMAKE_AUTOMOC ON)
qt5_add_resources(resfile ${srcdir}/ctSESAM.qrc)

include_directories(${CMAKE_CURRENT_BINARY_DIR} ${CMAKE_SOURCE_DIR}/cryptopp)

set(bigintdir ${srcdir}/3rdparty/bigint)
include_directories(${bigintdir})

add_executable(ctSESAM ${headers} ${sources} ${mocfiles} ${uis} ${bigintdir}/bigInt.cpp ${resfile})
qt5_use_modules(ctSESAM Widgets Network)
target_link_libraries(ctSESAM cryptopp)
