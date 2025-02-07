cmake_minimum_required(VERSION 3.5)

project(miniply LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include_directories(.)

add_executable(miniply-perf
  miniply.cpp
  miniply.h
  extra/miniply-perf.cpp
)

add_executable(miniply-info
  miniply.cpp
  miniply.h
  extra/miniply-info.cpp
)

add_library(miniply
  miniply.cpp
  miniply.h
)

include(CMakePackageConfigHelpers)

# Installation paths
include(GNUInstallDirs)

configure_package_config_file(
  cmake/config.cmake.in
  ${CMAKE_CURRENT_BINARY_DIR}/generated/${PROJECT_NAME}-config.cmake
  INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME})

install(
  FILES ${CMAKE_CURRENT_BINARY_DIR}/generated/${PROJECT_NAME}-config.cmake
  DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME})

install(
  FILES miniply.h
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

install(
  TARGETS ${PROJECT_NAME}
  EXPORT ${PROJECT_NAME}-targets
  INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

install(
  EXPORT ${PROJECT_NAME}-targets
  NAMESPACE ${PROJECT_NAME}::
  DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME})
