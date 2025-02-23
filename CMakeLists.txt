cmake_minimum_required(VERSION 3.12)
project(pybind11_catkin)

find_package(catkin REQUIRED)

catkin_package(
  CFG_EXTRAS pybind11_catkin.cmake
)

set(PYBIND11_MINIMUM_REQUIRED_VERSION 2.5.0)
set(PYBIND11_PYTHON_VERSION ${PYTHON_VERSION_STRING})

# Avoid finding pybind11 in parent catkin workspaces
# To this end, remove paths in CATKIN_WORKSPACES from CMAKE_PREFIX_PATH
foreach (_path ${CATKIN_WORKSPACES})
  list(FIND CMAKE_PREFIX_PATH ${_path} _index)
  if (${_index} GREATER -1)
    list(REMOVE_AT CMAKE_PREFIX_PATH ${_index})
  endif()
endforeach()

find_package(pybind11 ${PYBIND11_MINIMUM_REQUIRED_VERSION} QUIET
  NO_CMAKE_ENVIRONMENT_PATH NO_SYSTEM_ENVIRONMENT_PATH)

if(NOT pybind11_FOUND)
  include(ExternalProject)

  set(INSTALL_DIR "${CMAKE_CURRENT_BINARY_DIR}/pybind11_src-install")
  ExternalProject_Add(pybind11_src
    URL "https://github.com/pybind/pybind11/archive/v2.10.3.zip"
    UPDATE_DISCONNECTED TRUE
    INSTALL_DIR ${INSTALL_DIR}
    CMAKE_ARGS -DPYBIND11_NOPYTHON=TRUE
               -DPYBIND11_TEST=OFF
               -DCMAKE_INSTALL_PREFIX=${INSTALL_DIR}
               -DCMAKE_INSTALL_INCLUDEDIR=include/${PROJECT_NAME}
               -DPYBIND11_INTERNALS_VERSION=6
  )
  # Copy cmake/pybind11 and include/pybind11 to corresponding devel space folders
  ExternalProject_Add_Step(pybind11_src CopyToDevel
    COMMENT "Copying to devel space"
    COMMAND ${CMAKE_COMMAND} -E copy_directory ${INSTALL_DIR}/include/${PROJECT_NAME} ${CATKIN_DEVEL_PREFIX}/include/${PROJECT_NAME}
    COMMAND ${CMAKE_COMMAND} -E copy_directory ${INSTALL_DIR}/share/cmake/pybind11 ${CATKIN_DEVEL_PREFIX}/share/${PROJECT_NAME}/cmake
    DEPENDEES install
  )
  # Install to install space
  install(
    DIRECTORY ${INSTALL_DIR}/include/${PROJECT_NAME}/
    DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  )
  install(
    DIRECTORY ${INSTALL_DIR}/share/cmake/pybind11/
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/cmake
  )
else()
  message(STATUS "Found pybind11 ${pybind11_VERSION}: ${pybind11_DIR}")
endif()
