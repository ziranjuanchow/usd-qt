
# >=3.1 is required for CMAKE_CXX_STANDARD
cmake_minimum_required(VERSION 3.1)
project(usdqt)

set(CMAKE_MODULE_PATH "${CMAKE_MODULE_PATH};${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules;${CMAKE_CURRENT_SOURCE_DIR}/cmake/macros")

add_compile_options(-Wall -Wno-unused-local-typedefs
                    -Wno-deprecated -DBUILD_OPTLEVEL_OPT -DBUILD_COMPONENT_SRC_PREFIX="")

option(INSTALL_PURE_PYTHON "Install pure python files. Disable to only install compiled extension" ON)

include(Private)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(USD REQUIRED)
find_package(TBB REQUIRED)

add_definitions(-DPXR_PYTHON_SUPPORT_ENABLED)
find_package(PythonInterp 2.7 REQUIRED)
find_package(PythonLibs 2.7 REQUIRED)

set(Boost_USE_STATIC_LIBS OFF)
find_package(Boost COMPONENTS python REQUIRED)

include_directories(${Boost_INCLUDE_DIRS})

include_directories(${USD_INCLUDE_DIR})
link_directories(${USD_LIBRARY_DIR})

include_directories(SYSTEM ${PYTHON_INCLUDE_DIRS})
include_directories(SYSTEM ${TBB_INCLUDE_DIRS})

add_subdirectory(pxr)
