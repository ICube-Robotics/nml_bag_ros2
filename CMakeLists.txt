cmake_minimum_required(VERSION 3.10)
project(nml_bag_ros2)

find_package(ament_cmake_python REQUIRED)
find_package(ament_cmake_vendor_package REQUIRED)

set(PKG_GIT_TAG main)


set(SOURCE_BUILD_DIR ${CMAKE_CURRENT_SOURCE_DIR}) # Source files
message(STATUS "Cloning mnl_bag:${PKG_GIT_TAG} source")

if(NOT EXISTS "${SOURCE_BUILD_DIR}/vic_python_controllers")
  execute_process(COMMAND
                    git clone --quiet
                    https://github.com/ricmua/nml_bag.git
                      -b ${PKG_GIT_TAG}
                  WORKING_DIRECTORY ${SOURCE_BUILD_DIR}
                  RESULT_VARIABLE GIT_OUT
                  OUTPUT_VARIABLE GIT_OUT)
endif()

ament_python_install_package(
  nml_bag
  PACKAGE_DIR ${SOURCE_BUILD_DIR}/nml_bag/nml_bag
)

ament_package()
