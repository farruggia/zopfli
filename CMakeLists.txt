project(zopfli)
cmake_minimum_required(VERSION 2.8.7)
set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/CMakeModules")

# C++11 support, Release by default
include(Cpp11)
include(NinjaColorFix)
include(ReleaseDefault)
message(STATUS "Build type: ${CMAKE_BUILD_TYPE}")
# set(COTIRE_MINIMUM_NUMBER_OF_TARGET_SOURCES 1)

set(CMAKE_C_FLAGSFASTDEB "-W -Wall -Wextra -ansi -pedantic -lm -g -O3 -Wno-unused-function")
set(CMAKE_C_FLAGSDEBUG "-W -Wall -Wextra -ansi -pedantic -lm -g -O0 -Wno-unused-function")
set(CMAKE_C_FLAGSRELEASE "-W -Wall -Wextra -ansi -pedantic -lm -march=native -O3 -Wno-unused-function -DNDEBUG")
set(CMAKE_C_FLAGSRELEASE_LTO "-W -Wall -Wextra -ansi -pedantic -lm -O4 -march=native -Wno-unused-function -DNDEBUG")
set(CMAKE_C_FLAGSTEST "-W -Wall -Wextra -ansi -pedantic -lm -g -fsanitize=address -O2 -march=native -Wno-unused-function -DNDEBUG")

set(CMAKE_CXX_FLAGS_FASTDEB "-g -Wall -O3")
set(CMAKE_CXX_FLAGS_DEBUG "-g -Wall -O0")
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -march=native -ffast-math -funroll-loops -DNDEBUG")
set(CMAKE_CXX_FLAGS_RELEASE_LTO "-O4 -march=native -ffast-math -funroll-loops -DNDEBUG")
set(CMAKE_CXX_FLAGS_TEST "-Wall -O3 -march=native -ffast-math -funroll-loops -fsanitize=address -DNDEBUG")

include_directories("${PROJECT_SOURCE_DIR}/include/zopfli")

# Library
file(GLOB libraries lib/*.c*)
add_library(${CMAKE_PROJECT_NAME} ${libraries})