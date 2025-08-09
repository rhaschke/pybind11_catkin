^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Changelog for package pybind11_catkin
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.0.0 (2025-08-09)
------------------
* Drop pybind11-dev from depends
* Bump to pybind11 version 3.0.0
* Fix dependency on python-dev
* Export pybind11_catkin_INCLUDE_DIRS
* Forward pybind11::pybind11 to pybind11_catkin_LIBRARIES
* Require pybind11 in pybind11_catkin.cmake
* Don't use pybind11 from parent catkin workspaces
  This contradicts the idea of overlaying those workspaces with the current pybind11_catkin package.
* Fix cmake
  - Ensure correct relative location of pybind11Config.cmake and includes
  - Only perform install when NOT pybind11_FOUND
* Simplify pybind11_catkin.cmake
* Add message informing about existing pybind11 version
* Fix issues including Python.h
  New FindPython module uses Python_INCLUDE_DIRS instead of PYTHON_INCLUDE_DIRS
* Increase cmake_minimum_required to 3.12
  pybind11 relies on modern FindPython `introduced in cmake 3.12 <https://cmake.org/cmake/help/latest/module/FindPython.html>`_
* Set PYBIND11_PYTHON_VERSION
* Use system pybind11 when available `#23 <https://github.com/wxmerkt/pybind11_catkin/issues/23>`_
* Contributors: Robert Haschke, Simon Schmeisser, Wolfgang Merkt

2.10.3 (2023-02-09)
-------------------
* Ignore DESTDIR for the internal ExternalProject_Add() command (`#19 <https://github.com/ipab-slmc/pybind11_catkin/issues/19>`_)
* Update CI from Travis to GitHub Actions
* Update pybind11 to version 2.10.3 to support python3.11 (`#21 <https://github.com/ipab-slmc/pybind11_catkin/issues/21>`_)
* Update pybind to version 2.6.1 (`#13 <https://github.com/ipab-slmc/pybind11_catkin/issues/13>`_)
* Contributors: Henry Schreiner, Hongzhuo Liang, Johannes Meyer, Wolfgang Merkt

2.5.0 (2020-05-24)
------------------
* Update to v2.5.0, add compatibility with ROS Noetic (20.04) (`#12 <https://github.com/ipab-slmc/pybind11_catkin/issues/12>`_)
* Bump CMake version to avoid CMP0048. This breaks support with ROS Indigo (14.04).
* Contributors: Wolfgang Merkt

2.4.3 (2019-12-23)
------------------
* Clean-up of CMake files and logic (by @rhaschke) - `#11 <https://github.com/ipab-slmc/pybind11_catkin/issues/11>`_
* Ensure pybind11 uses same python version as catkin
* Update pybind11 version to 2.4.3
* Clarify bleeding edge vs releases in README - cf `#9 <https://github.com/ipab-slmc/pybind11_catkin/issues/9>`_
* Contributors: Robert Haschke, Wolfgang Merkt

2.2.4 (2019-01-15)
------------------
* Fixes installation of generated files
* Fix for arm-based builds
* Add dummy header to make bloom happy
* Update to v2.2.4
* Do not overwrite the exported include_dirs
  - Addresses `ros/rosdistro#18473 <https://github.com/ros/rosdistro/issues/18473>`_
* Update CMake logic to export devel/install more cleanly
* Added links to examples in readme.
* Update README.md
* Contributors: Artur Miller, Wolfgang Merkt

2.2.3 (2018-07-12)
------------------
* Adds workaround for both devel and install workspaces
* Add README with Travis Badge
* Add ROS Industrial CI
* pybind11_catkin: Do not change source directory on build
* Silence pybind11 warning
* Compatibility with 16.04 and ROS Kinetic
* pybind11 via http clone
* Added back python version override
* pybind11 >> pybind11_catkin with the submodule changed to external project
* Contributors: Vladimir Ivan, Wolfgang Merkt
