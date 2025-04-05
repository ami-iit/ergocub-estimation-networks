# SPDX-FileCopyrightText: Fondazione Istituto Italiano di Tecnologia (IIT)
# SPDX-License-Identifier: BSD-3-Clause

cmake_minimum_required(VERSION 3.16...4.0)

project(ergocub-estimation-networks LANGUAGES NONE)

include(GNUInstallDirs)

# Function to install models for a specific robot
function(install_robot_models robot_dir)
    file(GLOB_RECURSE model_files RELATIVE ${CMAKE_CURRENT_SOURCE_DIR}/${robot_dir}
        "${CMAKE_CURRENT_SOURCE_DIR}/${robot_dir}/*.onnx")
    if(model_files)
        foreach(model_file ${model_files})
            get_filename_component(model_name ${model_file} NAME)
            install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/${robot_dir}/${model_file}
                DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/ICUBcontrib/robots/${robot_dir}
                RENAME "${model_name}") # Keep only the filename
        endforeach()
    endif()
endfunction()

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
subdirlist(robot_dirs ${CMAKE_CURRENT_SOURCE_DIR})
# Install each models for each robot
foreach (robot_dir ${robot_dirs})
    install_robot_models("${robot_dir}")
endforeach()

# Define `uninstall` target
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR})
include(AddUninstallTarget)
