cmake_minimum_required(VERSION 2.8)

if (USE_CLANG)
    set(ENV{CC} "clang")
    set(ENV{CXX} "clang++")

    message(STATUS "Using Clang compiler settings")
    SET(CMAKE_C_COMPILER "clang")
    SET(CMAKE_CXX_COMPILER "clang++")

    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} $ENV{CXXFLAGS} -std=c++14 -fPIC -march=native -Wno-return-type -Wno-implicit-function-declaration -Wno-reserved-user-defined-literal -Wno-braced-scalar-init")
    set(ENV{CXXFLAGS} ${CMAKE_CXX_FLAGS})
else ()
    set(ENV{CC} "gcc")
    set(ENV{CXX} "g++")

    message(STATUS "Using GNU compiler settings")
    SET(CMAKE_C_COMPILER "gcc")
    SET(CMAKE_CXX_COMPILER "g++")

    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} $ENV{CXXFLAGS} -std=gnu++14 -fPIC")
    set(ENV{CXXFLAGS} ${CMAKE_CXX_FLAGS})
endif (USE_CLANG)

message(STATUS "Creating Makefiles for Debug Build")
#set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -g -O0 -D_DEBUG_ -std=gnu99 -D_GNU_SOURCE")
#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g -O0 -D_DEBUG_")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O3 -std=gnu99 -D_GNU_SOURCE")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")
set(ENV{CXXFLAGS} ${CMAKE_CXX_FLAGS})

include_directories(
    ${CMAKE_SOURCE_DIR}
)

set (CMAKE_EXPORT_COMPILE_COMMANDS ON)

add_subdirectory(test)
