cmake_minimum_required(VERSION 3.2)

set(Boost_USE_STATIC_LIBS ON)
set(Boost_USE_MULTITHREADED ON)
find_package(Boost REQUIRED COMPONENTS filesystem program_options system thread)
include_directories(${Boost_INCLUDE_DIRS})
link_directories(${Boost_LIBRARY_DIR})

set(SRCS main.cpp)

set(CMAKE_CXX_FLAGS
  "${CMAKE_CXX_FLAGS} -g -std=c++14 -frtti -Wall \
   -Wno-invalid-offsetof -Wno-sign-compare -Wno-char-subscripts -Wno-format\
   -Wno-deprecated -Wno-unused-local-typedefs")

set(CMAKE_CXX_FLAGS_DEBUG
  "${CMAKE_CXX_FLAGS_DEBUG} -O0")

set(CMAKE_CXX_FLAGS_RELEASE
  "${CMAKE_CXX_FLAGS_RELEASE} -O3 -fno-strict-aliasing")

set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -g")

add_definitions(-D_FILE_OFFSET_BITS=64)
set_property(DIRECTORY APPEND PROPERTY COMPILE_DEFINITIONS
  "$<$<CONFIG:Debug>:DEBUG;_DEBUG;_FORTIFY_SOURCE=2;>")
set_property(DIRECTORY APPEND PROPERTY COMPILE_DEFINITIONS
  "$<$<CONFIG:Release>:NDEBUG;>")

add_executable(scratch ${SRCS})

target_link_libraries(scratch ${Boost_LIBRARIES})

