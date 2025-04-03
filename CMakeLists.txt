# SPDX-FileCopyrightText: Fondazione Istituto Italiano di Tecnologia (IIT)
# SPDX-License-Identifier: BSD-3-Clause

cmake_minimum_required(VERSION 3.16...4.0)

project(ergocub-estimation-networks LANGUAGES NONE)

include(GNUInstallDirs)

# List the subdirectories (http://stackoverflow.com/questions/7787823/cmake-how-to-get-the-name-of-all-subdirectories-of-a-directory)
macro(SUBDIRLIST result curdir)
    file(GLOB children RELATIVE ${curdir} ${curdir}/*)
    set(dirlist "")
    foreach(child ${children})
        if(IS_DIRECTORY ${curdir}/${child})
            list(APPEND dirlist ${child})
        endif()
    endforeach()
    set(${result} ${dirlist})
endmacro()

# Get list of models
subdirlist(subdirs ${CMAKE_CURRENT_SOURCE_DIR})
# Install each models for each robot
foreach (dir ${subdirs})
    install(DIRECTORY ${dir}
            DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/ICUBcontrib/robots)
endforeach()

# Define `uninstall` target
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR})
include(AddUninstallTarget)
