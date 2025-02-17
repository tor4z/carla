cmake_minimum_required(VERSION 3.5.1)
project(libcarla)

message(STATUS "Build debug:   ${LIBCARLA_BUILD_DEBUG}")
message(STATUS "Build release: ${LIBCARLA_BUILD_RELEASE}")
message(STATUS "Build test:    ${LIBCARLA_BUILD_TEST}")
message(STATUS "CARLA_THIRD_PARTIES_INFO_FILE: ${CARLA_THIRD_PARTIES_INFO_FILE}")
message(STATUS "CARLA_CONFIG_FILE: ${CARLA_CONFIG_FILE}")
message(STATUS "CMAKE_TOOLCHAIN_FILE: ${CMAKE_TOOLCHAIN_FILE}")


set(libcarla_source_path "${PROJECT_SOURCE_DIR}/../source")
set(libcarla_source_thirdparty_path "${libcarla_source_path}/third-party")

include_directories(${libcarla_source_path})
include_directories(${libcarla_source_thirdparty_path})

if (CARLA_VERSION)
  configure_file(${libcarla_source_path}/carla/Version.h.in ${libcarla_source_path}/carla/Version.h)
endif()

if (CARLA_BUILD_TYPE STREQUAL "Client")
  add_subdirectory("client")
elseif (CARLA_BUILD_TYPE STREQUAL "Server")
  add_subdirectory("server")
elseif (CARLA_BUILD_TYPE STREQUAL "Pytorch")
  add_subdirectory("pytorch")
elseif (CARLA_BUILD_TYPE STREQUAL "ros2")
  add_subdirectory("fast_dds")
else ()
  message(FATAL_ERROR "Unknown build type '${CARLA_BUILD_TYPE}'")
endif ()

# GTest is not compiled on Windows.
if ((LIBCARLA_BUILD_TEST) AND (NOT WIN32) AND (NOT (CARLA_BUILD_TYPE STREQUAL "Pytorch")) AND (NOT (CARLA_BUILD_TYPE STREQUAL "ros2")))
  add_subdirectory("test")
endif()
