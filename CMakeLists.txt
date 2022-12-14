cmake_minimum_required(VERSION 3.8 FATAL_ERROR)
project(sherpa-onnx)

set(SHERPA_ONNX_VERSION "0.1")

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")

set(CMAKE_SKIP_BUILD_RPATH FALSE)
set(BUILD_RPATH_USE_ORIGIN TRUE)
set(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)

if(NOT APPLE)
  set(SHERPA_ONNX_RPATH_ORIGIN "$ORIGIN")
else()
  set(SHERPA_ONNX_RPATH_ORIGIN "@loader_path")
endif()

set(CMAKE_INSTALL_RPATH ${SHERPA_ONNX_RPATH_ORIGIN})
set(CMAKE_BUILD_RPATH ${SHERPA_ONNX_RPATH_ORIGIN})

set(BUILD_SHARED_LIBS ON)
if(WIN32)
  message(STATUS "Set BUILD_SHARED_LIBS to OFF for Windows")
  set(BUILD_SHARED_LIBS OFF CACHE BOOL "" FORCE)
endif()

if(NOT CMAKE_BUILD_TYPE)
  message(STATUS "No CMAKE_BUILD_TYPE given, default to Release")
  set(CMAKE_BUILD_TYPE Release)
endif()
message(STATUS "CMAKE_BUILD_TYPE: ${CMAKE_BUILD_TYPE}")

set(CMAKE_CXX_STANDARD 14 CACHE STRING "The C++ version to be used.")
set(CMAKE_CXX_EXTENSIONS OFF)

include_directories("/usr/local/include/onnxruntime")
include_directories("/usr/local/include/onnxruntime/core/session")
link_directories("/usr/local/lib")

add_subdirectory(3rd/kaldiio)
include_directories(3rd/kaldiio/kaldiio)

add_subdirectory(sherpa_ort)
