# Copyright (C) 2017 PSPC-lab - Department of Informatics, Bioengineering,
#                    Robotics and Systems Engineering - University of Genoa
# All Rights Reserved.
# Authors: Agostino Gibaldi, Andrea Canessa, Silvio P. Sabatini

find_package(YARP QUIET)
if(YARP_FOUND)
  list(APPEND CMAKE_MODULE_PATH ${YARP_MODULE_PATH})
  add_subdirectory(icub-vergence-control)
  add_subdirectory(icubsim-screen-handler)
else()
  message(STATUS "YARP not found")
endif()
