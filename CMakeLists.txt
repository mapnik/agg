cmake_minimum_required(VERSION 3.10)
project(agg VERSION 2.4.0)

include(FeatureSummary)
include(GNUInstallDirs)
include(GenerateExportHeader)

option(BUILD_SHARED_LIBS "build dynamic(ON) or static(OFF) libraries" ON)
option(USE_GPC "Use Gpc Boolean library" OFF)
option(USE_FREETYPE "Use Freetype library" OFF)
option(USE_EXPAT "Use Expat library" OFF)
option(USE_SDL "Use SDL as platform" OFF)
option(USE_AGG2D "Agg 2D graphical context" OFF)
option(USE_DEBUG "For debug version" OFF)


set(MAPNIK_DEBUG_POSTFIX "d" CACHE STRING "sets the debug library postfix")
set(CMAKE_CXX_STANDARD_REQUIRED ON) 
set(CMAKE_CXX_STANDARD 14 CACHE STRING "Sets the c++ standard. c++14 is minimum.")
set(CMAKE_CXX_EXTENSIONS OFF CACHE STRING "Enables the compiler specific extensions.") # Fallsback to -std=c++<ver> if off
message(STATUS "Using c++ extensions: ${CXX_EXTENSIONS}")
message(STATUS "Using c++${CMAKE_CXX_STANDARD}")
message(STATUS "postfix for debug libraries: ${MAPNIK_DEBUG_POSTFIX}")

find_package(X11)
if(USE_EXPAT)
    find_package(EXPAT REQUIRED)
endif()
if(USE_FREETYPE)
    find_package(Freetype REQUIRED)
endif()
if(USE_SDL)
    find_package(SDL2 CONFIG REQUIRED)
endif()

feature_summary(WHAT ENABLED_FEATURES DISABLED_FEATURES)
feature_summary(FILENAME "${CMAKE_CURRENT_BINARY_DIR}/features.log" WHAT ALL)

add_subdirectory(agg)
