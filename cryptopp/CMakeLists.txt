
set(srcdir ${CMAKE_CURRENT_SOURCE_DIR})
file(GLOB headers ${srcdir}/*.h)
file(GLOB sources ${srcdir}/*.cpp)

add_library(cryptopp STATIC ${headers} ${sources})

