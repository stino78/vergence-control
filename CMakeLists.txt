# Copyright (C) 2017 PSPC-lab - Department of Informatics, Bioengineering,
#                    Robotics and Systems Engineering - University of Genoa
# All Rights Reserved.
# Authors: Agostino Gibaldi, Andrea Canessa, Silvio P. Sabatini

cmake_minimum_required(VERSION 3.1)
project(VergenceControl LANGUAGES CXX VERSION 1.0.0)

include(GNUInstallDirs)
set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED 11)

find_package(OpenCV REQUIRED)

option(BUILD_SHARED_LIBS "Build libraries as shared as opposed to static" OFF)
option(ENABLE_RPATH "Enable RPATH for this library" ON)

mark_as_advanced(ENABLE_RPATH)
include(AddInstallRPATHSupport)
add_install_rpath_support(BIN_DIRS "${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_BINDIR}"
                          LIB_DIRS "${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}"
                          DEPENDS ENABLE_RPATH
                          USE_LINK_PATH)

if(NOT CMAKE_CONFIGURATION_TYPES)
  if(NOT CMAKE_BUILD_TYPE)
      message(STATUS "Setting build type to 'Release' as none was specified.")
      set_property(CACHE CMAKE_BUILD_TYPE PROPERTY VALUE "Release")
  endif()
endif()

add_subdirectory(src)

include(InstallBasicPackageFiles)
install_basic_package_files(${PROJECT_NAME} VARS_PREFIX ${PROJECT_NAME}
                                            VERSION ${${PROJECT_NAME}_VERSION}
                                            COMPATIBILITY AnyNewerVersion
                                            TARGETS_PROPERTY ${PROJECT_NAME}_TARGETS
                                            NO_CHECK_REQUIRED_COMPONENTS_MACRO)
include(AddUninstallTarget)

add_subdirectory(test)
add_subdirectory(icub)
