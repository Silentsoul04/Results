
To adapt this template to your own project, follow these steps:


In the root directory adapt/change/do the following:
--------------------------------------------------------------------

* [ ] Edit AUTHORS
* [ ] Edit LICENSE
* [ ] Edit README.md
* [ ] Rename ./template-config.cmake -> ./\<project>-config.cmake

CMakeLists.txt:
* [ ]  Set META_PROJECT_*
* [ ]  Set META_VERSION_*
* [ ]  Set META_AUTHOR_*
* [ ]  Set META_CMAKE_INIT_SHA (to the commit hash of the applied cmake-init template, e.g., to 83d7cbc29a6fcb74a98498e5b0fcebd953d9d5cc)
* [ ]  Adjust INSTALL_* to the desired install locations for all systems (defaults should be fine for a start)


In subdirectory "./deploy/" do:
--------------------------------------------------------------------

deploy/CMakeLists.txt:
* [ ] Rename deploy/packages/pack-template.cmake -> pack-\<project>.cmake

deploy/packages/pack-\<project>.cmake:
* [ ] Adjust OPTION_PACK_GENERATOR to your liking for all systems
* [ ] Adjust package options, e.g., CPACK_DEBIAN_PACKAGE_DEPENDS, CPACK_DEBIAN_PACKAGE_SECTION, CPACK_DEBIAN_PACKAGE_PRIORITY, CPACK_RPM_PACKAGE_LICENSE, CPACK_RPM_PACKAGE_GROUP, ...


In subdirectory "./source/" do:
--------------------------------------------------------------------

* [ ] Rename template-version.h -> \<project>-version.h


In subdirectory "./source/baselib/source" do:
--------------------------------------------------------------------

source/baselib/source/baselib.cpp:
* [ ] Substitute template/template-version.h -> \<project>/\<project>-version.h
* [ ] Substitute TEMPLATE_VERSION -> \<PROJECT>_VERSION

* [ ] Rename template-version.h -> \<project>-version.h


In subdirectory "./source/examples/fibcmd" do:
--------------------------------------------------------------------

source/fibcmd/main.cpp:
* [ ] Substitute template-version.h -> \<project>-version.h
* [ ] Substitute TEMPLATE_VERSION -> \<PROJECT>_VERSION


In subdirectory "./source/codegeneration/" do:
--------------------------------------------------------------------

* [ ] Remove/replace *_features.h for project-specific compiler feature detection headers (generate with current CMake and place here old cmake compatibility)


In subdirectory "./docs/api-docs/" do:
--------------------------------------------------------------------

docs/api-docs/doxyfile.in:
* [ ] Adjust INPUT tag (list of doxygen annotated sources)

docs/api-docs/CMakeLists.txt
* [ ] Adjust DEPENDS parameter to include all targets of project


In subdirectory "./docs/manual/" do:
--------------------------------------------------------------------

docs/manual/cmake-init.tex:
* [ ] Rename to match own project name

docs/manual/CMakeLists.txt
* [ ] Adjust source and pdf file name


In subdirectory "./source/tests/" do:
--------------------------------------------------------------------

source/tests/CMakeLists.txt:
* [ ]  Set META_PROJECT_NAME


General stuff left to do:
--------------------------------------------------------------------

* [ ] Rename and adjust targets in source/
* [ ] Add new targets to source/CMakeLists.txt
* [ ] Add new targets to ./{project}-config.cmake
* [ ] Add new targets to the INPUT tag in docs/api-docs/doxyfile.in
* [ ] Remove data/DATA_FOLDER.txt
* [ ] Populate data/
* [ ] Remove ADAPT.md

# 
# CMake options
# 

# CMake version
cmake_minimum_required(VERSION 3.0 FATAL_ERROR)

#
# Configure CMake environment
#

# Register general cmake commands
include(cmake/Custom.cmake)

# Set policies
set_policy(CMP0054 NEW) # ENABLE CMP0054: Only interpret if() arguments as variables or keywords when unquoted.
set_policy(CMP0042 NEW) # ENABLE CMP0042: MACOSX_RPATH is enabled by default.
set_policy(CMP0063 NEW) # ENABLE CMP0063: Honor visibility properties for all target types.
set_policy(CMP0077 NEW) # ENABLE CMP0077: option() honors normal variables

# Include cmake modules
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

include(GenerateExportHeader)

set(WriterCompilerDetectionHeaderFound NOTFOUND)
# This module is only available with CMake >=3.1, so check whether it could be found
# BUT in CMake 3.1 this module doesn't recognize AppleClang as compiler, so just use it as of CMake 3.2
if (${CMAKE_VERSION} VERSION_GREATER "3.2")
    include(WriteCompilerDetectionHeader OPTIONAL RESULT_VARIABLE WriterCompilerDetectionHeaderFound)
endif()

# Include custom cmake modules
include(cmake/Coverage.cmake)
include(cmake/GenerateTemplateExportHeader.cmake)
include(cmake/GetGitRevisionDescription.cmake)
include(cmake/HealthCheck.cmake)


# 
# Project description and (meta) information
# 

# Get git revision
get_git_head_revision(GIT_REFSPEC GIT_SHA1)
string(SUBSTRING "${GIT_SHA1}" 0 12 GIT_REV)
if(NOT GIT_SHA1)
    set(GIT_REV "0")
endif()

# Meta information about the project
set(META_PROJECT_NAME        "template")
set(META_PROJECT_DESCRIPTION "CMake Project Template")
set(META_AUTHOR_ORGANIZATION "CG Internals GmbH")
set(META_AUTHOR_DOMAIN       "https://github.com/cginternals/cmake-init/")
set(META_AUTHOR_MAINTAINER   "opensource@cginternals.com")
set(META_VERSION_MAJOR       "2")
set(META_VERSION_MINOR       "0")
set(META_VERSION_PATCH       "0")
set(META_VERSION_REVISION    "${GIT_REV}")
set(META_VERSION             "${META_VERSION_MAJOR}.${META_VERSION_MINOR}.${META_VERSION_PATCH}")
set(META_NAME_VERSION        "${META_PROJECT_NAME} v${META_VERSION} (${META_VERSION_REVISION})")
set(META_CMAKE_INIT_SHA      "${GIT_REV}")

string(MAKE_C_IDENTIFIER ${META_PROJECT_NAME} META_PROJECT_ID)
string(TOUPPER ${META_PROJECT_ID} META_PROJECT_ID)


# 
# Project configuration options
# 

# Project options
option(BUILD_SHARED_LIBS      "Build shared instead of static libraries."              ON)
option(OPTION_SELF_CONTAINED  "Create a self-contained install with all dependencies." OFF)
option(OPTION_BUILD_TESTS     "Build tests."                                           ON)
option(OPTION_BUILD_DOCS      "Build documentation."                                   OFF)
option(OPTION_BUILD_EXAMPLES  "Build examples."                                        OFF)
option(OPTION_ENABLE_COVERAGE "Add coverage information."                              OFF)


# 
# Declare project
# 

# Generate folders for IDE targets (e.g., VisualStudio solutions)
set_property(GLOBAL PROPERTY USE_FOLDERS ON)
set(IDE_FOLDER "")

# Declare project
project(${META_PROJECT_NAME} C CXX)

# Set output directories
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR})

# Create version file
file(WRITE "${PROJECT_BINARY_DIR}/VERSION" "${META_NAME_VERSION}")


#
# Project Health Check Setup
#

# Add cmake-init template check cmake targets
add_check_template_target(${META_CMAKE_INIT_SHA})

# Configure health check tools
enable_cppcheck(ON)
enable_clang_tidy(ON)
enable_coverage(${OPTION_ENABLE_COVERAGE})


# 
# Compiler settings and options
# 

include(cmake/CompileOptions.cmake)


# 
# Deployment/installation setup
# 

# Get project name
set(project ${META_PROJECT_NAME})

# Check for system dir install
set(SYSTEM_DIR_INSTALL FALSE)
if("${CMAKE_INSTALL_PREFIX}" STREQUAL "/usr" OR "${CMAKE_INSTALL_PREFIX}" STREQUAL "/usr/local")
    set(SYSTEM_DIR_INSTALL TRUE)
endif()

# Installation paths
if(UNIX AND SYSTEM_DIR_INSTALL)
    # Install into the system (/usr/bin or /usr/local/bin)
    set(INSTALL_ROOT      "share/${project}")       # /usr/[local]/share/<project>
    set(INSTALL_CMAKE     "share/${project}/cmake") # /usr/[local]/share/<project>/cmake
    set(INSTALL_EXAMPLES  "share/${project}")       # /usr/[local]/share/<project>
    set(INSTALL_DATA      "share/${project}")       # /usr/[local]/share/<project>
    set(INSTALL_BIN       "bin")                    # /usr/[local]/bin
    set(INSTALL_SHARED    "lib")                    # /usr/[local]/lib
    set(INSTALL_LIB       "lib")                    # /usr/[local]/lib
    set(INSTALL_INCLUDE   "include")                # /usr/[local]/include
    set(INSTALL_DOC       "share/doc/${project}")   # /usr/[local]/share/doc/<project>
    set(INSTALL_SHORTCUTS "share/applications")     # /usr/[local]/share/applications
    set(INSTALL_ICONS     "share/pixmaps")          # /usr/[local]/share/pixmaps
    set(INSTALL_INIT      "/etc/init")              # /etc/init (upstart init scripts)
else()
    # Install into local directory
    set(INSTALL_ROOT      ".")                      # ./
    set(INSTALL_CMAKE     "cmake")                  # ./cmake
    set(INSTALL_EXAMPLES  ".")                      # ./
    set(INSTALL_DATA      ".")                      # ./
    set(INSTALL_BIN       ".")                      # ./
    set(INSTALL_SHARED    "lib")                    # ./lib
    set(INSTALL_LIB       "lib")                    # ./lib
    set(INSTALL_INCLUDE   "include")                # ./include
    set(INSTALL_DOC       "doc")                    # ./doc
    set(INSTALL_SHORTCUTS "misc")                   # ./misc
    set(INSTALL_ICONS     "misc")                   # ./misc
    set(INSTALL_INIT      "misc")                   # ./misc
endif()

# Set runtime path
set(CMAKE_SKIP_BUILD_RPATH            FALSE) # Add absolute path to all dependencies for BUILD
set(CMAKE_BUILD_WITH_INSTALL_RPATH    FALSE) # Use CMAKE_INSTALL_RPATH for INSTALL
set(CMAKE_INSTALL_RPATH_USE_LINK_PATH FALSE) # Do NOT add path to dependencies for INSTALL

if(NOT SYSTEM_DIR_INSTALL)
    # Find libraries relative to binary
    if(APPLE)
        set(CMAKE_INSTALL_RPATH "@loader_path/../../../${INSTALL_LIB}")
    else()
        set(CMAKE_INSTALL_RPATH "$ORIGIN/${INSTALL_LIB}")       
    endif()
endif()


# 
# Project modules
# 

add_subdirectory(source)
add_subdirectory(docs)
add_subdirectory(deploy)


# 
# Deployment (global project files)
# 

# Install version file
install(FILES "${PROJECT_BINARY_DIR}/VERSION" DESTINATION ${INSTALL_ROOT} COMPONENT runtime)

# Install cmake find script for the project
install(FILES ${META_PROJECT_NAME}-config.cmake DESTINATION ${INSTALL_ROOT} COMPONENT dev)

# Install the project meta files
install(FILES AUTHORS   DESTINATION ${INSTALL_ROOT} COMPONENT runtime)
install(FILES LICENSE   DESTINATION ${INSTALL_ROOT} COMPONENT runtime)
install(FILES README.md DESTINATION ${INSTALL_ROOT} COMPONENT runtime)

# Install runtime data
install(DIRECTORY ${PROJECT_SOURCE_DIR}/data DESTINATION ${INSTALL_DATA} COMPONENT runtime)

Copyright (c) 2012-2015 Computer Graphics Systems Group at the Hasso-Plattner-Institute, Germany. 

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

<br><a href="https://github.com/cginternals/cmake-init/"><img src="https://raw.githubusercontent.com/cginternals/cmake-init/master/cmake-init-logo.svg?sanitize=true" width="50%"></a>

The C++ CMake Project Template

[![Travis](https://img.shields.io/travis/cginternals/cmake-init/master.svg?style=flat&logo=travis)](https://travis-ci.org/cginternals/cmake-init)
[![Appveyor](https://img.shields.io/appveyor/ci/scheibel/cmake-init/master.svg?style=flat&logo=appveyor)](https://ci.appveyor.com/project/scheibel/cmake-init/branch/master)
[![Tokei](https://tokei.rs/b1/github/cginternals/cmake-init)](https://github.com/Aaronepower/tokei)
[![Setup Guide](https://img.shields.io/badge/cmake%20guide-wiki-blue.svg?style=flat)](https://github.com/cginternals/cmake-init/wiki/Setup-Guide)


*cmake-init* is a sophisticated copy & paste template for modern C and C++ projects.
The main goals include support of all use cases around software development (programming, testing, Q&A, deployment, documentation) while being modular, flexible, and idiomatic. *cmake-init* is therefore a collection of cmake best-practices.

The main target platforms are typical desktop, laptop, and server platforms. Currently supported are:

* Windows
* macOS
* GNU/Linux

However, other UNIX versions may work as well if they are supported by CMake.

The cmake-init template assumes you want to setup a project using
* CMake (3.0 or above)
* C/C++ compiler


# Contents

* [Usage](#usage)
  * [Adaption Guide](#adaption-guide)
* [Non-Goals](#non-goals)
* [Module Documentation](#module-documentation)
  * [Core Modules](#core-modules)
    * [CMake Initialization](cmake-initialization)
    * [CMake Backward Compatibility](#cmake-backward-compatability)
    * [Project Meta Information](#project-meta-information)
    * [Project Meta Information Code Generation](#project-meta-information-code-generation)
    * [Project Build Options](#project-build-options)
  * [Maintainer Modules](#maintainer-modules)
    * [cmake-init Template Check](#cmake-init-template-check)
  * [Development Modules](#development-modules)
    * [Version Control System Integration](#version-control-system-integration)
    * [Build Targets](#build-targets)
    * [Documentation](#documentation)
    * [Tests](#tests)
    * [Linter](#linter)
    * [Continuous Integration](#continuous-integration)
    * [Deployment](#deployment)
    * [Packaging](#packaging)
    * [Run-time Assets](#run-time-assets)

# Usage

The intended use of the template is a copy of the current version with a subsequent replacement of project names and customization of modules to your needs. This is documented within the [adaption guide](#adaption-guide).
Another approach is the initialization of a new CMake project where the required features are adopted from cmake-init. We propose the former workflow.

Concluding, a new project should contain the core modules and, as needed, add the maintainer and development modules as required. All modules are designed in a way that they can be excluded. The process of integration or removal of a module/feature is documented with each module.

## Adaption Guide

The file [ADAPT.md](https://github.com/cginternals/cmake-init/blob/master/ADAPT.md) contains a task checklist for new projects. Your start with a copy of cmake-init and process each item from the checklist, adjusting the template to your needs.

## Update

After some time working on a project, cmake-init may be updated and you want to integrate the changes.
For an overview of changes we suggest to use the [cmake-init Template Check](#cmake-init-template-check) module.
Alternatively, you can update the required modules selectively.



# Non-Goals

In order to be usable in a deterministic, idiomatic fashion, cmake-init avoids the following approaches and features:

## Super-Build

Due to the current semantics of targets and CMake internals, combining multiple
cmake-init projects into one super-build project is not officially supported.
There are limited and restricting workarounds.
Actual solution: treat each project separately and use explicit dependency management.

## High Abstraction

We use low abstractions to not build a language upon CMake a user has to learn.

## File Glob

Explicit source specification prevents erroneous cases when adding and removing
sources from the project tree.

# Module Documentation

## Core Modules

### CMake Initialization

As with most CMake projects, cmake-init initializes the CMake environment. This includes the minimum required CMake version,

```cmake
# CMake version
cmake_minimum_required(VERSION 3.0 FATAL_ERROR)
```

required policies,

```cmake
# Set policies
set_policy(CMP0054 NEW) # ENABLE CMP0054: Only interpret if() arguments as variables or keywords when unquoted.
set_policy(CMP0042 NEW) # ENABLE CMP0042: MACOSX_RPATH is enabled by default.
set_policy(CMP0063 NEW) # ENABLE CMP0063: Honor visibility properties for all target types.
```

adaption of the cmake module path,

```cmake
# Include cmake modules
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
```

and an include of default modules that are typically required for each project.

```cpp
include(GenerateExportHeader)
include(WriteCompilerDetectionHeader)
```


### CMake Backward Compatibility

As some modules as `WriteCompilerDetectionHeader` may not be available, cmake-init suggests to use fallbacks and availability detection.

Using this example, the module include

```cmake
include(WriteCompilerDetectionHeader)
```

is replaced by

```cmake
set(WriterCompilerDetectionHeaderFound NOTFOUND)
# This module is only available with CMake >=3.1, so check whether it could be found
# BUT in CMake 3.1 this module doesn't recognize AppleClang as compiler, so just use it as of CMake 3.2
if (${CMAKE_VERSION} VERSION_GREATER "3.2")
    include(WriteCompilerDetectionHeader OPTIONAL RESULT_VARIABLE WriterCompilerDetectionHeaderFound)
endif()
```

and the result can be later used with

```cmake
if (WriterCompilerDetectionHeaderFound)
  # ...
endif ()
```

Another issue with older CMake versions is the unavailability of then-unpublished language standards (e.g., C++11 and CMake 3.0). For those versions, the compile options has to be extended manually.

For new projects, we suggest to require at least CMake 3.2 and to therefore adjust the minimum required version:

```cmake
cmake_minimum_required(VERSION 3.0 FATAL_ERROR)
```


### Project Meta Information

The declaration of project-wide information--that are used, e.g., within documentation, testing, and deployment--, is combined within the project meta information section in the main `CMakeLists.txt`.

```cmake
#
# Project description and (meta) information
#

# Meta information about the project
set(META_PROJECT_NAME        "template")
set(META_PROJECT_DESCRIPTION "CMake Project Template")
set(META_AUTHOR_ORGANIZATION "CG Internals GmbH")
set(META_AUTHOR_DOMAIN       "https://github.com/cginternals/cmake-init/")
set(META_AUTHOR_MAINTAINER   "opensource@cginternals.com")
set(META_VERSION_MAJOR       "2")
set(META_VERSION_MINOR       "0")
set(META_VERSION_PATCH       "0")
set(META_VERSION_REVISION    "<REVISION>")
set(META_VERSION             "${META_VERSION_MAJOR}.${META_VERSION_MINOR}.${META_VERSION_PATCH}")
set(META_NAME_VERSION        "${META_PROJECT_NAME} v${META_VERSION} (${META_VERSION_REVISION})")
set(META_CMAKE_INIT_SHA      "<CMAKE_INIT_REVISION>")

string(MAKE_C_IDENTIFIER ${META_PROJECT_NAME} META_PROJECT_ID)
string(TOUPPER ${META_PROJECT_ID} META_PROJECT_ID)
```

*cmake-init* supports the projects name, description, organization, domain, and maintainer email as well as detailed version information. For the version, we suggest to use [semantic versioning](https://semver.org/).
Depending on your version control system, you may want to integrate the current revision of the software as well: see [Version Control System Integration](#version-control-system-integration). If you use the [cmake-init Template Check](#cmake-init-template-check) module, the cmake-init SHA is declared within this section, too.

Last, *cmake-init* derives a project ID that complies with the naming schemes of C to be used within auto-generated and derived source code content (e.g., macro identifiers).


### Project Meta Information Code Generation

The result of this module is the generation of a C header file that propagates the project meta information to your C and C++ projects.
For this, the CMake file configuration feature is used on the `version.h.in` header template.

```c
#define @META_PROJECT_ID@_PROJECT_NAME        "@META_PROJECT_NAME@"
#define @META_PROJECT_ID@_PROJECT_DESCRIPTION "@META_PROJECT_DESCRIPTION@"

#define @META_PROJECT_ID@_AUTHOR_ORGANIZATION "@META_AUTHOR_ORGANIZATION@"
#define @META_PROJECT_ID@_AUTHOR_DOMAIN       "@META_AUTHOR_DOMAIN@"
#define @META_PROJECT_ID@_AUTHOR_MAINTAINER   "@META_AUTHOR_MAINTAINER@"

#define @META_PROJECT_ID@_VERSION_MAJOR       "@META_VERSION_MAJOR@"
#define @META_PROJECT_ID@_VERSION_MINOR       "@META_VERSION_MINOR@"
#define @META_PROJECT_ID@_VERSION_PATCH       "@META_VERSION_PATCH@"
#define @META_PROJECT_ID@_VERSION_REVISION    "@META_VERSION_REVISION@"

#define @META_PROJECT_ID@_VERSION             "@META_VERSION@"
#define @META_PROJECT_ID@_NAME_VERSION        "@META_NAME_VERSION@"
```

The template file is configured with the project meta information and the result is stored within the build directory. Beware that this header is stored in a path derived from your project name. You should adopt this as required.

```cmake
# Generate version-header
configure_file(version.h.in ${CMAKE_CURRENT_BINARY_DIR}/include/${META_PROJECT_NAME}/${META_PROJECT_NAME}-version.h)
```

We suggest to deploy this header disregarding its internal or even public use.

```cmake
#
# Deployment
#

# Deploy generated headers
install(DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/include/${META_PROJECT_NAME} DESTINATION include COMPONENT dev)
```


### Project Build Options

## Maintainer Modules

### cmake-init Template Check

This module allows to check the actuality of the used cmake-init template for own projects.
This module is usable when the following is integrated into the `CMakeLists.txt`.

```cmake
# Add cmake-init template check cmake targets
add_check_template_target(<CMAKE_INIT_SHA>)
```

Here, the `<CMAKE_INIT_SHA>` contains the git hash of the used cmake-init template.
Further, the files `cmake/HealthCheck.cmake` and `cmake/CheckTemplate.cmake` are required.

The hash is usually configured using

```cmake
# Meta information about the project
set(META_CMAKE_INIT_SHA      "<CMAKE_INIT_SHA>")

# Add cmake-init template check cmake targets
add_check_template_target(<CMAKE_INIT_SHA>)
```

Correctly configures, this module adds a cmake build target named `check-template` that compares the passed `<CMAKE_INIT_SHA>` with the current master commit hash of this repository and provides a link for a diff view.

## Development Modules

### Version Control System Integration

```cmake
# Get git revision
get_git_head_revision(GIT_REFSPEC GIT_SHA1)
string(SUBSTRING "${GIT_SHA1}" 0 12 GIT_REV)
if(NOT GIT_SHA1)
    set(GIT_REV "0")
endif()
```

### Build Targets

### Documentation

### Tests

### Linter

### Continuous Integration

### Deployment

### Packaging

### Run-time Assets
This is the runtime data folder for your project.

Use it only for data that is needed and loaded at runtime by your application.
It is installed and shipped during packaging of your application.

Other data files such as desktop icons, init scripts, or files needed for packaging,
belong into the deploy directory.

Have a look at the cmake-init documentation to learn how your application is able
to locate its data folder at runtime.

# 
# Target 'pack'
# 

add_custom_target(pack)
set_target_properties(pack PROPERTIES EXCLUDE_FROM_DEFAULT_BUILD 1)


# Install additional runtime dependencies
include(${PROJECT_SOURCE_DIR}/cmake/RuntimeDependencies.cmake)


# 
# Packages
# 

include(packages/pack-${META_PROJECT_NAME}.cmake)


#
# Target 'component_install'
#

add_custom_target(
    component_install
    COMMAND make preinstall
    COMMAND ${CMAKE_COMMAND} -P ${PROJECT_SOURCE_DIR}/cmake/ComponentInstall.cmake
    WORKING_DIRECTORY ${PROJECT_BINARY_DIR}
)

# Deployment Types

## System Install

## Global Install

## Source Build

## Relocatable

# Packages and Installer

## Package Manager

# Components
# git-build-recipe format 0.4 deb-version {debupstream}+{revno}
lp:cmake-init
nest-part packaging lp:cmake-init deploy/ubuntu-ppa/debian debian master

# 
# Target 'docs'
# 

if(NOT OPTION_BUILD_DOCS)
    return()
endif()

add_custom_target(docs)


# 
# Documentation
# 

add_subdirectory(api-docs)
add_subdirectory(manual)

# 
# Find doxygen
# 

find_package(Doxygen)
if(NOT DOXYGEN_FOUND)
    message(STATUS "Disabled generation of doxygen documentation (missing doxygen).")
    return()
endif()


# 
# Target name
# 

set(target api-docs)
message(STATUS "Doc ${target}")


# 
# Input file
# 

set(doxyfile_in doxyfile.in)


# 
# Create documentation
# 

# Set project variables
set(doxyfile            "${CMAKE_CURRENT_BINARY_DIR}/doxyfile")
set(doxyfile_directory  "${CMAKE_CURRENT_BINARY_DIR}/html")
set(doxyfile_html       "${doxyfile_directory}/index.html")

# Get filename and path of doxyfile
get_filename_component(name ${doxyfile_in} NAME)
get_filename_component(path ${doxyfile_in} PATH)
if(NOT path)
    set(path ${CMAKE_CURRENT_SOURCE_DIR})
endif()

# Configure doxyfile (if it is a real doxyfile already, it should simply copy the file)
set(DOXYGEN_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR})
configure_file(${doxyfile_in} ${doxyfile} @ONLY)

# Invoke doxygen
add_custom_command(
    OUTPUT              ${doxyfile_html}
    DEPENDS             ${doxyfile} ${META_PROJECT_NAME}::baselib ${META_PROJECT_NAME}::fiblib
    WORKING_DIRECTORY   ${path}
    COMMAND             ${CMAKE_COMMAND} -E copy_directory ${path} ${doxyfile_directory} # ToDO, configure doxygen to use source as is
    COMMAND             ${DOXYGEN} \"${doxyfile}\"
    COMMENT             "Creating doxygen documentation."
)

# Declare target
add_custom_target(${target} ALL DEPENDS ${doxyfile_html})
add_dependencies(docs ${target})


# 
# Deployment
# 

install(
    DIRECTORY ${doxyfile_directory}
    DESTINATION ${INSTALL_DOC}
    COMPONENT docs
)

# 
# Find LaTeX
# 

find_package(LATEX)
if(NOT LATEX_FOUND)
    message(STATUS "Disabled generation of documentation (missing LaTeX).")
    return()
endif()


# 
# Target name
# 

set(target docs-manual)
message(STATUS "Doc ${target}")


# 
# Input and output files
# 

set(source "${CMAKE_CURRENT_SOURCE_DIR}/cmake-init.tex")
set(pdf    "${CMAKE_CURRENT_BINARY_DIR}/cmake-init.pdf")


# 
# Create documentation
# 

# Invoke LaTeX
add_custom_command(
    OUTPUT            ${pdf}
    DEPENDS           ${source}
    WORKING_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}"
    COMMAND           ${PDFLATEX_COMPILER} \"${source}\"
    COMMAND           ${PDFLATEX_COMPILER} \"${source}\"
    COMMAND           ${PDFLATEX_COMPILER} \"${source}\"
    COMMENT           "Creating LaTeX documentation."
)

# Declare target
add_custom_target(${target} ALL DEPENDS ${pdf})
add_dependencies(docs ${target})


# 
# Deployment
# 

# PDF file
install(FILES ${pdf}
    DESTINATION "${INSTALL_DOC}"
    COMPONENT docs
)

# 
# Configuration for all sub-projects
# 

# Generate version-header
configure_file(version.h.in ${CMAKE_CURRENT_BINARY_DIR}/include/${META_PROJECT_NAME}/${META_PROJECT_NAME}-version.h @ONLY)


# 
# Sub-projects
# 

# Libraries
set(IDE_FOLDER "")
add_subdirectory(baselib)
add_subdirectory(fiblib)

# Examples
set(IDE_FOLDER "Examples")
add_subdirectory(examples)

# Tests
if(OPTION_BUILD_TESTS AND NOT MINGW)
    set(IDE_FOLDER "Tests")
    add_subdirectory(tests)
endif()


# 
# Deployment
# 

# Deploy generated headers
install(DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/include/${META_PROJECT_NAME} DESTINATION include COMPONENT dev)

# Target Types

## Command-line Executable

## GUI Executable

## Flexible Library

## Shared Library

## Static Library

## Plugin

## Header-only Library

## Virtual Library

## CMake-only Library

# Dependencies

# Build Options

# Compiler Features

# Source Code

# Tests

## Testing Systems

## External Testing

# Continuous Integration

# Linter

# 
# External dependencies
# 

# find_package(THIRDPARTY REQUIRED)


# 
# Library name and options
# 

# Target name
set(target baselib)

# Exit here if required dependencies are not met
message(STATUS "Lib ${target}")

# Set API export file and macro
string(MAKE_C_IDENTIFIER ${target} target_id)
string(TOUPPER ${target_id} target_id)
set(feature_file         "include/${target}/${target}_features.h")
set(export_file          "include/${target}/${target}_export.h")
set(template_export_file "include/${target}/${target}_api.h")
set(export_macro         "${target_id}_API")


# 
# Sources
# 

set(include_path "${CMAKE_CURRENT_SOURCE_DIR}/include/${target}")
set(source_path  "${CMAKE_CURRENT_SOURCE_DIR}/source")

set(headers
    ${include_path}/baselib.h
)

set(sources
    ${source_path}/baselib.cpp
)

# Group source files
set(header_group "Header Files (API)")
set(source_group "Source Files")
source_group_by_path(${include_path} "\\\\.h$|\\\\.hpp$" 
    ${header_group} ${headers})
source_group_by_path(${source_path}  "\\\\.cpp$|\\\\.c$|\\\\.h$|\\\\.hpp$" 
    ${source_group} ${sources})


# 
# Create library
# 

# Build library
add_library(${target}
    ${sources}
    ${headers}
)

# Create namespaced alias
add_library(${META_PROJECT_NAME}::${target} ALIAS ${target})

# Export library for downstream projects
export(TARGETS ${target} NAMESPACE ${META_PROJECT_NAME}:: FILE ${PROJECT_BINARY_DIR}/cmake/${target}/${target}-export.cmake)

# Create feature detection header
# Compilers: https://cmake.org/cmake/help/v3.1/variable/CMAKE_LANG_COMPILER_ID.html#variable:CMAKE_%3CLANG%3E_COMPILER_ID
# Feature: https://cmake.org/cmake/help/v3.1/prop_gbl/CMAKE_CXX_KNOWN_FEATURES.html

# Check for availability of module; use pre-generated version if not found
if (WriterCompilerDetectionHeaderFound)
    write_compiler_detection_header(
        FILE ${feature_file}
        PREFIX ${target_id}
        COMPILERS AppleClang Clang GNU MSVC
        FEATURES cxx_alignas cxx_alignof cxx_constexpr cxx_final cxx_noexcept cxx_nullptr cxx_sizeof_member cxx_thread_local
        VERSION 3.2
    )
else()
    file(
        COPY ${PROJECT_SOURCE_DIR}/source/codegeneration/${target}_features.h
        DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/include/${target}
        USE_SOURCE_PERMISSIONS
    )
endif()

# Create API export header
generate_export_header(${target}
    EXPORT_FILE_NAME  ${export_file}
    EXPORT_MACRO_NAME ${export_macro}
)
generate_template_export_header(${target}
    ${target_id}
    ${template_export_file}
)


# 
# Project options
# 

set_target_properties(${target}
    PROPERTIES
    ${DEFAULT_PROJECT_OPTIONS}
    FOLDER "${IDE_FOLDER}"
    VERSION ${META_VERSION}
    SOVERSION ${META_VERSION_MAJOR}
)


# 
# Include directories
# 

target_include_directories(${target}
    PRIVATE
    ${PROJECT_BINARY_DIR}/source/include
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    ${CMAKE_CURRENT_BINARY_DIR}/include

    PUBLIC
    ${DEFAULT_INCLUDE_DIRECTORIES}

    INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}/include>
    $<INSTALL_INTERFACE:include>
)


# 
# Libraries
# 

target_link_libraries(${target}
    PRIVATE

    PUBLIC
    ${DEFAULT_LIBRARIES}

    INTERFACE
)


# 
# Compile definitions
# 

target_compile_definitions(${target}
    PRIVATE

    PUBLIC
    $<$<NOT:$<BOOL:${BUILD_SHARED_LIBS}>>:${target_id}_STATIC_DEFINE>
    ${DEFAULT_COMPILE_DEFINITIONS}

    INTERFACE
)


# 
# Compile options
# 

target_compile_options(${target}
    PRIVATE

    PUBLIC
    ${DEFAULT_COMPILE_OPTIONS}

    INTERFACE
)


# 
# Linker options
# 

target_link_libraries(${target}
    PRIVATE

    PUBLIC
    ${DEFAULT_LINKER_OPTIONS}

    INTERFACE
)


#
# Target Health
#

perform_health_checks(
    ${target}
    ${sources}
    ${headers}
)


# 
# Deployment
# 

# Library
install(TARGETS ${target}
    EXPORT  "${target}-export"            COMPONENT dev
    RUNTIME DESTINATION ${INSTALL_BIN}    COMPONENT runtime
    LIBRARY DESTINATION ${INSTALL_SHARED} COMPONENT runtime
    ARCHIVE DESTINATION ${INSTALL_LIB}    COMPONENT dev
)

# Header files
install(DIRECTORY
    ${CMAKE_CURRENT_SOURCE_DIR}/include/${target} DESTINATION ${INSTALL_INCLUDE}
    COMPONENT dev
)

# Generated header files
install(DIRECTORY
    ${CMAKE_CURRENT_BINARY_DIR}/include/${target} DESTINATION ${INSTALL_INCLUDE}
    COMPONENT dev
)

# CMake config
install(EXPORT ${target}-export
    NAMESPACE   ${META_PROJECT_NAME}::
    DESTINATION ${INSTALL_CMAKE}/${target}
    COMPONENT   dev
)

# Check if examples are enabled
if(NOT OPTION_BUILD_EXAMPLES)
    return()
endif()

# Example applications
add_subdirectory(fibcmd)
add_subdirectory(fibgui)

# 
# External dependencies
# 

# find_package(THIRDPARTY REQUIRED)


# 
# Executable name and options
# 

# Target name
set(target fibcmd)

# Exit here if required dependencies are not met
message(STATUS "Example ${target}")


# 
# Sources
# 

set(sources
    main.cpp
)


# 
# Create executable
# 

# Build executable
add_executable(${target}
    MACOSX_BUNDLE
    ${sources}
)

# Create namespaced alias
add_executable(${META_PROJECT_NAME}::${target} ALIAS ${target})


# 
# Project options
# 

set_target_properties(${target}
    PROPERTIES
    ${DEFAULT_PROJECT_OPTIONS}
    FOLDER "${IDE_FOLDER}"
)


# 
# Include directories
# 

target_include_directories(${target}
    PRIVATE
    ${DEFAULT_INCLUDE_DIRECTORIES}
    ${PROJECT_BINARY_DIR}/source/include
)


# 
# Libraries
# 

target_link_libraries(${target}
    PRIVATE
    ${DEFAULT_LIBRARIES}
    ${META_PROJECT_NAME}::baselib
    ${META_PROJECT_NAME}::fiblib
)


# 
# Compile definitions
# 

target_compile_definitions(${target}
    PRIVATE
    ${DEFAULT_COMPILE_DEFINITIONS}
)


# 
# Compile options
# 

target_compile_options(${target}
    PRIVATE
    ${DEFAULT_COMPILE_OPTIONS}
)


# 
# Linker options
# 

target_link_libraries(${target}
    PRIVATE
    ${DEFAULT_LINKER_OPTIONS}
)


#
# Target Health
#

perform_health_checks(
    ${target}
    ${sources}
)

generate_coverage_report(${target})


# 
# Deployment
# 

# Executable
install(TARGETS ${target}
    RUNTIME DESTINATION ${INSTALL_BIN} COMPONENT examples
    BUNDLE  DESTINATION ${INSTALL_BIN} COMPONENT examples
)

# 
# External dependencies
# 

find_package(Qt5Core    5.1)
find_package(Qt5Gui     5.1)
find_package(Qt5Widgets 5.1)

# Enable automoc
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(AUTOMOC_MOC_OPTIONS PROPERTIES FOLDER CMakeAutomocTargets)
set_property(GLOBAL PROPERTY AUTOMOC_FOLDER CMakeAutomocTargets)

# ENABLE CMP0020: Automatically link Qt executables to qtmain target on Windows.
set_policy(CMP0020 NEW)


# 
# Executable name and options
# 

# Target name
set(target fibgui)

# Exit here if required dependencies are not met
if (NOT Qt5Core_FOUND)
    message(STATUS "Example ${target} skipped: Qt5 not found")
    return()
else()
    message(STATUS "Example ${target}")
endif()


# 
# Sources
# 

set(sources
    main.cpp
    MainWindow.cpp
    MainWindow.h
    MainWindow.ui
)


# 
# Create executable
# 

# Build executable
add_executable(${target}
    MACOSX_BUNDLE
    ${sources}
)

# Create namespaced alias
add_executable(${META_PROJECT_NAME}::${target} ALIAS ${target})


# 
# Project options
# 

set_target_properties(${target}
    PROPERTIES
    ${DEFAULT_PROJECT_OPTIONS}
    FOLDER "${IDE_FOLDER}"
)


# 
# Include directories
# 

target_include_directories(${target}
    PRIVATE
    ${DEFAULT_INCLUDE_DIRECTORIES}
    ${CMAKE_CURRENT_BINARY_DIR}
    ${PROJECT_BINARY_DIR}/source/include
)


# 
# Libraries
# 

target_link_libraries(${target}
    PRIVATE
    ${DEFAULT_LIBRARIES}
    Qt5::Core
    Qt5::Gui
    Qt5::Widgets
    ${META_PROJECT_NAME}::baselib
    ${META_PROJECT_NAME}::fiblib
)


# 
# Compile definitions
# 

target_compile_definitions(${target}
    PRIVATE
    ${DEFAULT_COMPILE_DEFINITIONS}
)


# 
# Compile options
# 

target_compile_options(${target}
    PRIVATE
    ${DEFAULT_COMPILE_OPTIONS}
)


# 
# Linker options
# 

target_link_libraries(${target}
    PRIVATE
    ${DEFAULT_LINKER_OPTIONS}
)


#
# Target Health
#

perform_health_checks(
    ${target}
    ${sources}
)


# 
# Deployment
# 

# Executable
install(TARGETS ${target}
    RUNTIME DESTINATION ${INSTALL_BIN} COMPONENT examples
    BUNDLE  DESTINATION ${INSTALL_BIN} COMPONENT examples
)

# 
# External dependencies
# 

# find_package(THIRDPARTY REQUIRED)


# 
# Library name and options
# 

# Target name
set(target fiblib)

# Exit here if required dependencies are not met
message(STATUS "Lib ${target}")

# Set API export file and macro
string(MAKE_C_IDENTIFIER ${target} target_id)
string(TOUPPER ${target_id} target_id)
set(feature_file         "include/${target}/${target}_features.h")
set(export_file          "include/${target}/${target}_export.h")
set(template_export_file "include/${target}/${target}_api.h")
set(export_macro         "${target_id}_API")


# 
# Sources
# 

set(include_path "${CMAKE_CURRENT_SOURCE_DIR}/include/${target}")
set(source_path  "${CMAKE_CURRENT_SOURCE_DIR}/source")

set(headers
    ${include_path}/CTFibonacci.h
    ${include_path}/CTFibonacci.inl
    ${include_path}/Fibonacci.h
)

set(sources
    ${source_path}/Fibonacci.cpp
)

# Group source files
set(header_group "Header Files (API)")
set(source_group "Source Files")
source_group_by_path(${include_path} "\\\\.h$|\\\\.hpp$" 
    ${header_group} ${headers})
source_group_by_path(${source_path}  "\\\\.cpp$|\\\\.c$|\\\\.h$|\\\\.hpp$" 
    ${source_group} ${sources})


# 
# Create library
# 

# Build library
add_library(${target}
    ${sources}
    ${headers}
)

# Create namespaced alias
add_library(${META_PROJECT_NAME}::${target} ALIAS ${target})

# Export library for downstream projects
export(TARGETS ${target} NAMESPACE ${META_PROJECT_NAME}:: FILE ${PROJECT_BINARY_DIR}/cmake/${target}/${target}-export.cmake)

# Create feature detection header
# Compilers: https://cmake.org/cmake/help/v3.1/variable/CMAKE_LANG_COMPILER_ID.html#variable:CMAKE_%3CLANG%3E_COMPILER_ID
# Feature: https://cmake.org/cmake/help/v3.1/prop_gbl/CMAKE_CXX_KNOWN_FEATURES.html

# Check for availability of module; use pre-generated version if not found
if (WriterCompilerDetectionHeaderFound)
    write_compiler_detection_header(
        FILE ${feature_file}
        PREFIX ${target_id}
        COMPILERS AppleClang Clang GNU MSVC
        FEATURES cxx_alignas cxx_alignof cxx_constexpr cxx_final cxx_noexcept cxx_nullptr cxx_sizeof_member cxx_thread_local
        VERSION 3.2
    )
else()
    file(
        COPY ${PROJECT_SOURCE_DIR}/source/codegeneration/${target}_features.h
        DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/include/${target}
        USE_SOURCE_PERMISSIONS
    )
endif()

# Create API export header
generate_export_header(${target}
    EXPORT_FILE_NAME  ${export_file}
    EXPORT_MACRO_NAME ${export_macro}
)

generate_template_export_header(${target}
    ${target_id}
    ${template_export_file}
)


# 
# Project options
# 

set_target_properties(${target}
    PROPERTIES
    ${DEFAULT_PROJECT_OPTIONS}
    FOLDER "${IDE_FOLDER}"
    VERSION ${META_VERSION}
    SOVERSION ${META_VERSION_MAJOR}
)


# 
# Include directories
# 

target_include_directories(${target}
    PRIVATE
    ${PROJECT_BINARY_DIR}/source/include
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    ${CMAKE_CURRENT_BINARY_DIR}/include

    PUBLIC
    ${DEFAULT_INCLUDE_DIRECTORIES}

    INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}/include>
    $<INSTALL_INTERFACE:include>
)


# 
# Libraries
# 

target_link_libraries(${target}
    PRIVATE

    PUBLIC
    ${DEFAULT_LIBRARIES}

    INTERFACE
)


# 
# Compile definitions
# 

target_compile_definitions(${target}
    PRIVATE

    PUBLIC
    $<$<NOT:$<BOOL:${BUILD_SHARED_LIBS}>>:${target_id}_STATIC_DEFINE>
    ${DEFAULT_COMPILE_DEFINITIONS}

    INTERFACE
)


# 
# Compile options
# 

target_compile_options(${target}
    PRIVATE

    PUBLIC
    ${DEFAULT_COMPILE_OPTIONS}

    INTERFACE
)


# 
# Linker options
# 

target_link_libraries(${target}
    PRIVATE

    PUBLIC
    ${DEFAULT_LINKER_OPTIONS}

    INTERFACE
)


#
# Target Health
#

perform_health_checks(
    ${target}
    ${sources}
    ${headers}
)


# 
# Deployment
# 

# Library
install(TARGETS ${target}
    EXPORT  "${target}-export"            COMPONENT dev
    RUNTIME DESTINATION ${INSTALL_BIN}    COMPONENT runtime
    LIBRARY DESTINATION ${INSTALL_SHARED} COMPONENT runtime
    ARCHIVE DESTINATION ${INSTALL_LIB}    COMPONENT dev
)

# Header files
install(DIRECTORY
    ${CMAKE_CURRENT_SOURCE_DIR}/include/${target} DESTINATION ${INSTALL_INCLUDE}
    COMPONENT dev
)

# Generated header files
install(DIRECTORY
    ${CMAKE_CURRENT_BINARY_DIR}/include/${target} DESTINATION ${INSTALL_INCLUDE}
    COMPONENT dev
)

# CMake config
install(EXPORT ${target}-export
    NAMESPACE   ${META_PROJECT_NAME}::
    DESTINATION ${INSTALL_CMAKE}/${target}
    COMPONENT   dev
)

#
# Configure test project and environment
#

# CMake version
cmake_minimum_required(VERSION 3.0 FATAL_ERROR)

# Meta information about the project
set(META_PROJECT_NAME "template")

# Declare project
project("${META_PROJECT_NAME}-tests" C CXX)

# Set policies
set_policy(CMP0054 NEW) # ENABLE  CMP0054: Only interpret if() arguments as variables or keywords when unquoted.
set_policy(CMP0042 NEW) # ENABLE  CMP0042: MACOSX_RPATH is enabled by default.
set_policy(CMP0063 NEW) # ENABLE  CMP0063: Honor visibility properties for all target types.
set_policy(CMP0037 OLD) # DISABLE CMP0037: Target names should not be reserved and should match a validity pattern.

# Compiler settings and options

if (EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/../../cmake")
    include(${CMAKE_CURRENT_SOURCE_DIR}/../../cmake/CompileOptions.cmake)
    include(${CMAKE_CURRENT_SOURCE_DIR}/../../cmake/Custom.cmake)
    list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/../../cmake")
else()
    include(${CMAKE_CURRENT_SOURCE_DIR}/cmake/CompileOptions.cmake)
    include(${CMAKE_CURRENT_SOURCE_DIR}/cmake/Custom.cmake)
    list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
endif()

# Function: Build test and add command to execute it via target 'test'
function(add_test_without_ctest target)
    add_subdirectory(${target})
    
    if(NOT TARGET ${target})
        return()
    endif()
    
    add_dependencies(test ${target})
    add_custom_command(TARGET test POST_BUILD 
        COMMAND $<TARGET_FILE:${target}> --gtest_output=xml:gtests-${target}.xml
    )

    generate_coverage_report(${target})
endfunction()

# Build gmock
set(gmock_build_tests           OFF CACHE BOOL "")
set(gtest_build_samples         OFF CACHE BOOL "")
set(gtest_build_tests           OFF CACHE BOOL "")
set(gtest_disable_pthreads      OFF CACHE BOOL "")
set(gtest_force_shared_crt      ON  CACHE BOOL "")
set(gtest_hide_internal_symbols OFF CACHE BOOL "")

add_subdirectory(googletest/googlemock)

# Create interface library to link against gmock
add_library(gmock-dev INTERFACE)

target_include_directories(gmock-dev
    SYSTEM INTERFACE
    ${CMAKE_CURRENT_SOURCE_DIR}/googletest/googletest/include
    ${CMAKE_CURRENT_SOURCE_DIR}/googletest/googlemock/include
)

target_link_libraries(gmock-dev
    INTERFACE
    gmock
)


# 
# Target 'test'
# 

add_custom_target(test)
set_target_properties(test PROPERTIES EXCLUDE_FROM_DEFAULT_BUILD 1)


# 
# Tests
# 

add_test_without_ctest(fiblib-test)
## Update googletest and googlemock

After updating, the following changes needs to be applied manually:

* https://github.com/cginternals/cmake-init/commit/6df2e5acd0111ca13f4a54f616a8e9e729f3fedc
* https://github.com/cginternals/cmake-init/commit/da2b52c0b8b47989d779b8285c1a0294a71947ac
* https://github.com/cginternals/cmake-init/commit/f505bef30fe3122d7bd3b8061fcf704fac452d7f
* https://github.com/cginternals/cmake-init/commit/217786a6e8ab1c3a69ab899ec7fba06d5516452a

### Explicit diff

`googletest/googlemock/CMakeLists.txt`

* Add `set(BUILD_SHARED_LIBS OFF)` after the call to `option(BUILD_SHARED_LIBS ...)`
* Add `set(CMAKE_MACOSX_RPATH OFF)` before the calls to `cxx_library(...)`
* Add `set_target_properties(gmock_main PROPERTIES FOLDER "Tests")` after the calls to `cxx_library(...)`
* Add `set_target_properties(gmock      PROPERTIES FOLDER "Tests")` after the calls to `cxx_library(...)`

`googletest/googletest/CMakeLists.txt`

* Add `set(BUILD_SHARED_LIBS OFF)` after the call to `option(BUILD_SHARED_LIBS ...)`
* Add `set(CMAKE_MACOSX_RPATH OFF)` before the calls to `cxx_library(...)`
* Add `set_target_properties(gtest_main PROPERTIES FOLDER "Tests")` after the calls to `cxx_library(...)`
* Add `set_target_properties(gtest      PROPERTIES FOLDER "Tests")` after the calls to `cxx_library(...)`
* Comment out the calls to `install`

# 
# External dependencies
# 

find_package(${META_PROJECT_NAME} REQUIRED HINTS "${CMAKE_CURRENT_SOURCE_DIR}/../../../")

# 
# Executable name and options
# 

# Target name
set(target fiblib-test)
message(STATUS "Test ${target}")


# 
# Sources
# 

set(sources
    main.cpp
    fibonacci_test.cpp
)


# 
# Create executable
# 

# Build executable
add_executable(${target}
    ${sources}
)

# Create namespaced alias
add_executable(${META_PROJECT_NAME}::${target} ALIAS ${target})


# 
# Project options
# 

set_target_properties(${target}
    PROPERTIES
    ${DEFAULT_PROJECT_OPTIONS}
    FOLDER "${IDE_FOLDER}"
)


# 
# Include directories
# 

target_include_directories(${target}
    PRIVATE
    ${DEFAULT_INCLUDE_DIRECTORIES}
    ${PROJECT_BINARY_DIR}/source/include
)


# 
# Libraries
# 

target_link_libraries(${target}
    PRIVATE
    ${DEFAULT_LIBRARIES}
    ${META_PROJECT_NAME}::fiblib
    gmock-dev
)


# 
# Compile definitions
# 

target_compile_definitions(${target}
    PRIVATE
    ${DEFAULT_COMPILE_DEFINITIONS}
)


# 
# Compile options
# 

target_compile_options(${target}
    PRIVATE
    ${DEFAULT_COMPILE_OPTIONS}
)


# 
# Linker options
# 

target_link_libraries(${target}
    PRIVATE
    ${DEFAULT_LINKER_OPTIONS}
)
cmake_minimum_required(VERSION 2.6.4)

if (POLICY CMP0048)
  cmake_policy(SET CMP0048 NEW)
endif (POLICY CMP0048)

project( googletest-distribution )

enable_testing()

include(CMakeDependentOption)
if (CMAKE_VERSION VERSION_LESS 2.8.5)
  set(CMAKE_INSTALL_BINDIR "bin" CACHE STRING "User executables (bin)")
  set(CMAKE_INSTALL_LIBDIR "lib${LIB_SUFFIX}" CACHE STRING "Object code libraries (lib)")
  set(CMAKE_INSTALL_INCLUDEDIR "include" CACHE STRING "C header files (include)")
  mark_as_advanced(CMAKE_INSTALL_BINDIR CMAKE_INSTALL_LIBDIR CMAKE_INSTALL_INCLUDEDIR)
else()
  include(GNUInstallDirs)
endif()

option(BUILD_GTEST "Builds the googletest subproject" OFF)

#Note that googlemock target already builds googletest
option(BUILD_GMOCK "Builds the googlemock subproject" ON)

cmake_dependent_option(INSTALL_GTEST "Enable installation of googletest. (Projects embedding googletest may want to turn this OFF.)" ON "BUILD_GTEST OR BUILD_GMOCK" OFF)
cmake_dependent_option(INSTALL_GMOCK "Enable installation of googlemock. (Projects embedding googlemock may want to turn this OFF.)" ON "BUILD_GMOCK" OFF)

if(BUILD_GMOCK)
  add_subdirectory( googlemock )
elseif(BUILD_GTEST)
  add_subdirectory( googletest )
endif()

# Google Test #

[![Build Status](https://travis-ci.org/google/googletest.svg?branch=master)](https://travis-ci.org/google/googletest)
[![Build status](https://ci.appveyor.com/api/projects/status/4o38plt0xbo1ubc8/branch/master?svg=true)](https://ci.appveyor.com/project/GoogleTestAppVeyor/googletest/branch/master)

Welcome to **Google Test**, Google's C++ test framework!

This repository is a merger of the formerly separate GoogleTest and
GoogleMock projects. These were so closely related that it makes sense to
maintain and release them together.

Please see the project page above for more information as well as the
mailing list for questions, discussions, and development.  There is
also an IRC channel on [OFTC](https://webchat.oftc.net/) (irc.oftc.net) #gtest available.  Please
join us!

Getting started information for **Google Test** is available in the 
[Google Test Primer](googletest/docs/Primer.md) documentation.

**Google Mock** is an extension to Google Test for writing and using C++ mock
classes.  See the separate [Google Mock documentation](googlemock/README.md).

More detailed documentation for googletest (including build instructions) are
in its interior [googletest/README.md](googletest/README.md) file.

## Features ##

  * An [xUnit](https://en.wikipedia.org/wiki/XUnit) test framework.
  * Test discovery.
  * A rich set of assertions.
  * User-defined assertions.
  * Death tests.
  * Fatal and non-fatal failures.
  * Value-parameterized tests.
  * Type-parameterized tests.
  * Various options for running the tests.
  * XML test report generation.

## Platforms ##

Google test has been used on a variety of platforms:

  * Linux
  * Mac OS X
  * Windows
  * Cygwin
  * MinGW
  * Windows Mobile
  * Symbian

## Who Is Using Google Test? ##

In addition to many internal projects at Google, Google Test is also used by
the following notable projects:

  * The [Chromium projects](http://www.chromium.org/) (behind the Chrome
    browser and Chrome OS).
  * The [LLVM](http://llvm.org/) compiler.
  * [Protocol Buffers](https://github.com/google/protobuf), Google's data
    interchange format.
  * The [OpenCV](http://opencv.org/) computer vision library.
  * [tiny-dnn](https://github.com/tiny-dnn/tiny-dnn): header only, dependency-free deep learning framework in C++11.

## Related Open Source Projects ##

[GTest Runner](https://github.com/nholthaus/gtest-runner) is a Qt5 based automated test-runner and Graphical User Interface with powerful features for Windows and Linux platforms.

[Google Test UI](https://github.com/ospector/gtest-gbar) is test runner that runs
your test binary, allows you to track its progress via a progress bar, and
displays a list of test failures. Clicking on one shows failure text. Google
Test UI is written in C#.

[GTest TAP Listener](https://github.com/kinow/gtest-tap-listener) is an event
listener for Google Test that implements the
[TAP protocol](https://en.wikipedia.org/wiki/Test_Anything_Protocol) for test
result output. If your test runner understands TAP, you may find it useful.

[gtest-parallel](https://github.com/google/gtest-parallel) is a test runner that
runs tests from your binary in parallel to provide significant speed-up.

## Requirements ##

Google Test is designed to have fairly minimal requirements to build
and use with your projects, but there are some.  Currently, we support
Linux, Windows, Mac OS X, and Cygwin.  We will also make our best
effort to support other platforms (e.g. Solaris, AIX, and z/OS).
However, since core members of the Google Test project have no access
to these platforms, Google Test may have outstanding issues there.  If
you notice any problems on your platform, please notify
[googletestframework@googlegroups.com](https://groups.google.com/forum/#!forum/googletestframework). Patches for fixing them are
even more welcome!

### Linux Requirements ###

These are the base requirements to build and use Google Test from a source
package (as described below):

  * GNU-compatible Make or gmake
  * POSIX-standard shell
  * POSIX(-2) Regular Expressions (regex.h)
  * A C++98-standard-compliant compiler

### Windows Requirements ###

  * Microsoft Visual C++ 2010 or newer

### Cygwin Requirements ###

  * Cygwin v1.5.25-14 or newer

### Mac OS X Requirements ###

  * Mac OS X v10.4 Tiger or newer
  * Xcode Developer Tools

### Requirements for Contributors ###

We welcome patches.  If you plan to contribute a patch, you need to
build Google Test and its own tests from a git checkout (described
below), which has further requirements:

  * [Python](https://www.python.org/) v2.3 or newer (for running some of
    the tests and re-generating certain source files from templates)
  * [CMake](https://cmake.org/) v2.6.4 or newer

## Regenerating Source Files ##

Some of Google Test's source files are generated from templates (not
in the C++ sense) using a script.
For example, the
file include/gtest/internal/gtest-type-util.h.pump is used to generate
gtest-type-util.h in the same directory.

You don't need to worry about regenerating the source files
unless you need to modify them.  You would then modify the
corresponding `.pump` files and run the '[pump.py](googletest/scripts/pump.py)'
generator script.  See the [Pump Manual](googletest/docs/PumpManual.md).

### Contributing Code ###

We welcome patches.  Please read the
[Developer's Guide](googletest/docs/DevGuide.md)
for how you can contribute. In particular, make sure you have signed
the Contributor License Agreement, or we won't be able to accept the
patch.

Happy testing!
########################################################################
# CMake build script for Google Mock.
#
# To run the tests for Google Mock itself on Linux, use 'make test' or
# ctest.  You can select which tests to run using 'ctest -R regex'.
# For more options, run 'ctest --help'.

# BUILD_SHARED_LIBS is a standard CMake variable, but we declare it here to
# make it prominent in the GUI.
option(BUILD_SHARED_LIBS "Build shared libraries (DLLs)." OFF)
set(BUILD_SHARED_LIBS OFF)

option(gmock_build_tests "Build all of Google Mock's own tests." OFF)

# A directory to find Google Test sources.
if (EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/gtest/CMakeLists.txt")
  set(gtest_dir gtest)
else()
  set(gtest_dir ../googletest)
endif()

# Defines pre_project_set_up_hermetic_build() and set_up_hermetic_build().
include("${gtest_dir}/cmake/hermetic_build.cmake" OPTIONAL)

if (COMMAND pre_project_set_up_hermetic_build)
  # Google Test also calls hermetic setup functions from add_subdirectory,
  # although its changes will not affect things at the current scope.
  pre_project_set_up_hermetic_build()
endif()

########################################################################
#
# Project-wide settings

# Name of the project.
#
# CMake files in this project can refer to the root source directory
# as ${gmock_SOURCE_DIR} and to the root binary directory as
# ${gmock_BINARY_DIR}.
# Language "C" is required for find_package(Threads).
if (CMAKE_VERSION VERSION_LESS 3.0)
  project(gmock CXX C)
else()
  cmake_policy(SET CMP0048 NEW)
  project(gmock VERSION 1.9.0 LANGUAGES CXX C)
endif()
cmake_minimum_required(VERSION 2.6.4)

if (COMMAND set_up_hermetic_build)
  set_up_hermetic_build()
endif()

# Instructs CMake to process Google Test's CMakeLists.txt and add its
# targets to the current scope.  We are placing Google Test's binary
# directory in a subdirectory of our own as VC compilation may break
# if they are the same (the default).
add_subdirectory("${gtest_dir}" "${gmock_BINARY_DIR}/gtest")

# Although Google Test's CMakeLists.txt calls this function, the
# changes there don't affect the current scope.  Therefore we have to
# call it again here.
config_compiler_and_linker()  # from ${gtest_dir}/cmake/internal_utils.cmake

# Adds Google Mock's and Google Test's header directories to the search path.
include_directories("${gmock_SOURCE_DIR}/include"
                    "${gmock_SOURCE_DIR}"
                    "${gtest_SOURCE_DIR}/include"
                    # This directory is needed to build directly from Google
                    # Test sources.
                    "${gtest_SOURCE_DIR}")

# Summary of tuple support for Microsoft Visual Studio:
# Compiler    version(MS)  version(cmake)  Support
# ----------  -----------  --------------  -----------------------------
# <= VS 2010  <= 10        <= 1600         Use Google Tests's own tuple.
# VS 2012     11           1700            std::tr1::tuple + _VARIADIC_MAX=10
# VS 2013     12           1800            std::tr1::tuple
# VS 2015     14           1900            std::tuple
# VS 2017     15           >= 1910         std::tuple
if (MSVC AND MSVC_VERSION EQUAL 1700)
  add_definitions(/D _VARIADIC_MAX=10)
endif()

########################################################################
#
# Defines the gmock & gmock_main libraries.  User tests should link
# with one of them.

set(CMAKE_MACOSX_RPATH OFF)

# Google Mock libraries.  We build them using more strict warnings than what
# are used for other targets, to ensure that Google Mock can be compiled by
# a user aggressive about warnings.
cxx_library(gmock
            "${cxx_strict}"
            "${gtest_dir}/src/gtest-all.cc"
            src/gmock-all.cc)

cxx_library(gmock_main
            "${cxx_strict}"
            "${gtest_dir}/src/gtest-all.cc"
            src/gmock-all.cc
            src/gmock_main.cc)

set_target_properties(gmock_main PROPERTIES FOLDER "Tests")
set_target_properties(gmock      PROPERTIES FOLDER "Tests")

# If the CMake version supports it, attach header directory information
# to the targets for when we are part of a parent build (ie being pulled
# in via add_subdirectory() rather than being a standalone build).
if (DEFINED CMAKE_VERSION AND NOT "${CMAKE_VERSION}" VERSION_LESS "2.8.11")
  target_include_directories(gmock      SYSTEM INTERFACE "${gmock_SOURCE_DIR}/include")
  target_include_directories(gmock_main SYSTEM INTERFACE "${gmock_SOURCE_DIR}/include")
endif()

########################################################################
#
# Install rules
# if(INSTALL_GMOCK)
#   install(TARGETS gmock gmock_main
#     RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
#     LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
#     ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR})
#   install(DIRECTORY ${gmock_SOURCE_DIR}/include/gmock
#     DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

#   # configure and install pkgconfig files
#   configure_file(
#     cmake/gmock.pc.in
#     "${CMAKE_BINARY_DIR}/gmock.pc"
#     @ONLY)
#   configure_file(
#     cmake/gmock_main.pc.in
#     "${CMAKE_BINARY_DIR}/gmock_main.pc"
#     @ONLY)
#   install(FILES "${CMAKE_BINARY_DIR}/gmock.pc" "${CMAKE_BINARY_DIR}/gmock_main.pc"
#     DESTINATION "${CMAKE_INSTALL_LIBDIR}/pkgconfig")
# endif()

########################################################################
#
# Google Mock's own tests.
#
# You can skip this section if you aren't interested in testing
# Google Mock itself.
#
# The tests are not built by default.  To build them, set the
# gmock_build_tests option to ON.  You can do it by running ccmake
# or specifying the -Dgmock_build_tests=ON flag when running cmake.

if (gmock_build_tests)
  # This must be set in the root directory for the tests to be run by
  # 'make test' or ctest.
  enable_testing()

  ############################################################
  # C++ tests built with standard compiler flags.

  cxx_test(gmock-actions_test gmock_main)
  cxx_test(gmock-cardinalities_test gmock_main)
  cxx_test(gmock_ex_test gmock_main)
  cxx_test(gmock-generated-actions_test gmock_main)
  cxx_test(gmock-generated-function-mockers_test gmock_main)
  cxx_test(gmock-generated-internal-utils_test gmock_main)
  cxx_test(gmock-generated-matchers_test gmock_main)
  cxx_test(gmock-internal-utils_test gmock_main)
  cxx_test(gmock-matchers_test gmock_main)
  cxx_test(gmock-more-actions_test gmock_main)
  cxx_test(gmock-nice-strict_test gmock_main)
  cxx_test(gmock-port_test gmock_main)
  cxx_test(gmock-spec-builders_test gmock_main)
  cxx_test(gmock_link_test gmock_main test/gmock_link2_test.cc)
  cxx_test(gmock_test gmock_main)

  if (DEFINED GTEST_HAS_PTHREAD)
    cxx_test(gmock_stress_test gmock)
  endif()

  # gmock_all_test is commented to save time building and running tests.
  # Uncomment if necessary.
  # cxx_test(gmock_all_test gmock_main)

  ############################################################
  # C++ tests built with non-standard compiler flags.

  cxx_library(gmock_main_no_exception "${cxx_no_exception}"
    "${gtest_dir}/src/gtest-all.cc" src/gmock-all.cc src/gmock_main.cc)

  cxx_library(gmock_main_no_rtti "${cxx_no_rtti}"
    "${gtest_dir}/src/gtest-all.cc" src/gmock-all.cc src/gmock_main.cc)

  if (NOT MSVC OR MSVC_VERSION LESS 1600)  # 1600 is Visual Studio 2010.
    # Visual Studio 2010, 2012, and 2013 define symbols in std::tr1 that
    # conflict with our own definitions. Therefore using our own tuple does not
    # work on those compilers.
    cxx_library(gmock_main_use_own_tuple "${cxx_use_own_tuple}"
      "${gtest_dir}/src/gtest-all.cc" src/gmock-all.cc src/gmock_main.cc)

    cxx_test_with_flags(gmock_use_own_tuple_test "${cxx_use_own_tuple}"
      gmock_main_use_own_tuple test/gmock-spec-builders_test.cc)
  endif()

  cxx_test_with_flags(gmock-more-actions_no_exception_test "${cxx_no_exception}"
    gmock_main_no_exception test/gmock-more-actions_test.cc)

  cxx_test_with_flags(gmock_no_rtti_test "${cxx_no_rtti}"
    gmock_main_no_rtti test/gmock-spec-builders_test.cc)

  cxx_shared_library(shared_gmock_main "${cxx_default}"
    "${gtest_dir}/src/gtest-all.cc" src/gmock-all.cc src/gmock_main.cc)

  # Tests that a binary can be built with Google Mock as a shared library.  On
  # some system configurations, it may not possible to run the binary without
  # knowing more details about the system configurations. We do not try to run
  # this binary. To get a more robust shared library coverage, configure with
  # -DBUILD_SHARED_LIBS=ON.
  cxx_executable_with_flags(shared_gmock_test_ "${cxx_default}"
    shared_gmock_main test/gmock-spec-builders_test.cc)
  set_target_properties(shared_gmock_test_
    PROPERTIES
    COMPILE_DEFINITIONS "GTEST_LINKED_AS_SHARED_LIBRARY=1")

  ############################################################
  # Python tests.

  cxx_executable(gmock_leak_test_ test gmock_main)
  py_test(gmock_leak_test)

  cxx_executable(gmock_output_test_ test gmock)
  py_test(gmock_output_test)
endif()
Copyright 2008, Google Inc.
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are
met:

    * Redistributions of source code must retain the above copyright
notice, this list of conditions and the following disclaimer.
    * Redistributions in binary form must reproduce the above
copyright notice, this list of conditions and the following disclaimer
in the documentation and/or other materials provided with the
distribution.
    * Neither the name of Google Inc. nor the names of its
contributors may be used to endorse or promote products derived from
this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
"AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
## Google Mock ##

The Google C++ mocking framework.

### Overview ###

Google's framework for writing and using C++ mock classes.
It can help you derive better designs of your system and write better tests.

It is inspired by:

  * [jMock](http://www.jmock.org/),
  * [EasyMock](http://www.easymock.org/), and
  * [Hamcrest](http://code.google.com/p/hamcrest/),

and designed with C++'s specifics in mind.

Google mock:

  * lets you create mock classes trivially using simple macros.
  * supports a rich set of matchers and actions.
  * handles unordered, partially ordered, or completely ordered expectations.
  * is extensible by users.

We hope you find it useful!

### Features ###

  * Provides a declarative syntax for defining mocks.
  * Can easily define partial (hybrid) mocks, which are a cross of real
    and mock objects.
  * Handles functions of arbitrary types and overloaded functions.
  * Comes with a rich set of matchers for validating function arguments.
  * Uses an intuitive syntax for controlling the behavior of a mock.
  * Does automatic verification of expectations (no record-and-replay needed).
  * Allows arbitrary (partial) ordering constraints on
    function calls to be expressed,.
  * Lets an user extend it by defining new matchers and actions.
  * Does not use exceptions.
  * Is easy to learn and use.

Please see the project page above for more information as well as the
mailing list for questions, discussions, and development.  There is
also an IRC channel on OFTC (irc.oftc.net) #gtest available.  Please
join us!

Please note that code under [scripts/generator](scripts/generator/) is
from [cppclean](http://code.google.com/p/cppclean/) and released under
the Apache License, which is different from Google Mock's license.

## Getting Started ##

If you are new to the project, we suggest that you read the user
documentation in the following order:

  * Learn the [basics](../../master/googletest/docs/Primer.md) of
    Google Test, if you choose to use Google Mock with it (recommended).
  * Read [Google Mock for Dummies](../../master/googlemock/docs/ForDummies.md).
  * Read the instructions below on how to build Google Mock.

You can also watch Zhanyong's [talk](http://www.youtube.com/watch?v=sYpCyLI47rM) on Google Mock's usage and implementation.

Once you understand the basics, check out the rest of the docs:

  * [CheatSheet](../../master/googlemock/docs/CheatSheet.md) - all the commonly used stuff
    at a glance.
  * [CookBook](../../master/googlemock/docs/CookBook.md) - recipes for getting things done,
    including advanced techniques.

If you need help, please check the
[KnownIssues](docs/KnownIssues.md) and
[FrequentlyAskedQuestions](docs/FrequentlyAskedQuestions.md) before
posting a question on the
[discussion group](http://groups.google.com/group/googlemock).


### Using Google Mock Without Google Test ###

Google Mock is not a testing framework itself.  Instead, it needs a
testing framework for writing tests.  Google Mock works seamlessly
with [Google Test](https://github.com/google/googletest), but
you can also use it with [any C++ testing framework](../../master/googlemock/docs/ForDummies.md#using-google-mock-with-any-testing-framework).

### Requirements for End Users ###

Google Mock is implemented on top of [Google Test](
http://github.com/google/googletest/), and depends on it.
You must use the bundled version of Google Test when using Google Mock.

You can also easily configure Google Mock to work with another testing
framework, although it will still need Google Test.  Please read
["Using_Google_Mock_with_Any_Testing_Framework"](
    ../../master/googlemock/docs/ForDummies.md#using-google-mock-with-any-testing-framework)
for instructions.

Google Mock depends on advanced C++ features and thus requires a more
modern compiler. The following are needed to use Google Mock:

#### Linux Requirements ####

  * GNU-compatible Make or "gmake"
  * POSIX-standard shell
  * POSIX(-2) Regular Expressions (regex.h)
  * C++98-standard-compliant compiler (e.g. GCC 3.4 or newer)

#### Windows Requirements ####

  * Microsoft Visual C++ 8.0 SP1 or newer

#### Mac OS X Requirements ####

  * Mac OS X 10.4 Tiger or newer
  * Developer Tools Installed

### Requirements for Contributors ###

We welcome patches. If you plan to contribute a patch, you need to
build Google Mock and its tests, which has further requirements:

  * Automake version 1.9 or newer
  * Autoconf version 2.59 or newer
  * Libtool / Libtoolize
  * Python version 2.3 or newer (for running some of the tests and
    re-generating certain source files from templates)

### Building Google Mock ###

#### Using CMake ####

If you have CMake available, it is recommended that you follow the
[build instructions][gtest_cmakebuild]
as described for Google Test. 

If are using Google Mock with an
existing CMake project, the section
[Incorporating Into An Existing CMake Project][gtest_incorpcmake]
may be of particular interest. 
To make it work for Google Mock you will need to change 

    target_link_libraries(example gtest_main)

to 

    target_link_libraries(example gmock_main)
    
This works because `gmock_main` library is compiled with Google Test.
However, it does not automatically add Google Test includes.
Therefore you will also have to change

    if (CMAKE_VERSION VERSION_LESS 2.8.11)
      include_directories("${gtest_SOURCE_DIR}/include")
    endif()

to

    if (CMAKE_VERSION VERSION_LESS 2.8.11)
      include_directories(BEFORE SYSTEM
        "${gtest_SOURCE_DIR}/include" "${gmock_SOURCE_DIR}/include")
    else()
      target_include_directories(gmock_main SYSTEM BEFORE INTERFACE
        "${gtest_SOURCE_DIR}/include" "${gmock_SOURCE_DIR}/include")
    endif()

This will addtionally mark Google Mock includes as system, which will 
silence compiler warnings when compiling your tests using clang with 
`-Wpedantic -Wall -Wextra -Wconversion`.


#### Preparing to Build (Unix only) ####

If you are using a Unix system and plan to use the GNU Autotools build
system to build Google Mock (described below), you'll need to
configure it now.

To prepare the Autotools build system:

    cd googlemock
    autoreconf -fvi

To build Google Mock and your tests that use it, you need to tell your
build system where to find its headers and source files.  The exact
way to do it depends on which build system you use, and is usually
straightforward.

This section shows how you can integrate Google Mock into your
existing build system.

Suppose you put Google Mock in directory `${GMOCK_DIR}` and Google Test
in `${GTEST_DIR}` (the latter is `${GMOCK_DIR}/gtest` by default).  To
build Google Mock, create a library build target (or a project as
called by Visual Studio and Xcode) to compile

    ${GTEST_DIR}/src/gtest-all.cc and ${GMOCK_DIR}/src/gmock-all.cc

with

    ${GTEST_DIR}/include and ${GMOCK_DIR}/include

in the system header search path, and

    ${GTEST_DIR} and ${GMOCK_DIR}

in the normal header search path.  Assuming a Linux-like system and gcc,
something like the following will do:

    g++ -isystem ${GTEST_DIR}/include -I${GTEST_DIR} \
        -isystem ${GMOCK_DIR}/include -I${GMOCK_DIR} \
        -pthread -c ${GTEST_DIR}/src/gtest-all.cc
    g++ -isystem ${GTEST_DIR}/include -I${GTEST_DIR} \
        -isystem ${GMOCK_DIR}/include -I${GMOCK_DIR} \
        -pthread -c ${GMOCK_DIR}/src/gmock-all.cc
    ar -rv libgmock.a gtest-all.o gmock-all.o

(We need -pthread as Google Test and Google Mock use threads.)

Next, you should compile your test source file with
${GTEST\_DIR}/include and ${GMOCK\_DIR}/include in the header search
path, and link it with gmock and any other necessary libraries:

    g++ -isystem ${GTEST_DIR}/include -isystem ${GMOCK_DIR}/include \
        -pthread path/to/your_test.cc libgmock.a -o your_test

As an example, the make/ directory contains a Makefile that you can
use to build Google Mock on systems where GNU make is available
(e.g. Linux, Mac OS X, and Cygwin).  It doesn't try to build Google
Mock's own tests.  Instead, it just builds the Google Mock library and
a sample test.  You can use it as a starting point for your own build
script.

If the default settings are correct for your environment, the
following commands should succeed:

    cd ${GMOCK_DIR}/make
    make
    ./gmock_test

If you see errors, try to tweak the contents of
[make/Makefile](make/Makefile) to make them go away.

### Windows ###

The msvc/2005 directory contains VC++ 2005 projects and the msvc/2010
directory contains VC++ 2010 projects for building Google Mock and
selected tests.

Change to the appropriate directory and run "msbuild gmock.sln" to
build the library and tests (or open the gmock.sln in the MSVC IDE).
If you want to create your own project to use with Google Mock, you'll
have to configure it to use the `gmock_config` propety sheet.  For that:

 * Open the Property Manager window (View | Other Windows | Property Manager)
 * Right-click on your project and select "Add Existing Property Sheet..."
 * Navigate to `gmock_config.vsprops` or `gmock_config.props` and select it.
 * In Project Properties | Configuration Properties | General | Additional
   Include Directories, type <path to Google Mock>/include.

### Tweaking Google Mock ###

Google Mock can be used in diverse environments.  The default
configuration may not work (or may not work well) out of the box in
some environments.  However, you can easily tweak Google Mock by
defining control macros on the compiler command line.  Generally,
these macros are named like `GTEST_XYZ` and you define them to either 1
or 0 to enable or disable a certain feature.

We list the most frequently used macros below.  For a complete list,
see file [${GTEST\_DIR}/include/gtest/internal/gtest-port.h](
../googletest/include/gtest/internal/gtest-port.h).

### Choosing a TR1 Tuple Library ###

Google Mock uses the C++ Technical Report 1 (TR1) tuple library
heavily.  Unfortunately TR1 tuple is not yet widely available with all
compilers.  The good news is that Google Test 1.4.0+ implements a
subset of TR1 tuple that's enough for Google Mock's need.  Google Mock
will automatically use that implementation when the compiler doesn't
provide TR1 tuple.

Usually you don't need to care about which tuple library Google Test
and Google Mock use.  However, if your project already uses TR1 tuple,
you need to tell Google Test and Google Mock to use the same TR1 tuple
library the rest of your project uses, or the two tuple
implementations will clash.  To do that, add

    -DGTEST_USE_OWN_TR1_TUPLE=0

to the compiler flags while compiling Google Test, Google Mock, and
your tests.  If you want to force Google Test and Google Mock to use
their own tuple library, just add

    -DGTEST_USE_OWN_TR1_TUPLE=1

to the compiler flags instead.

If you want to use Boost's TR1 tuple library with Google Mock, please
refer to the Boost website (http://www.boost.org/) for how to obtain
it and set it up.

### As a Shared Library (DLL) ###

Google Mock is compact, so most users can build and link it as a static
library for the simplicity.  Google Mock can be used as a DLL, but the
same DLL must contain Google Test as well.  See
[Google Test's README][gtest_readme]
for instructions on how to set up necessary compiler settings.

### Tweaking Google Mock ###

Most of Google Test's control macros apply to Google Mock as well.
Please see [Google Test's README][gtest_readme] for how to tweak them.

### Upgrading from an Earlier Version ###

We strive to keep Google Mock releases backward compatible.
Sometimes, though, we have to make some breaking changes for the
users' long-term benefits.  This section describes what you'll need to
do if you are upgrading from an earlier version of Google Mock.

#### Upgrading from 1.1.0 or Earlier ####

You may need to explicitly enable or disable Google Test's own TR1
tuple library.  See the instructions in section "[Choosing a TR1 Tuple
Library](../googletest/#choosing-a-tr1-tuple-library)".

#### Upgrading from 1.4.0 or Earlier ####

On platforms where the pthread library is available, Google Test and
Google Mock use it in order to be thread-safe.  For this to work, you
may need to tweak your compiler and/or linker flags.  Please see the
"[Multi-threaded Tests](../googletest#multi-threaded-tests
)" section in file Google Test's README for what you may need to do.

If you have custom matchers defined using `MatcherInterface` or
`MakePolymorphicMatcher()`, you'll need to update their definitions to
use the new matcher API (
[monomorphic](./docs/CookBook.md#writing-new-monomorphic-matchers),
[polymorphic](./docs/CookBook.md#writing-new-polymorphic-matchers)).
Matchers defined using `MATCHER()` or `MATCHER_P*()` aren't affected.

### Developing Google Mock ###

This section discusses how to make your own changes to Google Mock.

#### Testing Google Mock Itself ####

To make sure your changes work as intended and don't break existing
functionality, you'll want to compile and run Google Test's own tests.
For that you'll need Autotools.  First, make sure you have followed
the instructions above to configure Google Mock.
Then, create a build output directory and enter it.  Next,

    ${GMOCK_DIR}/configure  # try --help for more info

Once you have successfully configured Google Mock, the build steps are
standard for GNU-style OSS packages.

    make        # Standard makefile following GNU conventions
    make check  # Builds and runs all tests - all should pass.

Note that when building your project against Google Mock, you are building
against Google Test as well.  There is no need to configure Google Test
separately.

#### Contributing a Patch ####

We welcome patches.
Please read the [Developer's Guide](docs/DevGuide.md)
for how you can contribute. In particular, make sure you have signed
the Contributor License Agreement, or we won't be able to accept the
patch.

Happy testing!

[gtest_readme]: ../googletest/README.md "googletest"
[gtest_cmakebuild]:  ../googletest/README.md#using-cmake "Using CMake"
[gtest_incorpcmake]: ../googletest/README.md#incorporating-into-an-existing-cmake-project "Incorporating Into An Existing CMake Project"


# Defining a Mock Class #

## Mocking a Normal Class ##

Given
```
class Foo {
  ...
  virtual ~Foo();
  virtual int GetSize() const = 0;
  virtual string Describe(const char* name) = 0;
  virtual string Describe(int type) = 0;
  virtual bool Process(Bar elem, int count) = 0;
};
```
(note that `~Foo()` **must** be virtual) we can define its mock as
```
#include "gmock/gmock.h"

class MockFoo : public Foo {
  MOCK_CONST_METHOD0(GetSize, int());
  MOCK_METHOD1(Describe, string(const char* name));
  MOCK_METHOD1(Describe, string(int type));
  MOCK_METHOD2(Process, bool(Bar elem, int count));
};
```

To create a "nice" mock object which ignores all uninteresting calls,
or a "strict" mock object, which treats them as failures:
```
NiceMock<MockFoo> nice_foo;     // The type is a subclass of MockFoo.
StrictMock<MockFoo> strict_foo; // The type is a subclass of MockFoo.
```

## Mocking a Class Template ##

To mock
```
template <typename Elem>
class StackInterface {
 public:
  ...
  virtual ~StackInterface();
  virtual int GetSize() const = 0;
  virtual void Push(const Elem& x) = 0;
};
```
(note that `~StackInterface()` **must** be virtual) just append `_T` to the `MOCK_*` macros:
```
template <typename Elem>
class MockStack : public StackInterface<Elem> {
 public:
  ...
  MOCK_CONST_METHOD0_T(GetSize, int());
  MOCK_METHOD1_T(Push, void(const Elem& x));
};
```

## Specifying Calling Conventions for Mock Functions ##

If your mock function doesn't use the default calling convention, you
can specify it by appending `_WITH_CALLTYPE` to any of the macros
described in the previous two sections and supplying the calling
convention as the first argument to the macro. For example,
```
  MOCK_METHOD1_WITH_CALLTYPE(STDMETHODCALLTYPE, Foo, bool(int n));
  MOCK_CONST_METHOD2_WITH_CALLTYPE(STDMETHODCALLTYPE, Bar, int(double x, double y));
```
where `STDMETHODCALLTYPE` is defined by `<objbase.h>` on Windows.

# Using Mocks in Tests #

The typical flow is:
  1. Import the Google Mock names you need to use. All Google Mock names are in the `testing` namespace unless they are macros or otherwise noted.
  1. Create the mock objects.
  1. Optionally, set the default actions of the mock objects.
  1. Set your expectations on the mock objects (How will they be called? What wil they do?).
  1. Exercise code that uses the mock objects; if necessary, check the result using [Google Test](../../googletest/) assertions.
  1. When a mock objects is destructed, Google Mock automatically verifies that all expectations on it have been satisfied.

Here is an example:
```
using ::testing::Return;                            // #1

TEST(BarTest, DoesThis) {
  MockFoo foo;                                    // #2

  ON_CALL(foo, GetSize())                         // #3
      .WillByDefault(Return(1));
  // ... other default actions ...

  EXPECT_CALL(foo, Describe(5))                   // #4
      .Times(3)
      .WillRepeatedly(Return("Category 5"));
  // ... other expectations ...

  EXPECT_EQ("good", MyProductionFunction(&foo));  // #5
}                                                 // #6
```

# Setting Default Actions #

Google Mock has a **built-in default action** for any function that
returns `void`, `bool`, a numeric value, or a pointer.

To customize the default action for functions with return type `T` globally:
```
using ::testing::DefaultValue;

// Sets the default value to be returned. T must be CopyConstructible.
DefaultValue<T>::Set(value);
// Sets a factory. Will be invoked on demand. T must be MoveConstructible.
//   T MakeT();
DefaultValue<T>::SetFactory(&MakeT);
// ... use the mocks ...
// Resets the default value.
DefaultValue<T>::Clear();
```

To customize the default action for a particular method, use `ON_CALL()`:
```
ON_CALL(mock_object, method(matchers))
    .With(multi_argument_matcher)  ?
    .WillByDefault(action);
```

# Setting Expectations #

`EXPECT_CALL()` sets **expectations** on a mock method (How will it be
called? What will it do?):
```
EXPECT_CALL(mock_object, method(matchers))
    .With(multi_argument_matcher)  ?
    .Times(cardinality)            ?
    .InSequence(sequences)         *
    .After(expectations)           *
    .WillOnce(action)              *
    .WillRepeatedly(action)        ?
    .RetiresOnSaturation();        ?
```

If `Times()` is omitted, the cardinality is assumed to be:

  * `Times(1)` when there is neither `WillOnce()` nor `WillRepeatedly()`;
  * `Times(n)` when there are `n WillOnce()`s but no `WillRepeatedly()`, where `n` >= 1; or
  * `Times(AtLeast(n))` when there are `n WillOnce()`s and a `WillRepeatedly()`, where `n` >= 0.

A method with no `EXPECT_CALL()` is free to be invoked _any number of times_, and the default action will be taken each time.

# Matchers #

A **matcher** matches a _single_ argument.  You can use it inside
`ON_CALL()` or `EXPECT_CALL()`, or use it to validate a value
directly:

| `EXPECT_THAT(value, matcher)` | Asserts that `value` matches `matcher`. |
|:------------------------------|:----------------------------------------|
| `ASSERT_THAT(value, matcher)` | The same as `EXPECT_THAT(value, matcher)`, except that it generates a **fatal** failure. |

Built-in matchers (where `argument` is the function argument) are
divided into several categories:

## Wildcard ##
|`_`|`argument` can be any value of the correct type.|
|:--|:-----------------------------------------------|
|`A<type>()` or `An<type>()`|`argument` can be any value of type `type`.     |

## Generic Comparison ##

|`Eq(value)` or `value`|`argument == value`|
|:---------------------|:------------------|
|`Ge(value)`           |`argument >= value`|
|`Gt(value)`           |`argument > value` |
|`Le(value)`           |`argument <= value`|
|`Lt(value)`           |`argument < value` |
|`Ne(value)`           |`argument != value`|
|`IsNull()`            |`argument` is a `NULL` pointer (raw or smart).|
|`NotNull()`           |`argument` is a non-null pointer (raw or smart).|
|`Ref(variable)`       |`argument` is a reference to `variable`.|
|`TypedEq<type>(value)`|`argument` has type `type` and is equal to `value`. You may need to use this instead of `Eq(value)` when the mock function is overloaded.|

Except `Ref()`, these matchers make a _copy_ of `value` in case it's
modified or destructed later. If the compiler complains that `value`
doesn't have a public copy constructor, try wrap it in `ByRef()`,
e.g. `Eq(ByRef(non_copyable_value))`. If you do that, make sure
`non_copyable_value` is not changed afterwards, or the meaning of your
matcher will be changed.

## Floating-Point Matchers ##

|`DoubleEq(a_double)`|`argument` is a `double` value approximately equal to `a_double`, treating two NaNs as unequal.|
|:-------------------|:----------------------------------------------------------------------------------------------|
|`FloatEq(a_float)`  |`argument` is a `float` value approximately equal to `a_float`, treating two NaNs as unequal.  |
|`NanSensitiveDoubleEq(a_double)`|`argument` is a `double` value approximately equal to `a_double`, treating two NaNs as equal.  |
|`NanSensitiveFloatEq(a_float)`|`argument` is a `float` value approximately equal to `a_float`, treating two NaNs as equal.    |

The above matchers use ULP-based comparison (the same as used in
[Google Test](../../googletest/)). They
automatically pick a reasonable error bound based on the absolute
value of the expected value.  `DoubleEq()` and `FloatEq()` conform to
the IEEE standard, which requires comparing two NaNs for equality to
return false. The `NanSensitive*` version instead treats two NaNs as
equal, which is often what a user wants.

|`DoubleNear(a_double, max_abs_error)`|`argument` is a `double` value close to `a_double` (absolute error <= `max_abs_error`), treating two NaNs as unequal.|
|:------------------------------------|:--------------------------------------------------------------------------------------------------------------------|
|`FloatNear(a_float, max_abs_error)`  |`argument` is a `float` value close to `a_float` (absolute error <= `max_abs_error`), treating two NaNs as unequal.  |
|`NanSensitiveDoubleNear(a_double, max_abs_error)`|`argument` is a `double` value close to `a_double` (absolute error <= `max_abs_error`), treating two NaNs as equal.  |
|`NanSensitiveFloatNear(a_float, max_abs_error)`|`argument` is a `float` value close to `a_float` (absolute error <= `max_abs_error`), treating two NaNs as equal.    |

## String Matchers ##

The `argument` can be either a C string or a C++ string object:

|`ContainsRegex(string)`|`argument` matches the given regular expression.|
|:----------------------|:-----------------------------------------------|
|`EndsWith(suffix)`     |`argument` ends with string `suffix`.           |
|`HasSubstr(string)`    |`argument` contains `string` as a sub-string.   |
|`MatchesRegex(string)` |`argument` matches the given regular expression with the match starting at the first character and ending at the last character.|
|`StartsWith(prefix)`   |`argument` starts with string `prefix`.         |
|`StrCaseEq(string)`    |`argument` is equal to `string`, ignoring case. |
|`StrCaseNe(string)`    |`argument` is not equal to `string`, ignoring case.|
|`StrEq(string)`        |`argument` is equal to `string`.                |
|`StrNe(string)`        |`argument` is not equal to `string`.            |

`ContainsRegex()` and `MatchesRegex()` use the regular expression
syntax defined
[here](../../googletest/docs/AdvancedGuide.md#regular-expression-syntax).
`StrCaseEq()`, `StrCaseNe()`, `StrEq()`, and `StrNe()` work for wide
strings as well.

## Container Matchers ##

Most STL-style containers support `==`, so you can use
`Eq(expected_container)` or simply `expected_container` to match a
container exactly.   If you want to write the elements in-line,
match them more flexibly, or get more informative messages, you can use:

| `ContainerEq(container)` | The same as `Eq(container)` except that the failure message also includes which elements are in one container but not the other. |
|:-------------------------|:---------------------------------------------------------------------------------------------------------------------------------|
| `Contains(e)`            | `argument` contains an element that matches `e`, which can be either a value or a matcher.                                       |
| `Each(e)`                | `argument` is a container where _every_ element matches `e`, which can be either a value or a matcher.                           |
| `ElementsAre(e0, e1, ..., en)` | `argument` has `n + 1` elements, where the i-th element matches `ei`, which can be a value or a matcher. 0 to 10 arguments are allowed. |
| `ElementsAreArray({ e0, e1, ..., en })`, `ElementsAreArray(array)`, or `ElementsAreArray(array, count)` | The same as `ElementsAre()` except that the expected element values/matchers come from an initializer list, STL-style container, or C-style array. |
| `IsEmpty()`              | `argument` is an empty container (`container.empty()`).                                                                          |
| `Pointwise(m, container)` | `argument` contains the same number of elements as in `container`, and for all i, (the i-th element in `argument`, the i-th element in `container`) match `m`, which is a matcher on 2-tuples. E.g. `Pointwise(Le(), upper_bounds)` verifies that each element in `argument` doesn't exceed the corresponding element in `upper_bounds`. See more detail below. |
| `SizeIs(m)`              | `argument` is a container whose size matches `m`. E.g. `SizeIs(2)` or `SizeIs(Lt(2))`.                                           |
| `UnorderedElementsAre(e0, e1, ..., en)` | `argument` has `n + 1` elements, and under some permutation each element matches an `ei` (for a different `i`), which can be a value or a matcher. 0 to 10 arguments are allowed. |
| `UnorderedElementsAreArray({ e0, e1, ..., en })`, `UnorderedElementsAreArray(array)`, or `UnorderedElementsAreArray(array, count)` | The same as `UnorderedElementsAre()` except that the expected element values/matchers come from an initializer list, STL-style container, or C-style array. |
| `WhenSorted(m)`          | When `argument` is sorted using the `<` operator, it matches container matcher `m`. E.g. `WhenSorted(ElementsAre(1, 2, 3))` verifies that `argument` contains elements `1`, `2`, and `3`, ignoring order. |
| `WhenSortedBy(comparator, m)` | The same as `WhenSorted(m)`, except that the given comparator instead of `<` is used to sort `argument`. E.g. `WhenSortedBy(std::greater<int>(), ElementsAre(3, 2, 1))`. |

Notes:

  * These matchers can also match:
    1. a native array passed by reference (e.g. in `Foo(const int (&a)[5])`), and
    1. an array passed as a pointer and a count (e.g. in `Bar(const T* buffer, int len)` -- see [Multi-argument Matchers](#Multiargument_Matchers.md)).
  * The array being matched may be multi-dimensional (i.e. its elements can be arrays).
  * `m` in `Pointwise(m, ...)` should be a matcher for `::testing::tuple<T, U>` where `T` and `U` are the element type of the actual container and the expected container, respectively. For example, to compare two `Foo` containers where `Foo` doesn't support `operator==` but has an `Equals()` method, one might write:

```
using ::testing::get;
MATCHER(FooEq, "") {
  return get<0>(arg).Equals(get<1>(arg));
}
...
EXPECT_THAT(actual_foos, Pointwise(FooEq(), expected_foos));
```

## Member Matchers ##

|`Field(&class::field, m)`|`argument.field` (or `argument->field` when `argument` is a plain pointer) matches matcher `m`, where `argument` is an object of type _class_.|
|:------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------|
|`Key(e)`                 |`argument.first` matches `e`, which can be either a value or a matcher. E.g. `Contains(Key(Le(5)))` can verify that a `map` contains a key `<= 5`.|
|`Pair(m1, m2)`           |`argument` is an `std::pair` whose `first` field matches `m1` and `second` field matches `m2`.                                                |
|`Property(&class::property, m)`|`argument.property()` (or `argument->property()` when `argument` is a plain pointer) matches matcher `m`, where `argument` is an object of type _class_.|

## Matching the Result of a Function or Functor ##

|`ResultOf(f, m)`|`f(argument)` matches matcher `m`, where `f` is a function or functor.|
|:---------------|:---------------------------------------------------------------------|

## Pointer Matchers ##

|`Pointee(m)`|`argument` (either a smart pointer or a raw pointer) points to a value that matches matcher `m`.|
|:-----------|:-----------------------------------------------------------------------------------------------|
|`WhenDynamicCastTo<T>(m)`| when `argument` is passed through `dynamic_cast<T>()`, it matches matcher `m`.                 |

## Multiargument Matchers ##

Technically, all matchers match a _single_ value. A "multi-argument"
matcher is just one that matches a _tuple_. The following matchers can
be used to match a tuple `(x, y)`:

|`Eq()`|`x == y`|
|:-----|:-------|
|`Ge()`|`x >= y`|
|`Gt()`|`x > y` |
|`Le()`|`x <= y`|
|`Lt()`|`x < y` |
|`Ne()`|`x != y`|

You can use the following selectors to pick a subset of the arguments
(or reorder them) to participate in the matching:

|`AllArgs(m)`|Equivalent to `m`. Useful as syntactic sugar in `.With(AllArgs(m))`.|
|:-----------|:-------------------------------------------------------------------|
|`Args<N1, N2, ..., Nk>(m)`|The tuple of the `k` selected (using 0-based indices) arguments matches `m`, e.g. `Args<1, 2>(Eq())`.|

## Composite Matchers ##

You can make a matcher from one or more other matchers:

|`AllOf(m1, m2, ..., mn)`|`argument` matches all of the matchers `m1` to `mn`.|
|:-----------------------|:---------------------------------------------------|
|`AnyOf(m1, m2, ..., mn)`|`argument` matches at least one of the matchers `m1` to `mn`.|
|`Not(m)`                |`argument` doesn't match matcher `m`.               |

## Adapters for Matchers ##

|`MatcherCast<T>(m)`|casts matcher `m` to type `Matcher<T>`.|
|:------------------|:--------------------------------------|
|`SafeMatcherCast<T>(m)`| [safely casts](CookBook.md#casting-matchers) matcher `m` to type `Matcher<T>`. |
|`Truly(predicate)` |`predicate(argument)` returns something considered by C++ to be true, where `predicate` is a function or functor.|

## Matchers as Predicates ##

|`Matches(m)(value)`|evaluates to `true` if `value` matches `m`. You can use `Matches(m)` alone as a unary functor.|
|:------------------|:---------------------------------------------------------------------------------------------|
|`ExplainMatchResult(m, value, result_listener)`|evaluates to `true` if `value` matches `m`, explaining the result to `result_listener`.       |
|`Value(value, m)`  |evaluates to `true` if `value` matches `m`.                                                   |

## Defining Matchers ##

| `MATCHER(IsEven, "") { return (arg % 2) == 0; }` | Defines a matcher `IsEven()` to match an even number. |
|:-------------------------------------------------|:------------------------------------------------------|
| `MATCHER_P(IsDivisibleBy, n, "") { *result_listener << "where the remainder is " << (arg % n); return (arg % n) == 0; }` | Defines a macher `IsDivisibleBy(n)` to match a number divisible by `n`. |
| `MATCHER_P2(IsBetween, a, b, std::string(negation ? "isn't" : "is") + " between " + PrintToString(a) + " and " + PrintToString(b)) { return a <= arg && arg <= b; }` | Defines a matcher `IsBetween(a, b)` to match a value in the range [`a`, `b`]. |

**Notes:**

  1. The `MATCHER*` macros cannot be used inside a function or class.
  1. The matcher body must be _purely functional_ (i.e. it cannot have any side effect, and the result must not depend on anything other than the value being matched and the matcher parameters).
  1. You can use `PrintToString(x)` to convert a value `x` of any type to a string.

## Matchers as Test Assertions ##

|`ASSERT_THAT(expression, m)`|Generates a [fatal failure](../../googletest/docs/Primer.md#assertions) if the value of `expression` doesn't match matcher `m`.|
|:---------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------|
|`EXPECT_THAT(expression, m)`|Generates a non-fatal failure if the value of `expression` doesn't match matcher `m`.                                                          |

# Actions #

**Actions** specify what a mock function should do when invoked.

## Returning a Value ##

|`Return()`|Return from a `void` mock function.|
|:---------|:----------------------------------|
|`Return(value)`|Return `value`. If the type of `value` is different to the mock function's return type, `value` is converted to the latter type <i>at the time the expectation is set</i>, not when the action is executed.|
|`ReturnArg<N>()`|Return the `N`-th (0-based) argument.|
|`ReturnNew<T>(a1, ..., ak)`|Return `new T(a1, ..., ak)`; a different object is created each time.|
|`ReturnNull()`|Return a null pointer.             |
|`ReturnPointee(ptr)`|Return the value pointed to by `ptr`.|
|`ReturnRef(variable)`|Return a reference to `variable`.  |
|`ReturnRefOfCopy(value)`|Return a reference to a copy of `value`; the copy lives as long as the action.|

## Side Effects ##

|`Assign(&variable, value)`|Assign `value` to variable.|
|:-------------------------|:--------------------------|
| `DeleteArg<N>()`         | Delete the `N`-th (0-based) argument, which must be a pointer. |
| `SaveArg<N>(pointer)`    | Save the `N`-th (0-based) argument to `*pointer`. |
| `SaveArgPointee<N>(pointer)` | Save the value pointed to by the `N`-th (0-based) argument to `*pointer`. |
| `SetArgReferee<N>(value)` |	Assign value to the variable referenced by the `N`-th (0-based) argument. |
|`SetArgPointee<N>(value)` |Assign `value` to the variable pointed by the `N`-th (0-based) argument.|
|`SetArgumentPointee<N>(value)`|Same as `SetArgPointee<N>(value)`. Deprecated. Will be removed in v1.7.0.|
|`SetArrayArgument<N>(first, last)`|Copies the elements in source range [`first`, `last`) to the array pointed to by the `N`-th (0-based) argument, which can be either a pointer or an iterator. The action does not take ownership of the elements in the source range.|
|`SetErrnoAndReturn(error, value)`|Set `errno` to `error` and return `value`.|
|`Throw(exception)`        |Throws the given exception, which can be any copyable value. Available since v1.1.0.|

## Using a Function or a Functor as an Action ##

|`Invoke(f)`|Invoke `f` with the arguments passed to the mock function, where `f` can be a global/static function or a functor.|
|:----------|:-----------------------------------------------------------------------------------------------------------------|
|`Invoke(object_pointer, &class::method)`|Invoke the {method on the object with the arguments passed to the mock function.                                  |
|`InvokeWithoutArgs(f)`|Invoke `f`, which can be a global/static function or a functor. `f` must take no arguments.                       |
|`InvokeWithoutArgs(object_pointer, &class::method)`|Invoke the method on the object, which takes no arguments.                                                        |
|`InvokeArgument<N>(arg1, arg2, ..., argk)`|Invoke the mock function's `N`-th (0-based) argument, which must be a function or a functor, with the `k` arguments.|

The return value of the invoked function is used as the return value
of the action.

When defining a function or functor to be used with `Invoke*()`, you can declare any unused parameters as `Unused`:
```
  double Distance(Unused, double x, double y) { return sqrt(x*x + y*y); }
  ...
  EXPECT_CALL(mock, Foo("Hi", _, _)).WillOnce(Invoke(Distance));
```

In `InvokeArgument<N>(...)`, if an argument needs to be passed by reference, wrap it inside `ByRef()`. For example,
```
  InvokeArgument<2>(5, string("Hi"), ByRef(foo))
```
calls the mock function's #2 argument, passing to it `5` and `string("Hi")` by value, and `foo` by reference.

## Default Action ##

|`DoDefault()`|Do the default action (specified by `ON_CALL()` or the built-in one).|
|:------------|:--------------------------------------------------------------------|

**Note:** due to technical reasons, `DoDefault()` cannot be used inside  a composite action - trying to do so will result in a run-time error.

## Composite Actions ##

|`DoAll(a1, a2, ..., an)`|Do all actions `a1` to `an` and return the result of `an` in each invocation. The first `n - 1` sub-actions must return void. |
|:-----------------------|:-----------------------------------------------------------------------------------------------------------------------------|
|`IgnoreResult(a)`       |Perform action `a` and ignore its result. `a` must not return void.                                                           |
|`WithArg<N>(a)`         |Pass the `N`-th (0-based) argument of the mock function to action `a` and perform it.                                         |
|`WithArgs<N1, N2, ..., Nk>(a)`|Pass the selected (0-based) arguments of the mock function to action `a` and perform it.                                      |
|`WithoutArgs(a)`        |Perform action `a` without any arguments.                                                                                     |

## Defining Actions ##

| `ACTION(Sum) { return arg0 + arg1; }` | Defines an action `Sum()` to return the sum of the mock function's argument #0 and #1. |
|:--------------------------------------|:---------------------------------------------------------------------------------------|
| `ACTION_P(Plus, n) { return arg0 + n; }` | Defines an action `Plus(n)` to return the sum of the mock function's argument #0 and `n`. |
| `ACTION_Pk(Foo, p1, ..., pk) { statements; }` | Defines a parameterized action `Foo(p1, ..., pk)` to execute the given `statements`.   |

The `ACTION*` macros cannot be used inside a function or class.

# Cardinalities #

These are used in `Times()` to specify how many times a mock function will be called:

|`AnyNumber()`|The function can be called any number of times.|
|:------------|:----------------------------------------------|
|`AtLeast(n)` |The call is expected at least `n` times.       |
|`AtMost(n)`  |The call is expected at most `n` times.        |
|`Between(m, n)`|The call is expected between `m` and `n` (inclusive) times.|
|`Exactly(n) or n`|The call is expected exactly `n` times. In particular, the call should never happen when `n` is 0.|

# Expectation Order #

By default, the expectations can be matched in _any_ order.  If some
or all expectations must be matched in a given order, there are two
ways to specify it.  They can be used either independently or
together.

## The After Clause ##

```
using ::testing::Expectation;
...
Expectation init_x = EXPECT_CALL(foo, InitX());
Expectation init_y = EXPECT_CALL(foo, InitY());
EXPECT_CALL(foo, Bar())
    .After(init_x, init_y);
```
says that `Bar()` can be called only after both `InitX()` and
`InitY()` have been called.

If you don't know how many pre-requisites an expectation has when you
write it, you can use an `ExpectationSet` to collect them:

```
using ::testing::ExpectationSet;
...
ExpectationSet all_inits;
for (int i = 0; i < element_count; i++) {
  all_inits += EXPECT_CALL(foo, InitElement(i));
}
EXPECT_CALL(foo, Bar())
    .After(all_inits);
```
says that `Bar()` can be called only after all elements have been
initialized (but we don't care about which elements get initialized
before the others).

Modifying an `ExpectationSet` after using it in an `.After()` doesn't
affect the meaning of the `.After()`.

## Sequences ##

When you have a long chain of sequential expectations, it's easier to
specify the order using **sequences**, which don't require you to given
each expectation in the chain a different name.  <i>All expected<br>
calls</i> in the same sequence must occur in the order they are
specified.

```
using ::testing::Sequence;
Sequence s1, s2;
...
EXPECT_CALL(foo, Reset())
    .InSequence(s1, s2)
    .WillOnce(Return(true));
EXPECT_CALL(foo, GetSize())
    .InSequence(s1)
    .WillOnce(Return(1));
EXPECT_CALL(foo, Describe(A<const char*>()))
    .InSequence(s2)
    .WillOnce(Return("dummy"));
```
says that `Reset()` must be called before _both_ `GetSize()` _and_
`Describe()`, and the latter two can occur in any order.

To put many expectations in a sequence conveniently:
```
using ::testing::InSequence;
{
  InSequence dummy;

  EXPECT_CALL(...)...;
  EXPECT_CALL(...)...;
  ...
  EXPECT_CALL(...)...;
}
```
says that all expected calls in the scope of `dummy` must occur in
strict order. The name `dummy` is irrelevant.)

# Verifying and Resetting a Mock #

Google Mock will verify the expectations on a mock object when it is destructed, or you can do it earlier:
```
using ::testing::Mock;
...
// Verifies and removes the expectations on mock_obj;
// returns true iff successful.
Mock::VerifyAndClearExpectations(&mock_obj);
...
// Verifies and removes the expectations on mock_obj;
// also removes the default actions set by ON_CALL();
// returns true iff successful.
Mock::VerifyAndClear(&mock_obj);
```

You can also tell Google Mock that a mock object can be leaked and doesn't
need to be verified:
```
Mock::AllowLeak(&mock_obj);
```

# Mock Classes #

Google Mock defines a convenient mock class template
```
class MockFunction<R(A1, ..., An)> {
 public:
  MOCK_METHODn(Call, R(A1, ..., An));
};
```
See this [recipe](CookBook.md#using-check-points) for one application of it.

# Flags #

| `--gmock_catch_leaked_mocks=0` | Don't report leaked mock objects as failures. |
|:-------------------------------|:----------------------------------------------|
| `--gmock_verbose=LEVEL`        | Sets the default verbosity level (`info`, `warning`, or `error`) of Google Mock messages. |


You can find recipes for using Google Mock here. If you haven't yet,
please read the [ForDummies](ForDummies.md) document first to make sure you understand
the basics.

**Note:** Google Mock lives in the `testing` name space. For
readability, it is recommended to write `using ::testing::Foo;` once in
your file before using the name `Foo` defined by Google Mock. We omit
such `using` statements in this page for brevity, but you should do it
in your own code.

# Creating Mock Classes #

## Mocking Private or Protected Methods ##

You must always put a mock method definition (`MOCK_METHOD*`) in a
`public:` section of the mock class, regardless of the method being
mocked being `public`, `protected`, or `private` in the base class.
This allows `ON_CALL` and `EXPECT_CALL` to reference the mock function
from outside of the mock class.  (Yes, C++ allows a subclass to specify
a different access level than the base class on a virtual function.)
Example:

```
class Foo {
 public:
  ...
  virtual bool Transform(Gadget* g) = 0;

 protected:
  virtual void Resume();

 private:
  virtual int GetTimeOut();
};

class MockFoo : public Foo {
 public:
  ...
  MOCK_METHOD1(Transform, bool(Gadget* g));

  // The following must be in the public section, even though the
  // methods are protected or private in the base class.
  MOCK_METHOD0(Resume, void());
  MOCK_METHOD0(GetTimeOut, int());
};
```

## Mocking Overloaded Methods ##

You can mock overloaded functions as usual. No special attention is required:

```
class Foo {
  ...

  // Must be virtual as we'll inherit from Foo.
  virtual ~Foo();

  // Overloaded on the types and/or numbers of arguments.
  virtual int Add(Element x);
  virtual int Add(int times, Element x);

  // Overloaded on the const-ness of this object.
  virtual Bar& GetBar();
  virtual const Bar& GetBar() const;
};

class MockFoo : public Foo {
  ...
  MOCK_METHOD1(Add, int(Element x));
  MOCK_METHOD2(Add, int(int times, Element x);

  MOCK_METHOD0(GetBar, Bar&());
  MOCK_CONST_METHOD0(GetBar, const Bar&());
};
```

**Note:** if you don't mock all versions of the overloaded method, the
compiler will give you a warning about some methods in the base class
being hidden. To fix that, use `using` to bring them in scope:

```
class MockFoo : public Foo {
  ...
  using Foo::Add;
  MOCK_METHOD1(Add, int(Element x));
  // We don't want to mock int Add(int times, Element x);
  ...
};
```

## Mocking Class Templates ##

To mock a class template, append `_T` to the `MOCK_*` macros:

```
template <typename Elem>
class StackInterface {
  ...
  // Must be virtual as we'll inherit from StackInterface.
  virtual ~StackInterface();

  virtual int GetSize() const = 0;
  virtual void Push(const Elem& x) = 0;
};

template <typename Elem>
class MockStack : public StackInterface<Elem> {
  ...
  MOCK_CONST_METHOD0_T(GetSize, int());
  MOCK_METHOD1_T(Push, void(const Elem& x));
};
```

## Mocking Nonvirtual Methods ##

Google Mock can mock non-virtual functions to be used in what we call _hi-perf
dependency injection_.

In this case, instead of sharing a common base class with the real
class, your mock class will be _unrelated_ to the real class, but
contain methods with the same signatures.  The syntax for mocking
non-virtual methods is the _same_ as mocking virtual methods:

```
// A simple packet stream class.  None of its members is virtual.
class ConcretePacketStream {
 public:
  void AppendPacket(Packet* new_packet);
  const Packet* GetPacket(size_t packet_number) const;
  size_t NumberOfPackets() const;
  ...
};

// A mock packet stream class.  It inherits from no other, but defines
// GetPacket() and NumberOfPackets().
class MockPacketStream {
 public:
  MOCK_CONST_METHOD1(GetPacket, const Packet*(size_t packet_number));
  MOCK_CONST_METHOD0(NumberOfPackets, size_t());
  ...
};
```

Note that the mock class doesn't define `AppendPacket()`, unlike the
real class. That's fine as long as the test doesn't need to call it.

Next, you need a way to say that you want to use
`ConcretePacketStream` in production code and to use `MockPacketStream`
in tests.  Since the functions are not virtual and the two classes are
unrelated, you must specify your choice at _compile time_ (as opposed
to run time).

One way to do it is to templatize your code that needs to use a packet
stream.  More specifically, you will give your code a template type
argument for the type of the packet stream.  In production, you will
instantiate your template with `ConcretePacketStream` as the type
argument.  In tests, you will instantiate the same template with
`MockPacketStream`.  For example, you may write:

```
template <class PacketStream>
void CreateConnection(PacketStream* stream) { ... }

template <class PacketStream>
class PacketReader {
 public:
  void ReadPackets(PacketStream* stream, size_t packet_num);
};
```

Then you can use `CreateConnection<ConcretePacketStream>()` and
`PacketReader<ConcretePacketStream>` in production code, and use
`CreateConnection<MockPacketStream>()` and
`PacketReader<MockPacketStream>` in tests.

```
  MockPacketStream mock_stream;
  EXPECT_CALL(mock_stream, ...)...;
  .. set more expectations on mock_stream ...
  PacketReader<MockPacketStream> reader(&mock_stream);
  ... exercise reader ...
```

## Mocking Free Functions ##

It's possible to use Google Mock to mock a free function (i.e. a
C-style function or a static method).  You just need to rewrite your
code to use an interface (abstract class).

Instead of calling a free function (say, `OpenFile`) directly,
introduce an interface for it and have a concrete subclass that calls
the free function:

```
class FileInterface {
 public:
  ...
  virtual bool Open(const char* path, const char* mode) = 0;
};

class File : public FileInterface {
 public:
  ...
  virtual bool Open(const char* path, const char* mode) {
    return OpenFile(path, mode);
  }
};
```

Your code should talk to `FileInterface` to open a file.  Now it's
easy to mock out the function.

This may seem much hassle, but in practice you often have multiple
related functions that you can put in the same interface, so the
per-function syntactic overhead will be much lower.

If you are concerned about the performance overhead incurred by
virtual functions, and profiling confirms your concern, you can
combine this with the recipe for [mocking non-virtual methods](#mocking-nonvirtual-methods).

## The Nice, the Strict, and the Naggy ##

If a mock method has no `EXPECT_CALL` spec but is called, Google Mock
will print a warning about the "uninteresting call". The rationale is:

  * New methods may be added to an interface after a test is written. We shouldn't fail a test just because a method it doesn't know about is called.
  * However, this may also mean there's a bug in the test, so Google Mock shouldn't be silent either. If the user believes these calls are harmless, they can add an `EXPECT_CALL()` to suppress the warning.

However, sometimes you may want to suppress all "uninteresting call"
warnings, while sometimes you may want the opposite, i.e. to treat all
of them as errors. Google Mock lets you make the decision on a
per-mock-object basis.

Suppose your test uses a mock class `MockFoo`:

```
TEST(...) {
  MockFoo mock_foo;
  EXPECT_CALL(mock_foo, DoThis());
  ... code that uses mock_foo ...
}
```

If a method of `mock_foo` other than `DoThis()` is called, it will be
reported by Google Mock as a warning. However, if you rewrite your
test to use `NiceMock<MockFoo>` instead, the warning will be gone,
resulting in a cleaner test output:

```
using ::testing::NiceMock;

TEST(...) {
  NiceMock<MockFoo> mock_foo;
  EXPECT_CALL(mock_foo, DoThis());
  ... code that uses mock_foo ...
}
```

`NiceMock<MockFoo>` is a subclass of `MockFoo`, so it can be used
wherever `MockFoo` is accepted.

It also works if `MockFoo`'s constructor takes some arguments, as
`NiceMock<MockFoo>` "inherits" `MockFoo`'s constructors:

```
using ::testing::NiceMock;

TEST(...) {
  NiceMock<MockFoo> mock_foo(5, "hi");  // Calls MockFoo(5, "hi").
  EXPECT_CALL(mock_foo, DoThis());
  ... code that uses mock_foo ...
}
```

The usage of `StrictMock` is similar, except that it makes all
uninteresting calls failures:

```
using ::testing::StrictMock;

TEST(...) {
  StrictMock<MockFoo> mock_foo;
  EXPECT_CALL(mock_foo, DoThis());
  ... code that uses mock_foo ...

  // The test will fail if a method of mock_foo other than DoThis()
  // is called.
}
```

There are some caveats though (I don't like them just as much as the
next guy, but sadly they are side effects of C++'s limitations):

  1. `NiceMock<MockFoo>` and `StrictMock<MockFoo>` only work for mock methods defined using the `MOCK_METHOD*` family of macros **directly** in the `MockFoo` class. If a mock method is defined in a **base class** of `MockFoo`, the "nice" or "strict" modifier may not affect it, depending on the compiler. In particular, nesting `NiceMock` and `StrictMock` (e.g. `NiceMock<StrictMock<MockFoo> >`) is **not** supported.
  1. The constructors of the base mock (`MockFoo`) cannot have arguments passed by non-const reference, which happens to be banned by the [Google C++ style guide](https://google.github.io/styleguide/cppguide.html).
  1. During the constructor or destructor of `MockFoo`, the mock object is _not_ nice or strict.  This may cause surprises if the constructor or destructor calls a mock method on `this` object. (This behavior, however, is consistent with C++'s general rule: if a constructor or destructor calls a virtual method of `this` object, that method is treated as non-virtual.  In other words, to the base class's constructor or destructor, `this` object behaves like an instance of the base class, not the derived class.  This rule is required for safety.  Otherwise a base constructor may use members of a derived class before they are initialized, or a base destructor may use members of a derived class after they have been destroyed.)

Finally, you should be **very cautious** about when to use naggy or strict mocks, as they tend to make tests more brittle and harder to maintain. When you refactor your code without changing its externally visible behavior, ideally you should't need to update any tests. If your code interacts with a naggy mock, however, you may start to get spammed with warnings as the result of your change. Worse, if your code interacts with a strict mock, your tests may start to fail and you'll be forced to fix them. Our general recommendation is to use nice mocks (not yet the default) most of the time, use naggy mocks (the current default) when developing or debugging tests, and use strict mocks only as the last resort.

## Simplifying the Interface without Breaking Existing Code ##

Sometimes a method has a long list of arguments that is mostly
uninteresting. For example,

```
class LogSink {
 public:
  ...
  virtual void send(LogSeverity severity, const char* full_filename,
                    const char* base_filename, int line,
                    const struct tm* tm_time,
                    const char* message, size_t message_len) = 0;
};
```

This method's argument list is lengthy and hard to work with (let's
say that the `message` argument is not even 0-terminated). If we mock
it as is, using the mock will be awkward. If, however, we try to
simplify this interface, we'll need to fix all clients depending on
it, which is often infeasible.

The trick is to re-dispatch the method in the mock class:

```
class ScopedMockLog : public LogSink {
 public:
  ...
  virtual void send(LogSeverity severity, const char* full_filename,
                    const char* base_filename, int line, const tm* tm_time,
                    const char* message, size_t message_len) {
    // We are only interested in the log severity, full file name, and
    // log message.
    Log(severity, full_filename, std::string(message, message_len));
  }

  // Implements the mock method:
  //
  //   void Log(LogSeverity severity,
  //            const string& file_path,
  //            const string& message);
  MOCK_METHOD3(Log, void(LogSeverity severity, const string& file_path,
                         const string& message));
};
```

By defining a new mock method with a trimmed argument list, we make
the mock class much more user-friendly.

## Alternative to Mocking Concrete Classes ##

Often you may find yourself using classes that don't implement
interfaces. In order to test your code that uses such a class (let's
call it `Concrete`), you may be tempted to make the methods of
`Concrete` virtual and then mock it.

Try not to do that.

Making a non-virtual function virtual is a big decision. It creates an
extension point where subclasses can tweak your class' behavior. This
weakens your control on the class because now it's harder to maintain
the class' invariants. You should make a function virtual only when
there is a valid reason for a subclass to override it.

Mocking concrete classes directly is problematic as it creates a tight
coupling between the class and the tests - any small change in the
class may invalidate your tests and make test maintenance a pain.

To avoid such problems, many programmers have been practicing "coding
to interfaces": instead of talking to the `Concrete` class, your code
would define an interface and talk to it. Then you implement that
interface as an adaptor on top of `Concrete`. In tests, you can easily
mock that interface to observe how your code is doing.

This technique incurs some overhead:

  * You pay the cost of virtual function calls (usually not a problem).
  * There is more abstraction for the programmers to learn.

However, it can also bring significant benefits in addition to better
testability:

  * `Concrete`'s API may not fit your problem domain very well, as you may not be the only client it tries to serve. By designing your own interface, you have a chance to tailor it to your need - you may add higher-level functionalities, rename stuff, etc instead of just trimming the class. This allows you to write your code (user of the interface) in a more natural way, which means it will be more readable, more maintainable, and you'll be more productive.
  * If `Concrete`'s implementation ever has to change, you don't have to rewrite everywhere it is used. Instead, you can absorb the change in your implementation of the interface, and your other code and tests will be insulated from this change.

Some people worry that if everyone is practicing this technique, they
will end up writing lots of redundant code. This concern is totally
understandable. However, there are two reasons why it may not be the
case:

  * Different projects may need to use `Concrete` in different ways, so the best interfaces for them will be different. Therefore, each of them will have its own domain-specific interface on top of `Concrete`, and they will not be the same code.
  * If enough projects want to use the same interface, they can always share it, just like they have been sharing `Concrete`. You can check in the interface and the adaptor somewhere near `Concrete` (perhaps in a `contrib` sub-directory) and let many projects use it.

You need to weigh the pros and cons carefully for your particular
problem, but I'd like to assure you that the Java community has been
practicing this for a long time and it's a proven effective technique
applicable in a wide variety of situations. :-)

## Delegating Calls to a Fake ##

Some times you have a non-trivial fake implementation of an
interface. For example:

```
class Foo {
 public:
  virtual ~Foo() {}
  virtual char DoThis(int n) = 0;
  virtual void DoThat(const char* s, int* p) = 0;
};

class FakeFoo : public Foo {
 public:
  virtual char DoThis(int n) {
    return (n > 0) ? '+' :
        (n < 0) ? '-' : '0';
  }

  virtual void DoThat(const char* s, int* p) {
    *p = strlen(s);
  }
};
```

Now you want to mock this interface such that you can set expectations
on it. However, you also want to use `FakeFoo` for the default
behavior, as duplicating it in the mock object is, well, a lot of
work.

When you define the mock class using Google Mock, you can have it
delegate its default action to a fake class you already have, using
this pattern:

```
using ::testing::_;
using ::testing::Invoke;

class MockFoo : public Foo {
 public:
  // Normal mock method definitions using Google Mock.
  MOCK_METHOD1(DoThis, char(int n));
  MOCK_METHOD2(DoThat, void(const char* s, int* p));

  // Delegates the default actions of the methods to a FakeFoo object.
  // This must be called *before* the custom ON_CALL() statements.
  void DelegateToFake() {
    ON_CALL(*this, DoThis(_))
        .WillByDefault(Invoke(&fake_, &FakeFoo::DoThis));
    ON_CALL(*this, DoThat(_, _))
        .WillByDefault(Invoke(&fake_, &FakeFoo::DoThat));
  }
 private:
  FakeFoo fake_;  // Keeps an instance of the fake in the mock.
};
```

With that, you can use `MockFoo` in your tests as usual. Just remember
that if you don't explicitly set an action in an `ON_CALL()` or
`EXPECT_CALL()`, the fake will be called upon to do it:

```
using ::testing::_;

TEST(AbcTest, Xyz) {
  MockFoo foo;
  foo.DelegateToFake(); // Enables the fake for delegation.

  // Put your ON_CALL(foo, ...)s here, if any.

  // No action specified, meaning to use the default action.
  EXPECT_CALL(foo, DoThis(5));
  EXPECT_CALL(foo, DoThat(_, _));

  int n = 0;
  EXPECT_EQ('+', foo.DoThis(5));  // FakeFoo::DoThis() is invoked.
  foo.DoThat("Hi", &n);           // FakeFoo::DoThat() is invoked.
  EXPECT_EQ(2, n);
}
```

**Some tips:**

  * If you want, you can still override the default action by providing your own `ON_CALL()` or using `.WillOnce()` / `.WillRepeatedly()` in `EXPECT_CALL()`.
  * In `DelegateToFake()`, you only need to delegate the methods whose fake implementation you intend to use.
  * The general technique discussed here works for overloaded methods, but you'll need to tell the compiler which version you mean. To disambiguate a mock function (the one you specify inside the parentheses of `ON_CALL()`), see the "Selecting Between Overloaded Functions" section on this page; to disambiguate a fake function (the one you place inside `Invoke()`), use a `static_cast` to specify the function's type. For instance, if class `Foo` has methods `char DoThis(int n)` and `bool DoThis(double x) const`, and you want to invoke the latter, you need to write `Invoke(&fake_, static_cast<bool (FakeFoo::*)(double) const>(&FakeFoo::DoThis))` instead of `Invoke(&fake_, &FakeFoo::DoThis)` (The strange-looking thing inside the angled brackets of `static_cast` is the type of a function pointer to the second `DoThis()` method.).
  * Having to mix a mock and a fake is often a sign of something gone wrong. Perhaps you haven't got used to the interaction-based way of testing yet. Or perhaps your interface is taking on too many roles and should be split up. Therefore, **don't abuse this**. We would only recommend to do it as an intermediate step when you are refactoring your code.

Regarding the tip on mixing a mock and a fake, here's an example on
why it may be a bad sign: Suppose you have a class `System` for
low-level system operations. In particular, it does file and I/O
operations. And suppose you want to test how your code uses `System`
to do I/O, and you just want the file operations to work normally. If
you mock out the entire `System` class, you'll have to provide a fake
implementation for the file operation part, which suggests that
`System` is taking on too many roles.

Instead, you can define a `FileOps` interface and an `IOOps` interface
and split `System`'s functionalities into the two. Then you can mock
`IOOps` without mocking `FileOps`.

## Delegating Calls to a Real Object ##

When using testing doubles (mocks, fakes, stubs, and etc), sometimes
their behaviors will differ from those of the real objects. This
difference could be either intentional (as in simulating an error such
that you can test the error handling code) or unintentional. If your
mocks have different behaviors than the real objects by mistake, you
could end up with code that passes the tests but fails in production.

You can use the _delegating-to-real_ technique to ensure that your
mock has the same behavior as the real object while retaining the
ability to validate calls. This technique is very similar to the
delegating-to-fake technique, the difference being that we use a real
object instead of a fake. Here's an example:

```
using ::testing::_;
using ::testing::AtLeast;
using ::testing::Invoke;

class MockFoo : public Foo {
 public:
  MockFoo() {
    // By default, all calls are delegated to the real object.
    ON_CALL(*this, DoThis())
        .WillByDefault(Invoke(&real_, &Foo::DoThis));
    ON_CALL(*this, DoThat(_))
        .WillByDefault(Invoke(&real_, &Foo::DoThat));
    ...
  }
  MOCK_METHOD0(DoThis, ...);
  MOCK_METHOD1(DoThat, ...);
  ...
 private:
  Foo real_;
};
...

  MockFoo mock;

  EXPECT_CALL(mock, DoThis())
      .Times(3);
  EXPECT_CALL(mock, DoThat("Hi"))
      .Times(AtLeast(1));
  ... use mock in test ...
```

With this, Google Mock will verify that your code made the right calls
(with the right arguments, in the right order, called the right number
of times, etc), and a real object will answer the calls (so the
behavior will be the same as in production). This gives you the best
of both worlds.

## Delegating Calls to a Parent Class ##

Ideally, you should code to interfaces, whose methods are all pure
virtual. In reality, sometimes you do need to mock a virtual method
that is not pure (i.e, it already has an implementation). For example:

```
class Foo {
 public:
  virtual ~Foo();

  virtual void Pure(int n) = 0;
  virtual int Concrete(const char* str) { ... }
};

class MockFoo : public Foo {
 public:
  // Mocking a pure method.
  MOCK_METHOD1(Pure, void(int n));
  // Mocking a concrete method.  Foo::Concrete() is shadowed.
  MOCK_METHOD1(Concrete, int(const char* str));
};
```

Sometimes you may want to call `Foo::Concrete()` instead of
`MockFoo::Concrete()`. Perhaps you want to do it as part of a stub
action, or perhaps your test doesn't need to mock `Concrete()` at all
(but it would be oh-so painful to have to define a new mock class
whenever you don't need to mock one of its methods).

The trick is to leave a back door in your mock class for accessing the
real methods in the base class:

```
class MockFoo : public Foo {
 public:
  // Mocking a pure method.
  MOCK_METHOD1(Pure, void(int n));
  // Mocking a concrete method.  Foo::Concrete() is shadowed.
  MOCK_METHOD1(Concrete, int(const char* str));

  // Use this to call Concrete() defined in Foo.
  int FooConcrete(const char* str) { return Foo::Concrete(str); }
};
```

Now, you can call `Foo::Concrete()` inside an action by:

```
using ::testing::_;
using ::testing::Invoke;
...
  EXPECT_CALL(foo, Concrete(_))
      .WillOnce(Invoke(&foo, &MockFoo::FooConcrete));
```

or tell the mock object that you don't want to mock `Concrete()`:

```
using ::testing::Invoke;
...
  ON_CALL(foo, Concrete(_))
      .WillByDefault(Invoke(&foo, &MockFoo::FooConcrete));
```

(Why don't we just write `Invoke(&foo, &Foo::Concrete)`? If you do
that, `MockFoo::Concrete()` will be called (and cause an infinite
recursion) since `Foo::Concrete()` is virtual. That's just how C++
works.)

# Using Matchers #

## Matching Argument Values Exactly ##

You can specify exactly which arguments a mock method is expecting:

```
using ::testing::Return;
...
  EXPECT_CALL(foo, DoThis(5))
      .WillOnce(Return('a'));
  EXPECT_CALL(foo, DoThat("Hello", bar));
```

## Using Simple Matchers ##

You can use matchers to match arguments that have a certain property:

```
using ::testing::Ge;
using ::testing::NotNull;
using ::testing::Return;
...
  EXPECT_CALL(foo, DoThis(Ge(5)))  // The argument must be >= 5.
      .WillOnce(Return('a'));
  EXPECT_CALL(foo, DoThat("Hello", NotNull()));
  // The second argument must not be NULL.
```

A frequently used matcher is `_`, which matches anything:

```
using ::testing::_;
using ::testing::NotNull;
...
  EXPECT_CALL(foo, DoThat(_, NotNull()));
```

## Combining Matchers ##

You can build complex matchers from existing ones using `AllOf()`,
`AnyOf()`, and `Not()`:

```
using ::testing::AllOf;
using ::testing::Gt;
using ::testing::HasSubstr;
using ::testing::Ne;
using ::testing::Not;
...
  // The argument must be > 5 and != 10.
  EXPECT_CALL(foo, DoThis(AllOf(Gt(5),
                                Ne(10))));

  // The first argument must not contain sub-string "blah".
  EXPECT_CALL(foo, DoThat(Not(HasSubstr("blah")),
                          NULL));
```

## Casting Matchers ##

Google Mock matchers are statically typed, meaning that the compiler
can catch your mistake if you use a matcher of the wrong type (for
example, if you use `Eq(5)` to match a `string` argument). Good for
you!

Sometimes, however, you know what you're doing and want the compiler
to give you some slack. One example is that you have a matcher for
`long` and the argument you want to match is `int`. While the two
types aren't exactly the same, there is nothing really wrong with
using a `Matcher<long>` to match an `int` - after all, we can first
convert the `int` argument to a `long` before giving it to the
matcher.

To support this need, Google Mock gives you the
`SafeMatcherCast<T>(m)` function. It casts a matcher `m` to type
`Matcher<T>`. To ensure safety, Google Mock checks that (let `U` be the
type `m` accepts):

  1. Type `T` can be implicitly cast to type `U`;
  1. When both `T` and `U` are built-in arithmetic types (`bool`, integers, and floating-point numbers), the conversion from `T` to `U` is not lossy (in other words, any value representable by `T` can also be represented by `U`); and
  1. When `U` is a reference, `T` must also be a reference (as the underlying matcher may be interested in the address of the `U` value).

The code won't compile if any of these conditions aren't met.

Here's one example:

```
using ::testing::SafeMatcherCast;

// A base class and a child class.
class Base { ... };
class Derived : public Base { ... };

class MockFoo : public Foo {
 public:
  MOCK_METHOD1(DoThis, void(Derived* derived));
};
...

  MockFoo foo;
  // m is a Matcher<Base*> we got from somewhere.
  EXPECT_CALL(foo, DoThis(SafeMatcherCast<Derived*>(m)));
```

If you find `SafeMatcherCast<T>(m)` too limiting, you can use a similar
function `MatcherCast<T>(m)`. The difference is that `MatcherCast` works
as long as you can `static_cast` type `T` to type `U`.

`MatcherCast` essentially lets you bypass C++'s type system
(`static_cast` isn't always safe as it could throw away information,
for example), so be careful not to misuse/abuse it.

## Selecting Between Overloaded Functions ##

If you expect an overloaded function to be called, the compiler may
need some help on which overloaded version it is.

To disambiguate functions overloaded on the const-ness of this object,
use the `Const()` argument wrapper.

```
using ::testing::ReturnRef;

class MockFoo : public Foo {
  ...
  MOCK_METHOD0(GetBar, Bar&());
  MOCK_CONST_METHOD0(GetBar, const Bar&());
};
...

  MockFoo foo;
  Bar bar1, bar2;
  EXPECT_CALL(foo, GetBar())         // The non-const GetBar().
      .WillOnce(ReturnRef(bar1));
  EXPECT_CALL(Const(foo), GetBar())  // The const GetBar().
      .WillOnce(ReturnRef(bar2));
```

(`Const()` is defined by Google Mock and returns a `const` reference
to its argument.)

To disambiguate overloaded functions with the same number of arguments
but different argument types, you may need to specify the exact type
of a matcher, either by wrapping your matcher in `Matcher<type>()`, or
using a matcher whose type is fixed (`TypedEq<type>`, `An<type>()`,
etc):

```
using ::testing::An;
using ::testing::Lt;
using ::testing::Matcher;
using ::testing::TypedEq;

class MockPrinter : public Printer {
 public:
  MOCK_METHOD1(Print, void(int n));
  MOCK_METHOD1(Print, void(char c));
};

TEST(PrinterTest, Print) {
  MockPrinter printer;

  EXPECT_CALL(printer, Print(An<int>()));            // void Print(int);
  EXPECT_CALL(printer, Print(Matcher<int>(Lt(5))));  // void Print(int);
  EXPECT_CALL(printer, Print(TypedEq<char>('a')));   // void Print(char);

  printer.Print(3);
  printer.Print(6);
  printer.Print('a');
}
```

## Performing Different Actions Based on the Arguments ##

When a mock method is called, the _last_ matching expectation that's
still active will be selected (think "newer overrides older"). So, you
can make a method do different things depending on its argument values
like this:

```
using ::testing::_;
using ::testing::Lt;
using ::testing::Return;
...
  // The default case.
  EXPECT_CALL(foo, DoThis(_))
      .WillRepeatedly(Return('b'));

  // The more specific case.
  EXPECT_CALL(foo, DoThis(Lt(5)))
      .WillRepeatedly(Return('a'));
```

Now, if `foo.DoThis()` is called with a value less than 5, `'a'` will
be returned; otherwise `'b'` will be returned.

## Matching Multiple Arguments as a Whole ##

Sometimes it's not enough to match the arguments individually. For
example, we may want to say that the first argument must be less than
the second argument. The `With()` clause allows us to match
all arguments of a mock function as a whole. For example,

```
using ::testing::_;
using ::testing::Lt;
using ::testing::Ne;
...
  EXPECT_CALL(foo, InRange(Ne(0), _))
      .With(Lt());
```

says that the first argument of `InRange()` must not be 0, and must be
less than the second argument.

The expression inside `With()` must be a matcher of type
`Matcher< ::testing::tuple<A1, ..., An> >`, where `A1`, ..., `An` are the
types of the function arguments.

You can also write `AllArgs(m)` instead of `m` inside `.With()`. The
two forms are equivalent, but `.With(AllArgs(Lt()))` is more readable
than `.With(Lt())`.

You can use `Args<k1, ..., kn>(m)` to match the `n` selected arguments
(as a tuple) against `m`. For example,

```
using ::testing::_;
using ::testing::AllOf;
using ::testing::Args;
using ::testing::Lt;
...
  EXPECT_CALL(foo, Blah(_, _, _))
      .With(AllOf(Args<0, 1>(Lt()), Args<1, 2>(Lt())));
```

says that `Blah()` will be called with arguments `x`, `y`, and `z` where
`x < y < z`.

As a convenience and example, Google Mock provides some matchers for
2-tuples, including the `Lt()` matcher above. See the [CheatSheet](CheatSheet.md) for
the complete list.

Note that if you want to pass the arguments to a predicate of your own
(e.g. `.With(Args<0, 1>(Truly(&MyPredicate)))`), that predicate MUST be
written to take a `::testing::tuple` as its argument; Google Mock will pass the `n` selected arguments as _one_ single tuple to the predicate.

## Using Matchers as Predicates ##

Have you noticed that a matcher is just a fancy predicate that also
knows how to describe itself? Many existing algorithms take predicates
as arguments (e.g. those defined in STL's `<algorithm>` header), and
it would be a shame if Google Mock matchers are not allowed to
participate.

Luckily, you can use a matcher where a unary predicate functor is
expected by wrapping it inside the `Matches()` function. For example,

```
#include <algorithm>
#include <vector>

std::vector<int> v;
...
// How many elements in v are >= 10?
const int count = count_if(v.begin(), v.end(), Matches(Ge(10)));
```

Since you can build complex matchers from simpler ones easily using
Google Mock, this gives you a way to conveniently construct composite
predicates (doing the same using STL's `<functional>` header is just
painful). For example, here's a predicate that's satisfied by any
number that is >= 0, <= 100, and != 50:

```
Matches(AllOf(Ge(0), Le(100), Ne(50)))
```

## Using Matchers in Google Test Assertions ##

Since matchers are basically predicates that also know how to describe
themselves, there is a way to take advantage of them in
[Google Test](../../googletest/) assertions. It's
called `ASSERT_THAT` and `EXPECT_THAT`:

```
  ASSERT_THAT(value, matcher);  // Asserts that value matches matcher.
  EXPECT_THAT(value, matcher);  // The non-fatal version.
```

For example, in a Google Test test you can write:

```
#include "gmock/gmock.h"

using ::testing::AllOf;
using ::testing::Ge;
using ::testing::Le;
using ::testing::MatchesRegex;
using ::testing::StartsWith;
...

  EXPECT_THAT(Foo(), StartsWith("Hello"));
  EXPECT_THAT(Bar(), MatchesRegex("Line \\d+"));
  ASSERT_THAT(Baz(), AllOf(Ge(5), Le(10)));
```

which (as you can probably guess) executes `Foo()`, `Bar()`, and
`Baz()`, and verifies that:

  * `Foo()` returns a string that starts with `"Hello"`.
  * `Bar()` returns a string that matches regular expression `"Line \\d+"`.
  * `Baz()` returns a number in the range [5, 10].

The nice thing about these macros is that _they read like
English_. They generate informative messages too. For example, if the
first `EXPECT_THAT()` above fails, the message will be something like:

```
Value of: Foo()
  Actual: "Hi, world!"
Expected: starts with "Hello"
```

**Credit:** The idea of `(ASSERT|EXPECT)_THAT` was stolen from the
[Hamcrest](https://github.com/hamcrest/) project, which adds
`assertThat()` to JUnit.

## Using Predicates as Matchers ##

Google Mock provides a built-in set of matchers. In case you find them
lacking, you can use an arbitray unary predicate function or functor
as a matcher - as long as the predicate accepts a value of the type
you want. You do this by wrapping the predicate inside the `Truly()`
function, for example:

```
using ::testing::Truly;

int IsEven(int n) { return (n % 2) == 0 ? 1 : 0; }
...

  // Bar() must be called with an even number.
  EXPECT_CALL(foo, Bar(Truly(IsEven)));
```

Note that the predicate function / functor doesn't have to return
`bool`. It works as long as the return value can be used as the
condition in statement `if (condition) ...`.

## Matching Arguments that Are Not Copyable ##

When you do an `EXPECT_CALL(mock_obj, Foo(bar))`, Google Mock saves
away a copy of `bar`. When `Foo()` is called later, Google Mock
compares the argument to `Foo()` with the saved copy of `bar`. This
way, you don't need to worry about `bar` being modified or destroyed
after the `EXPECT_CALL()` is executed. The same is true when you use
matchers like `Eq(bar)`, `Le(bar)`, and so on.

But what if `bar` cannot be copied (i.e. has no copy constructor)? You
could define your own matcher function and use it with `Truly()`, as
the previous couple of recipes have shown. Or, you may be able to get
away from it if you can guarantee that `bar` won't be changed after
the `EXPECT_CALL()` is executed. Just tell Google Mock that it should
save a reference to `bar`, instead of a copy of it. Here's how:

```
using ::testing::Eq;
using ::testing::ByRef;
using ::testing::Lt;
...
  // Expects that Foo()'s argument == bar.
  EXPECT_CALL(mock_obj, Foo(Eq(ByRef(bar))));

  // Expects that Foo()'s argument < bar.
  EXPECT_CALL(mock_obj, Foo(Lt(ByRef(bar))));
```

Remember: if you do this, don't change `bar` after the
`EXPECT_CALL()`, or the result is undefined.

## Validating a Member of an Object ##

Often a mock function takes a reference to object as an argument. When
matching the argument, you may not want to compare the entire object
against a fixed object, as that may be over-specification. Instead,
you may need to validate a certain member variable or the result of a
certain getter method of the object. You can do this with `Field()`
and `Property()`. More specifically,

```
Field(&Foo::bar, m)
```

is a matcher that matches a `Foo` object whose `bar` member variable
satisfies matcher `m`.

```
Property(&Foo::baz, m)
```

is a matcher that matches a `Foo` object whose `baz()` method returns
a value that satisfies matcher `m`.

For example:

| Expression                   | Description                        |
|:-----------------------------|:-----------------------------------|
| `Field(&Foo::number, Ge(3))` | Matches `x` where `x.number >= 3`. |
| `Property(&Foo::name, StartsWith("John "))` | Matches `x` where `x.name()` starts with `"John "`. |

Note that in `Property(&Foo::baz, ...)`, method `baz()` must take no
argument and be declared as `const`.

BTW, `Field()` and `Property()` can also match plain pointers to
objects. For instance,

```
Field(&Foo::number, Ge(3))
```

matches a plain pointer `p` where `p->number >= 3`. If `p` is `NULL`,
the match will always fail regardless of the inner matcher.

What if you want to validate more than one members at the same time?
Remember that there is `AllOf()`.

## Validating the Value Pointed to by a Pointer Argument ##

C++ functions often take pointers as arguments. You can use matchers
like `IsNull()`, `NotNull()`, and other comparison matchers to match a
pointer, but what if you want to make sure the value _pointed to_ by
the pointer, instead of the pointer itself, has a certain property?
Well, you can use the `Pointee(m)` matcher.

`Pointee(m)` matches a pointer iff `m` matches the value the pointer
points to. For example:

```
using ::testing::Ge;
using ::testing::Pointee;
...
  EXPECT_CALL(foo, Bar(Pointee(Ge(3))));
```

expects `foo.Bar()` to be called with a pointer that points to a value
greater than or equal to 3.

One nice thing about `Pointee()` is that it treats a `NULL` pointer as
a match failure, so you can write `Pointee(m)` instead of

```
  AllOf(NotNull(), Pointee(m))
```

without worrying that a `NULL` pointer will crash your test.

Also, did we tell you that `Pointee()` works with both raw pointers
**and** smart pointers (`linked_ptr`, `shared_ptr`, `scoped_ptr`, and
etc)?

What if you have a pointer to pointer? You guessed it - you can use
nested `Pointee()` to probe deeper inside the value. For example,
`Pointee(Pointee(Lt(3)))` matches a pointer that points to a pointer
that points to a number less than 3 (what a mouthful...).

## Testing a Certain Property of an Object ##

Sometimes you want to specify that an object argument has a certain
property, but there is no existing matcher that does this. If you want
good error messages, you should define a matcher. If you want to do it
quick and dirty, you could get away with writing an ordinary function.

Let's say you have a mock function that takes an object of type `Foo`,
which has an `int bar()` method and an `int baz()` method, and you
want to constrain that the argument's `bar()` value plus its `baz()`
value is a given number. Here's how you can define a matcher to do it:

```
using ::testing::MatcherInterface;
using ::testing::MatchResultListener;

class BarPlusBazEqMatcher : public MatcherInterface<const Foo&> {
 public:
  explicit BarPlusBazEqMatcher(int expected_sum)
      : expected_sum_(expected_sum) {}

  virtual bool MatchAndExplain(const Foo& foo,
                               MatchResultListener* listener) const {
    return (foo.bar() + foo.baz()) == expected_sum_;
  }

  virtual void DescribeTo(::std::ostream* os) const {
    *os << "bar() + baz() equals " << expected_sum_;
  }

  virtual void DescribeNegationTo(::std::ostream* os) const {
    *os << "bar() + baz() does not equal " << expected_sum_;
  }
 private:
  const int expected_sum_;
};

inline Matcher<const Foo&> BarPlusBazEq(int expected_sum) {
  return MakeMatcher(new BarPlusBazEqMatcher(expected_sum));
}

...

  EXPECT_CALL(..., DoThis(BarPlusBazEq(5)))...;
```

## Matching Containers ##

Sometimes an STL container (e.g. list, vector, map, ...) is passed to
a mock function and you may want to validate it. Since most STL
containers support the `==` operator, you can write
`Eq(expected_container)` or simply `expected_container` to match a
container exactly.

Sometimes, though, you may want to be more flexible (for example, the
first element must be an exact match, but the second element can be
any positive number, and so on). Also, containers used in tests often
have a small number of elements, and having to define the expected
container out-of-line is a bit of a hassle.

You can use the `ElementsAre()` or `UnorderedElementsAre()` matcher in
such cases:

```
using ::testing::_;
using ::testing::ElementsAre;
using ::testing::Gt;
...

  MOCK_METHOD1(Foo, void(const vector<int>& numbers));
...

  EXPECT_CALL(mock, Foo(ElementsAre(1, Gt(0), _, 5)));
```

The above matcher says that the container must have 4 elements, which
must be 1, greater than 0, anything, and 5 respectively.

If you instead write:

```
using ::testing::_;
using ::testing::Gt;
using ::testing::UnorderedElementsAre;
...

  MOCK_METHOD1(Foo, void(const vector<int>& numbers));
...

  EXPECT_CALL(mock, Foo(UnorderedElementsAre(1, Gt(0), _, 5)));
```

It means that the container must have 4 elements, which under some
permutation must be 1, greater than 0, anything, and 5 respectively.

`ElementsAre()` and `UnorderedElementsAre()` are overloaded to take 0
to 10 arguments. If more are needed, you can place them in a C-style
array and use `ElementsAreArray()` or `UnorderedElementsAreArray()`
instead:

```
using ::testing::ElementsAreArray;
...

  // ElementsAreArray accepts an array of element values.
  const int expected_vector1[] = { 1, 5, 2, 4, ... };
  EXPECT_CALL(mock, Foo(ElementsAreArray(expected_vector1)));

  // Or, an array of element matchers.
  Matcher<int> expected_vector2 = { 1, Gt(2), _, 3, ... };
  EXPECT_CALL(mock, Foo(ElementsAreArray(expected_vector2)));
```

In case the array needs to be dynamically created (and therefore the
array size cannot be inferred by the compiler), you can give
`ElementsAreArray()` an additional argument to specify the array size:

```
using ::testing::ElementsAreArray;
...
  int* const expected_vector3 = new int[count];
  ... fill expected_vector3 with values ...
  EXPECT_CALL(mock, Foo(ElementsAreArray(expected_vector3, count)));
```

**Tips:**

  * `ElementsAre*()` can be used to match _any_ container that implements the STL iterator pattern (i.e. it has a `const_iterator` type and supports `begin()/end()`), not just the ones defined in STL. It will even work with container types yet to be written - as long as they follows the above pattern.
  * You can use nested `ElementsAre*()` to match nested (multi-dimensional) containers.
  * If the container is passed by pointer instead of by reference, just write `Pointee(ElementsAre*(...))`.
  * The order of elements _matters_ for `ElementsAre*()`. Therefore don't use it with containers whose element order is undefined (e.g. `hash_map`).

## Sharing Matchers ##

Under the hood, a Google Mock matcher object consists of a pointer to
a ref-counted implementation object. Copying matchers is allowed and
very efficient, as only the pointer is copied. When the last matcher
that references the implementation object dies, the implementation
object will be deleted.

Therefore, if you have some complex matcher that you want to use again
and again, there is no need to build it everytime. Just assign it to a
matcher variable and use that variable repeatedly! For example,

```
  Matcher<int> in_range = AllOf(Gt(5), Le(10));
  ... use in_range as a matcher in multiple EXPECT_CALLs ...
```

# Setting Expectations #

## Knowing When to Expect ##

`ON_CALL` is likely the single most under-utilized construct in Google Mock.

There are basically two constructs for defining the behavior of a mock object: `ON_CALL` and `EXPECT_CALL`. The difference? `ON_CALL` defines what happens when a mock method is called, but _doesn't imply any expectation on the method being called._ `EXPECT_CALL` not only defines the behavior, but also sets an expectation that _the method will be called with the given arguments, for the given number of times_ (and _in the given order_ when you specify the order too).

Since `EXPECT_CALL` does more, isn't it better than `ON_CALL`? Not really. Every `EXPECT_CALL` adds a constraint on the behavior of the code under test. Having more constraints than necessary is _baaad_ - even worse than not having enough constraints.

This may be counter-intuitive. How could tests that verify more be worse than tests that verify less? Isn't verification the whole point of tests?

The answer, lies in _what_ a test should verify. **A good test verifies the contract of the code.** If a test over-specifies, it doesn't leave enough freedom to the implementation. As a result, changing the implementation without breaking the contract (e.g. refactoring and optimization), which should be perfectly fine to do, can break such tests. Then you have to spend time fixing them, only to see them broken again the next time the implementation is changed.

Keep in mind that one doesn't have to verify more than one property in one test. In fact, **it's a good style to verify only one thing in one test.** If you do that, a bug will likely break only one or two tests instead of dozens (which case would you rather debug?). If you are also in the habit of giving tests descriptive names that tell what they verify, you can often easily guess what's wrong just from the test log itself.

So use `ON_CALL` by default, and only use `EXPECT_CALL` when you actually intend to verify that the call is made. For example, you may have a bunch of `ON_CALL`s in your test fixture to set the common mock behavior shared by all tests in the same group, and write (scarcely) different `EXPECT_CALL`s in different `TEST_F`s to verify different aspects of the code's behavior. Compared with the style where each `TEST` has many `EXPECT_CALL`s, this leads to tests that are more resilient to implementational changes (and thus less likely to require maintenance) and makes the intent of the tests more obvious (so they are easier to maintain when you do need to maintain them).

If you are bothered by the "Uninteresting mock function call" message printed when a mock method without an `EXPECT_CALL` is called, you may use a `NiceMock` instead to suppress all such messages for the mock object, or suppress the message for specific methods by adding `EXPECT_CALL(...).Times(AnyNumber())`. DO NOT suppress it by blindly adding an `EXPECT_CALL(...)`, or you'll have a test that's a pain to maintain.

## Ignoring Uninteresting Calls ##

If you are not interested in how a mock method is called, just don't
say anything about it. In this case, if the method is ever called,
Google Mock will perform its default action to allow the test program
to continue. If you are not happy with the default action taken by
Google Mock, you can override it using `DefaultValue<T>::Set()`
(described later in this document) or `ON_CALL()`.

Please note that once you expressed interest in a particular mock
method (via `EXPECT_CALL()`), all invocations to it must match some
expectation. If this function is called but the arguments don't match
any `EXPECT_CALL()` statement, it will be an error.

## Disallowing Unexpected Calls ##

If a mock method shouldn't be called at all, explicitly say so:

```
using ::testing::_;
...
  EXPECT_CALL(foo, Bar(_))
      .Times(0);
```

If some calls to the method are allowed, but the rest are not, just
list all the expected calls:

```
using ::testing::AnyNumber;
using ::testing::Gt;
...
  EXPECT_CALL(foo, Bar(5));
  EXPECT_CALL(foo, Bar(Gt(10)))
      .Times(AnyNumber());
```

A call to `foo.Bar()` that doesn't match any of the `EXPECT_CALL()`
statements will be an error.

## Understanding Uninteresting vs Unexpected Calls ##

_Uninteresting_ calls and _unexpected_ calls are different concepts in Google Mock. _Very_ different.

A call `x.Y(...)` is **uninteresting** if there's _not even a single_ `EXPECT_CALL(x, Y(...))` set. In other words, the test isn't interested in the `x.Y()` method at all, as evident in that the test doesn't care to say anything about it.

A call `x.Y(...)` is **unexpected** if there are some `EXPECT_CALL(x, Y(...))s` set, but none of them matches the call. Put another way, the test is interested in the `x.Y()` method (therefore it _explicitly_ sets some `EXPECT_CALL` to verify how it's called); however, the verification fails as the test doesn't expect this particular call to happen.

**An unexpected call is always an error,** as the code under test doesn't behave the way the test expects it to behave.

**By default, an uninteresting call is not an error,** as it violates no constraint specified by the test. (Google Mock's philosophy is that saying nothing means there is no constraint.) However, it leads to a warning, as it _might_ indicate a problem (e.g. the test author might have forgotten to specify a constraint).

In Google Mock, `NiceMock` and `StrictMock` can be used to make a mock class "nice" or "strict". How does this affect uninteresting calls and unexpected calls?

A **nice mock** suppresses uninteresting call warnings. It is less chatty than the default mock, but otherwise is the same. If a test fails with a default mock, it will also fail using a nice mock instead. And vice versa. Don't expect making a mock nice to change the test's result.

A **strict mock** turns uninteresting call warnings into errors. So making a mock strict may change the test's result.

Let's look at an example:

```
TEST(...) {
  NiceMock<MockDomainRegistry> mock_registry;
  EXPECT_CALL(mock_registry, GetDomainOwner("google.com"))
          .WillRepeatedly(Return("Larry Page"));

  // Use mock_registry in code under test.
  ... &mock_registry ...
}
```

The sole `EXPECT_CALL` here says that all calls to `GetDomainOwner()` must have `"google.com"` as the argument. If `GetDomainOwner("yahoo.com")` is called, it will be an unexpected call, and thus an error. Having a nice mock doesn't change the severity of an unexpected call.

So how do we tell Google Mock that `GetDomainOwner()` can be called with some other arguments as well? The standard technique is to add a "catch all" `EXPECT_CALL`:

```
  EXPECT_CALL(mock_registry, GetDomainOwner(_))
        .Times(AnyNumber());  // catches all other calls to this method.
  EXPECT_CALL(mock_registry, GetDomainOwner("google.com"))
        .WillRepeatedly(Return("Larry Page"));
```

Remember that `_` is the wildcard matcher that matches anything. With this, if `GetDomainOwner("google.com")` is called, it will do what the second `EXPECT_CALL` says; if it is called with a different argument, it will do what the first `EXPECT_CALL` says.

Note that the order of the two `EXPECT_CALLs` is important, as a newer `EXPECT_CALL` takes precedence over an older one.

For more on uninteresting calls, nice mocks, and strict mocks, read ["The Nice, the Strict, and the Naggy"](#the-nice-the-strict-and-the-naggy).

## Expecting Ordered Calls ##

Although an `EXPECT_CALL()` statement defined earlier takes precedence
when Google Mock tries to match a function call with an expectation,
by default calls don't have to happen in the order `EXPECT_CALL()`
statements are written. For example, if the arguments match the
matchers in the third `EXPECT_CALL()`, but not those in the first two,
then the third expectation will be used.

If you would rather have all calls occur in the order of the
expectations, put the `EXPECT_CALL()` statements in a block where you
define a variable of type `InSequence`:

```
  using ::testing::_;
  using ::testing::InSequence;

  {
    InSequence s;

    EXPECT_CALL(foo, DoThis(5));
    EXPECT_CALL(bar, DoThat(_))
        .Times(2);
    EXPECT_CALL(foo, DoThis(6));
  }
```

In this example, we expect a call to `foo.DoThis(5)`, followed by two
calls to `bar.DoThat()` where the argument can be anything, which are
in turn followed by a call to `foo.DoThis(6)`. If a call occurred
out-of-order, Google Mock will report an error.

## Expecting Partially Ordered Calls ##

Sometimes requiring everything to occur in a predetermined order can
lead to brittle tests. For example, we may care about `A` occurring
before both `B` and `C`, but aren't interested in the relative order
of `B` and `C`. In this case, the test should reflect our real intent,
instead of being overly constraining.

Google Mock allows you to impose an arbitrary DAG (directed acyclic
graph) on the calls. One way to express the DAG is to use the
[After](CheatSheet.md#the-after-clause) clause of `EXPECT_CALL`.

Another way is via the `InSequence()` clause (not the same as the
`InSequence` class), which we borrowed from jMock 2. It's less
flexible than `After()`, but more convenient when you have long chains
of sequential calls, as it doesn't require you to come up with
different names for the expectations in the chains.  Here's how it
works:

If we view `EXPECT_CALL()` statements as nodes in a graph, and add an
edge from node A to node B wherever A must occur before B, we can get
a DAG. We use the term "sequence" to mean a directed path in this
DAG. Now, if we decompose the DAG into sequences, we just need to know
which sequences each `EXPECT_CALL()` belongs to in order to be able to
reconstruct the orginal DAG.

So, to specify the partial order on the expectations we need to do two
things: first to define some `Sequence` objects, and then for each
`EXPECT_CALL()` say which `Sequence` objects it is part
of. Expectations in the same sequence must occur in the order they are
written. For example,

```
  using ::testing::Sequence;

  Sequence s1, s2;

  EXPECT_CALL(foo, A())
      .InSequence(s1, s2);
  EXPECT_CALL(bar, B())
      .InSequence(s1);
  EXPECT_CALL(bar, C())
      .InSequence(s2);
  EXPECT_CALL(foo, D())
      .InSequence(s2);
```

specifies the following DAG (where `s1` is `A -> B`, and `s2` is `A ->
C -> D`):

```
       +---> B
       |
  A ---|
       |
       +---> C ---> D
```

This means that A must occur before B and C, and C must occur before
D. There's no restriction about the order other than these.

## Controlling When an Expectation Retires ##

When a mock method is called, Google Mock only consider expectations
that are still active. An expectation is active when created, and
becomes inactive (aka _retires_) when a call that has to occur later
has occurred. For example, in

```
  using ::testing::_;
  using ::testing::Sequence;

  Sequence s1, s2;

  EXPECT_CALL(log, Log(WARNING, _, "File too large."))     // #1
      .Times(AnyNumber())
      .InSequence(s1, s2);
  EXPECT_CALL(log, Log(WARNING, _, "Data set is empty."))  // #2
      .InSequence(s1);
  EXPECT_CALL(log, Log(WARNING, _, "User not found."))     // #3
      .InSequence(s2);
```

as soon as either #2 or #3 is matched, #1 will retire. If a warning
`"File too large."` is logged after this, it will be an error.

Note that an expectation doesn't retire automatically when it's
saturated. For example,

```
using ::testing::_;
...
  EXPECT_CALL(log, Log(WARNING, _, _));                  // #1
  EXPECT_CALL(log, Log(WARNING, _, "File too large."));  // #2
```

says that there will be exactly one warning with the message `"File
too large."`. If the second warning contains this message too, #2 will
match again and result in an upper-bound-violated error.

If this is not what you want, you can ask an expectation to retire as
soon as it becomes saturated:

```
using ::testing::_;
...
  EXPECT_CALL(log, Log(WARNING, _, _));                 // #1
  EXPECT_CALL(log, Log(WARNING, _, "File too large."))  // #2
      .RetiresOnSaturation();
```

Here #2 can be used only once, so if you have two warnings with the
message `"File too large."`, the first will match #2 and the second
will match #1 - there will be no error.

# Using Actions #

## Returning References from Mock Methods ##

If a mock function's return type is a reference, you need to use
`ReturnRef()` instead of `Return()` to return a result:

```
using ::testing::ReturnRef;

class MockFoo : public Foo {
 public:
  MOCK_METHOD0(GetBar, Bar&());
};
...

  MockFoo foo;
  Bar bar;
  EXPECT_CALL(foo, GetBar())
      .WillOnce(ReturnRef(bar));
```

## Returning Live Values from Mock Methods ##

The `Return(x)` action saves a copy of `x` when the action is
_created_, and always returns the same value whenever it's
executed. Sometimes you may want to instead return the _live_ value of
`x` (i.e. its value at the time when the action is _executed_.).

If the mock function's return type is a reference, you can do it using
`ReturnRef(x)`, as shown in the previous recipe ("Returning References
from Mock Methods"). However, Google Mock doesn't let you use
`ReturnRef()` in a mock function whose return type is not a reference,
as doing that usually indicates a user error. So, what shall you do?

You may be tempted to try `ByRef()`:

```
using testing::ByRef;
using testing::Return;

class MockFoo : public Foo {
 public:
  MOCK_METHOD0(GetValue, int());
};
...
  int x = 0;
  MockFoo foo;
  EXPECT_CALL(foo, GetValue())
      .WillRepeatedly(Return(ByRef(x)));
  x = 42;
  EXPECT_EQ(42, foo.GetValue());
```

Unfortunately, it doesn't work here. The above code will fail with error:

```
Value of: foo.GetValue()
  Actual: 0
Expected: 42
```

The reason is that `Return(value)` converts `value` to the actual
return type of the mock function at the time when the action is
_created_, not when it is _executed_. (This behavior was chosen for
the action to be safe when `value` is a proxy object that references
some temporary objects.) As a result, `ByRef(x)` is converted to an
`int` value (instead of a `const int&`) when the expectation is set,
and `Return(ByRef(x))` will always return 0.

`ReturnPointee(pointer)` was provided to solve this problem
specifically. It returns the value pointed to by `pointer` at the time
the action is _executed_:

```
using testing::ReturnPointee;
...
  int x = 0;
  MockFoo foo;
  EXPECT_CALL(foo, GetValue())
      .WillRepeatedly(ReturnPointee(&x));  // Note the & here.
  x = 42;
  EXPECT_EQ(42, foo.GetValue());  // This will succeed now.
```

## Combining Actions ##

Want to do more than one thing when a function is called? That's
fine. `DoAll()` allow you to do sequence of actions every time. Only
the return value of the last action in the sequence will be used.

```
using ::testing::DoAll;

class MockFoo : public Foo {
 public:
  MOCK_METHOD1(Bar, bool(int n));
};
...

  EXPECT_CALL(foo, Bar(_))
      .WillOnce(DoAll(action_1,
                      action_2,
                      ...
                      action_n));
```

## Mocking Side Effects ##

Sometimes a method exhibits its effect not via returning a value but
via side effects. For example, it may change some global state or
modify an output argument. To mock side effects, in general you can
define your own action by implementing `::testing::ActionInterface`.

If all you need to do is to change an output argument, the built-in
`SetArgPointee()` action is convenient:

```
using ::testing::SetArgPointee;

class MockMutator : public Mutator {
 public:
  MOCK_METHOD2(Mutate, void(bool mutate, int* value));
  ...
};
...

  MockMutator mutator;
  EXPECT_CALL(mutator, Mutate(true, _))
      .WillOnce(SetArgPointee<1>(5));
```

In this example, when `mutator.Mutate()` is called, we will assign 5
to the `int` variable pointed to by argument #1
(0-based).

`SetArgPointee()` conveniently makes an internal copy of the
value you pass to it, removing the need to keep the value in scope and
alive. The implication however is that the value must have a copy
constructor and assignment operator.

If the mock method also needs to return a value as well, you can chain
`SetArgPointee()` with `Return()` using `DoAll()`:

```
using ::testing::_;
using ::testing::Return;
using ::testing::SetArgPointee;

class MockMutator : public Mutator {
 public:
  ...
  MOCK_METHOD1(MutateInt, bool(int* value));
};
...

  MockMutator mutator;
  EXPECT_CALL(mutator, MutateInt(_))
      .WillOnce(DoAll(SetArgPointee<0>(5),
                      Return(true)));
```

If the output argument is an array, use the
`SetArrayArgument<N>(first, last)` action instead. It copies the
elements in source range `[first, last)` to the array pointed to by
the `N`-th (0-based) argument:

```
using ::testing::NotNull;
using ::testing::SetArrayArgument;

class MockArrayMutator : public ArrayMutator {
 public:
  MOCK_METHOD2(Mutate, void(int* values, int num_values));
  ...
};
...

  MockArrayMutator mutator;
  int values[5] = { 1, 2, 3, 4, 5 };
  EXPECT_CALL(mutator, Mutate(NotNull(), 5))
      .WillOnce(SetArrayArgument<0>(values, values + 5));
```

This also works when the argument is an output iterator:

```
using ::testing::_;
using ::testing::SetArrayArgument;

class MockRolodex : public Rolodex {
 public:
  MOCK_METHOD1(GetNames, void(std::back_insert_iterator<vector<string> >));
  ...
};
...

  MockRolodex rolodex;
  vector<string> names;
  names.push_back("George");
  names.push_back("John");
  names.push_back("Thomas");
  EXPECT_CALL(rolodex, GetNames(_))
      .WillOnce(SetArrayArgument<0>(names.begin(), names.end()));
```

## Changing a Mock Object's Behavior Based on the State ##

If you expect a call to change the behavior of a mock object, you can use `::testing::InSequence` to specify different behaviors before and after the call:

```
using ::testing::InSequence;
using ::testing::Return;

...
  {
    InSequence seq;
    EXPECT_CALL(my_mock, IsDirty())
        .WillRepeatedly(Return(true));
    EXPECT_CALL(my_mock, Flush());
    EXPECT_CALL(my_mock, IsDirty())
        .WillRepeatedly(Return(false));
  }
  my_mock.FlushIfDirty();
```

This makes `my_mock.IsDirty()` return `true` before `my_mock.Flush()` is called and return `false` afterwards.

If the behavior change is more complex, you can store the effects in a variable and make a mock method get its return value from that variable:

```
using ::testing::_;
using ::testing::SaveArg;
using ::testing::Return;

ACTION_P(ReturnPointee, p) { return *p; }
...
  int previous_value = 0;
  EXPECT_CALL(my_mock, GetPrevValue())
      .WillRepeatedly(ReturnPointee(&previous_value));
  EXPECT_CALL(my_mock, UpdateValue(_))
      .WillRepeatedly(SaveArg<0>(&previous_value));
  my_mock.DoSomethingToUpdateValue();
```

Here `my_mock.GetPrevValue()` will always return the argument of the last `UpdateValue()` call.

## Setting the Default Value for a Return Type ##

If a mock method's return type is a built-in C++ type or pointer, by
default it will return 0 when invoked. Also, in C++ 11 and above, a mock
method whose return type has a default constructor will return a default-constructed
value by default.  You only need to specify an
action if this default value doesn't work for you.

Sometimes, you may want to change this default value, or you may want
to specify a default value for types Google Mock doesn't know
about. You can do this using the `::testing::DefaultValue` class
template:

```
class MockFoo : public Foo {
 public:
  MOCK_METHOD0(CalculateBar, Bar());
};
...

  Bar default_bar;
  // Sets the default return value for type Bar.
  DefaultValue<Bar>::Set(default_bar);

  MockFoo foo;

  // We don't need to specify an action here, as the default
  // return value works for us.
  EXPECT_CALL(foo, CalculateBar());

  foo.CalculateBar();  // This should return default_bar.

  // Unsets the default return value.
  DefaultValue<Bar>::Clear();
```

Please note that changing the default value for a type can make you
tests hard to understand. We recommend you to use this feature
judiciously. For example, you may want to make sure the `Set()` and
`Clear()` calls are right next to the code that uses your mock.

## Setting the Default Actions for a Mock Method ##

You've learned how to change the default value of a given
type. However, this may be too coarse for your purpose: perhaps you
have two mock methods with the same return type and you want them to
have different behaviors. The `ON_CALL()` macro allows you to
customize your mock's behavior at the method level:

```
using ::testing::_;
using ::testing::AnyNumber;
using ::testing::Gt;
using ::testing::Return;
...
  ON_CALL(foo, Sign(_))
      .WillByDefault(Return(-1));
  ON_CALL(foo, Sign(0))
      .WillByDefault(Return(0));
  ON_CALL(foo, Sign(Gt(0)))
      .WillByDefault(Return(1));

  EXPECT_CALL(foo, Sign(_))
      .Times(AnyNumber());

  foo.Sign(5);   // This should return 1.
  foo.Sign(-9);  // This should return -1.
  foo.Sign(0);   // This should return 0.
```

As you may have guessed, when there are more than one `ON_CALL()`
statements, the news order take precedence over the older ones. In
other words, the **last** one that matches the function arguments will
be used. This matching order allows you to set up the common behavior
in a mock object's constructor or the test fixture's set-up phase and
specialize the mock's behavior later.

## Using Functions/Methods/Functors as Actions ##

If the built-in actions don't suit you, you can easily use an existing
function, method, or functor as an action:

```
using ::testing::_;
using ::testing::Invoke;

class MockFoo : public Foo {
 public:
  MOCK_METHOD2(Sum, int(int x, int y));
  MOCK_METHOD1(ComplexJob, bool(int x));
};

int CalculateSum(int x, int y) { return x + y; }

class Helper {
 public:
  bool ComplexJob(int x);
};
...

  MockFoo foo;
  Helper helper;
  EXPECT_CALL(foo, Sum(_, _))
      .WillOnce(Invoke(CalculateSum));
  EXPECT_CALL(foo, ComplexJob(_))
      .WillOnce(Invoke(&helper, &Helper::ComplexJob));

  foo.Sum(5, 6);       // Invokes CalculateSum(5, 6).
  foo.ComplexJob(10);  // Invokes helper.ComplexJob(10);
```

The only requirement is that the type of the function, etc must be
_compatible_ with the signature of the mock function, meaning that the
latter's arguments can be implicitly converted to the corresponding
arguments of the former, and the former's return type can be
implicitly converted to that of the latter. So, you can invoke
something whose type is _not_ exactly the same as the mock function,
as long as it's safe to do so - nice, huh?

## Invoking a Function/Method/Functor Without Arguments ##

`Invoke()` is very useful for doing actions that are more complex. It
passes the mock function's arguments to the function or functor being
invoked such that the callee has the full context of the call to work
with. If the invoked function is not interested in some or all of the
arguments, it can simply ignore them.

Yet, a common pattern is that a test author wants to invoke a function
without the arguments of the mock function. `Invoke()` allows her to
do that using a wrapper function that throws away the arguments before
invoking an underlining nullary function. Needless to say, this can be
tedious and obscures the intent of the test.

`InvokeWithoutArgs()` solves this problem. It's like `Invoke()` except
that it doesn't pass the mock function's arguments to the
callee. Here's an example:

```
using ::testing::_;
using ::testing::InvokeWithoutArgs;

class MockFoo : public Foo {
 public:
  MOCK_METHOD1(ComplexJob, bool(int n));
};

bool Job1() { ... }
...

  MockFoo foo;
  EXPECT_CALL(foo, ComplexJob(_))
      .WillOnce(InvokeWithoutArgs(Job1));

  foo.ComplexJob(10);  // Invokes Job1().
```

## Invoking an Argument of the Mock Function ##

Sometimes a mock function will receive a function pointer or a functor
(in other words, a "callable") as an argument, e.g.

```
class MockFoo : public Foo {
 public:
  MOCK_METHOD2(DoThis, bool(int n, bool (*fp)(int)));
};
```

and you may want to invoke this callable argument:

```
using ::testing::_;
...
  MockFoo foo;
  EXPECT_CALL(foo, DoThis(_, _))
      .WillOnce(...);
  // Will execute (*fp)(5), where fp is the
  // second argument DoThis() receives.
```

Arghh, you need to refer to a mock function argument but your version
of C++ has no lambdas, so you have to define your own action. :-(
Or do you really?

Well, Google Mock has an action to solve _exactly_ this problem:

```
  InvokeArgument<N>(arg_1, arg_2, ..., arg_m)
```

will invoke the `N`-th (0-based) argument the mock function receives,
with `arg_1`, `arg_2`, ..., and `arg_m`. No matter if the argument is
a function pointer or a functor, Google Mock handles them both.

With that, you could write:

```
using ::testing::_;
using ::testing::InvokeArgument;
...
  EXPECT_CALL(foo, DoThis(_, _))
      .WillOnce(InvokeArgument<1>(5));
  // Will execute (*fp)(5), where fp is the
  // second argument DoThis() receives.
```

What if the callable takes an argument by reference? No problem - just
wrap it inside `ByRef()`:

```
...
  MOCK_METHOD1(Bar, bool(bool (*fp)(int, const Helper&)));
...
using ::testing::_;
using ::testing::ByRef;
using ::testing::InvokeArgument;
...

  MockFoo foo;
  Helper helper;
  ...
  EXPECT_CALL(foo, Bar(_))
      .WillOnce(InvokeArgument<0>(5, ByRef(helper)));
  // ByRef(helper) guarantees that a reference to helper, not a copy of it,
  // will be passed to the callable.
```

What if the callable takes an argument by reference and we do **not**
wrap the argument in `ByRef()`? Then `InvokeArgument()` will _make a
copy_ of the argument, and pass a _reference to the copy_, instead of
a reference to the original value, to the callable. This is especially
handy when the argument is a temporary value:

```
...
  MOCK_METHOD1(DoThat, bool(bool (*f)(const double& x, const string& s)));
...
using ::testing::_;
using ::testing::InvokeArgument;
...

  MockFoo foo;
  ...
  EXPECT_CALL(foo, DoThat(_))
      .WillOnce(InvokeArgument<0>(5.0, string("Hi")));
  // Will execute (*f)(5.0, string("Hi")), where f is the function pointer
  // DoThat() receives.  Note that the values 5.0 and string("Hi") are
  // temporary and dead once the EXPECT_CALL() statement finishes.  Yet
  // it's fine to perform this action later, since a copy of the values
  // are kept inside the InvokeArgument action.
```

## Ignoring an Action's Result ##

Sometimes you have an action that returns _something_, but you need an
action that returns `void` (perhaps you want to use it in a mock
function that returns `void`, or perhaps it needs to be used in
`DoAll()` and it's not the last in the list). `IgnoreResult()` lets
you do that. For example:

```
using ::testing::_;
using ::testing::Invoke;
using ::testing::Return;

int Process(const MyData& data);
string DoSomething();

class MockFoo : public Foo {
 public:
  MOCK_METHOD1(Abc, void(const MyData& data));
  MOCK_METHOD0(Xyz, bool());
};
...

  MockFoo foo;
  EXPECT_CALL(foo, Abc(_))
  // .WillOnce(Invoke(Process));
  // The above line won't compile as Process() returns int but Abc() needs
  // to return void.
      .WillOnce(IgnoreResult(Invoke(Process)));

  EXPECT_CALL(foo, Xyz())
      .WillOnce(DoAll(IgnoreResult(Invoke(DoSomething)),
      // Ignores the string DoSomething() returns.
                      Return(true)));
```

Note that you **cannot** use `IgnoreResult()` on an action that already
returns `void`. Doing so will lead to ugly compiler errors.

## Selecting an Action's Arguments ##

Say you have a mock function `Foo()` that takes seven arguments, and
you have a custom action that you want to invoke when `Foo()` is
called. Trouble is, the custom action only wants three arguments:

```
using ::testing::_;
using ::testing::Invoke;
...
  MOCK_METHOD7(Foo, bool(bool visible, const string& name, int x, int y,
                         const map<pair<int, int>, double>& weight,
                         double min_weight, double max_wight));
...

bool IsVisibleInQuadrant1(bool visible, int x, int y) {
  return visible && x >= 0 && y >= 0;
}
...

  EXPECT_CALL(mock, Foo(_, _, _, _, _, _, _))
      .WillOnce(Invoke(IsVisibleInQuadrant1));  // Uh, won't compile. :-(
```

To please the compiler God, you can to define an "adaptor" that has
the same signature as `Foo()` and calls the custom action with the
right arguments:

```
using ::testing::_;
using ::testing::Invoke;

bool MyIsVisibleInQuadrant1(bool visible, const string& name, int x, int y,
                            const map<pair<int, int>, double>& weight,
                            double min_weight, double max_wight) {
  return IsVisibleInQuadrant1(visible, x, y);
}
...

  EXPECT_CALL(mock, Foo(_, _, _, _, _, _, _))
      .WillOnce(Invoke(MyIsVisibleInQuadrant1));  // Now it works.
```

But isn't this awkward?

Google Mock provides a generic _action adaptor_, so you can spend your
time minding more important business than writing your own
adaptors. Here's the syntax:

```
  WithArgs<N1, N2, ..., Nk>(action)
```

creates an action that passes the arguments of the mock function at
the given indices (0-based) to the inner `action` and performs
it. Using `WithArgs`, our original example can be written as:

```
using ::testing::_;
using ::testing::Invoke;
using ::testing::WithArgs;
...
  EXPECT_CALL(mock, Foo(_, _, _, _, _, _, _))
      .WillOnce(WithArgs<0, 2, 3>(Invoke(IsVisibleInQuadrant1)));
      // No need to define your own adaptor.
```

For better readability, Google Mock also gives you:

  * `WithoutArgs(action)` when the inner `action` takes _no_ argument, and
  * `WithArg<N>(action)` (no `s` after `Arg`) when the inner `action` takes _one_ argument.

As you may have realized, `InvokeWithoutArgs(...)` is just syntactic
sugar for `WithoutArgs(Invoke(...))`.

Here are more tips:

  * The inner action used in `WithArgs` and friends does not have to be `Invoke()` -- it can be anything.
  * You can repeat an argument in the argument list if necessary, e.g. `WithArgs<2, 3, 3, 5>(...)`.
  * You can change the order of the arguments, e.g. `WithArgs<3, 2, 1>(...)`.
  * The types of the selected arguments do _not_ have to match the signature of the inner action exactly. It works as long as they can be implicitly converted to the corresponding arguments of the inner action. For example, if the 4-th argument of the mock function is an `int` and `my_action` takes a `double`, `WithArg<4>(my_action)` will work.

## Ignoring Arguments in Action Functions ##

The selecting-an-action's-arguments recipe showed us one way to make a
mock function and an action with incompatible argument lists fit
together. The downside is that wrapping the action in
`WithArgs<...>()` can get tedious for people writing the tests.

If you are defining a function, method, or functor to be used with
`Invoke*()`, and you are not interested in some of its arguments, an
alternative to `WithArgs` is to declare the uninteresting arguments as
`Unused`. This makes the definition less cluttered and less fragile in
case the types of the uninteresting arguments change. It could also
increase the chance the action function can be reused. For example,
given

```
  MOCK_METHOD3(Foo, double(const string& label, double x, double y));
  MOCK_METHOD3(Bar, double(int index, double x, double y));
```

instead of

```
using ::testing::_;
using ::testing::Invoke;

double DistanceToOriginWithLabel(const string& label, double x, double y) {
  return sqrt(x*x + y*y);
}

double DistanceToOriginWithIndex(int index, double x, double y) {
  return sqrt(x*x + y*y);
}
...

  EXEPCT_CALL(mock, Foo("abc", _, _))
      .WillOnce(Invoke(DistanceToOriginWithLabel));
  EXEPCT_CALL(mock, Bar(5, _, _))
      .WillOnce(Invoke(DistanceToOriginWithIndex));
```

you could write

```
using ::testing::_;
using ::testing::Invoke;
using ::testing::Unused;

double DistanceToOrigin(Unused, double x, double y) {
  return sqrt(x*x + y*y);
}
...

  EXEPCT_CALL(mock, Foo("abc", _, _))
      .WillOnce(Invoke(DistanceToOrigin));
  EXEPCT_CALL(mock, Bar(5, _, _))
      .WillOnce(Invoke(DistanceToOrigin));
```

## Sharing Actions ##

Just like matchers, a Google Mock action object consists of a pointer
to a ref-counted implementation object. Therefore copying actions is
also allowed and very efficient. When the last action that references
the implementation object dies, the implementation object will be
deleted.

If you have some complex action that you want to use again and again,
you may not have to build it from scratch everytime. If the action
doesn't have an internal state (i.e. if it always does the same thing
no matter how many times it has been called), you can assign it to an
action variable and use that variable repeatedly. For example:

```
  Action<bool(int*)> set_flag = DoAll(SetArgPointee<0>(5),
                                      Return(true));
  ... use set_flag in .WillOnce() and .WillRepeatedly() ...
```

However, if the action has its own state, you may be surprised if you
share the action object. Suppose you have an action factory
`IncrementCounter(init)` which creates an action that increments and
returns a counter whose initial value is `init`, using two actions
created from the same expression and using a shared action will
exihibit different behaviors. Example:

```
  EXPECT_CALL(foo, DoThis())
      .WillRepeatedly(IncrementCounter(0));
  EXPECT_CALL(foo, DoThat())
      .WillRepeatedly(IncrementCounter(0));
  foo.DoThis();  // Returns 1.
  foo.DoThis();  // Returns 2.
  foo.DoThat();  // Returns 1 - Blah() uses a different
                 // counter than Bar()'s.
```

versus

```
  Action<int()> increment = IncrementCounter(0);

  EXPECT_CALL(foo, DoThis())
      .WillRepeatedly(increment);
  EXPECT_CALL(foo, DoThat())
      .WillRepeatedly(increment);
  foo.DoThis();  // Returns 1.
  foo.DoThis();  // Returns 2.
  foo.DoThat();  // Returns 3 - the counter is shared.
```

# Misc Recipes on Using Google Mock #

## Mocking Methods That Use Move-Only Types ##

C++11 introduced <em>move-only types</em>.  A move-only-typed value can be moved from one object to another, but cannot be copied.  `std::unique_ptr<T>` is probably the most commonly used move-only type.

Mocking a method that takes and/or returns move-only types presents some challenges, but nothing insurmountable.  This recipe shows you how you can do it.

Let’s say we are working on a fictional project that lets one post and share snippets called “buzzes”.  Your code uses these types:

```
enum class AccessLevel { kInternal, kPublic };

class Buzz {
 public:
  explicit Buzz(AccessLevel access) { … }
  ...
};

class Buzzer {
 public:
  virtual ~Buzzer() {}
  virtual std::unique_ptr<Buzz> MakeBuzz(const std::string& text) = 0;
  virtual bool ShareBuzz(std::unique_ptr<Buzz> buzz, Time timestamp) = 0;
  ...
};
```

A `Buzz` object represents a snippet being posted.  A class that implements the `Buzzer` interface is capable of creating and sharing `Buzz`.  Methods in `Buzzer` may return a `unique_ptr<Buzz>` or take a `unique_ptr<Buzz>`.  Now we need to mock `Buzzer` in our tests.

To mock a method that returns a move-only type, you just use the familiar `MOCK_METHOD` syntax as usual:

```
class MockBuzzer : public Buzzer {
 public:
  MOCK_METHOD1(MakeBuzz, std::unique_ptr<Buzz>(const std::string& text));
  …
};
```

However, if you attempt to use the same `MOCK_METHOD` pattern to mock a method that takes a move-only parameter, you’ll get a compiler error currently:

```
  // Does NOT compile!
  MOCK_METHOD2(ShareBuzz, bool(std::unique_ptr<Buzz> buzz, Time timestamp));
```

While it’s highly desirable to make this syntax just work, it’s not trivial and the work hasn’t been done yet.  Fortunately, there is a trick you can apply today to get something that works nearly as well as this.

The trick, is to delegate the `ShareBuzz()` method to a mock method (let’s call it `DoShareBuzz()`) that does not take move-only parameters:

```
class MockBuzzer : public Buzzer {
 public:
  MOCK_METHOD1(MakeBuzz, std::unique_ptr<Buzz>(const std::string& text));
  MOCK_METHOD2(DoShareBuzz, bool(Buzz* buzz, Time timestamp));
  bool ShareBuzz(std::unique_ptr<Buzz> buzz, Time timestamp) {
    return DoShareBuzz(buzz.get(), timestamp);
  }
};
```

Note that there's no need to define or declare `DoShareBuzz()` in a base class.  You only need to define it as a `MOCK_METHOD` in the mock class.

Now that we have the mock class defined, we can use it in tests.  In the following code examples, we assume that we have defined a `MockBuzzer` object named `mock_buzzer_`:

```
  MockBuzzer mock_buzzer_;
```

First let’s see how we can set expectations on the `MakeBuzz()` method, which returns a `unique_ptr<Buzz>`.

As usual, if you set an expectation without an action (i.e. the `.WillOnce()` or `.WillRepeated()` clause), when that expectation fires, the default action for that method will be taken.  Since `unique_ptr<>` has a default constructor that returns a null `unique_ptr`, that’s what you’ll get if you don’t specify an action:

```
  // Use the default action.
  EXPECT_CALL(mock_buzzer_, MakeBuzz("hello"));

  // Triggers the previous EXPECT_CALL.
  EXPECT_EQ(nullptr, mock_buzzer_.MakeBuzz("hello"));
```

If you are not happy with the default action, you can tweak it.  Depending on what you need, you may either tweak the default action for a specific (mock object, mock method) combination using `ON_CALL()`, or you may tweak the default action for all mock methods that return a specific type.  The usage of `ON_CALL()` is similar to `EXPECT_CALL()`, so we’ll skip it and just explain how to do the latter (tweaking the default action for a specific return type).  You do this via the `DefaultValue<>::SetFactory()` and `DefaultValue<>::Clear()` API:

```
  // Sets the default action for return type std::unique_ptr<Buzz> to
  // creating a new Buzz every time.
  DefaultValue<std::unique_ptr<Buzz>>::SetFactory(
      [] { return MakeUnique<Buzz>(AccessLevel::kInternal); });

  // When this fires, the default action of MakeBuzz() will run, which
  // will return a new Buzz object.
  EXPECT_CALL(mock_buzzer_, MakeBuzz("hello")).Times(AnyNumber());

  auto buzz1 = mock_buzzer_.MakeBuzz("hello");
  auto buzz2 = mock_buzzer_.MakeBuzz("hello");
  EXPECT_NE(nullptr, buzz1);
  EXPECT_NE(nullptr, buzz2);
  EXPECT_NE(buzz1, buzz2);

  // Resets the default action for return type std::unique_ptr<Buzz>,
  // to avoid interfere with other tests.
  DefaultValue<std::unique_ptr<Buzz>>::Clear();
```

What if you want the method to do something other than the default action?  If you just need to return a pre-defined move-only value, you can use the `Return(ByMove(...))` action:

```
  // When this fires, the unique_ptr<> specified by ByMove(...) will
  // be returned.
  EXPECT_CALL(mock_buzzer_, MakeBuzz("world"))
      .WillOnce(Return(ByMove(MakeUnique<Buzz>(AccessLevel::kInternal))));

  EXPECT_NE(nullptr, mock_buzzer_.MakeBuzz("world"));
```

Note that `ByMove()` is essential here - if you drop it, the code won’t compile.

Quiz time!  What do you think will happen if a `Return(ByMove(...))` action is performed more than once (e.g. you write `….WillRepeatedly(Return(ByMove(...)));`)?  Come think of it, after the first time the action runs, the source value will be consumed (since it’s a move-only value), so the next time around, there’s no value to move from -- you’ll get a run-time error that `Return(ByMove(...))` can only be run once.

If you need your mock method to do more than just moving a pre-defined value, remember that you can always use `Invoke()` to call a lambda or a callable object, which can do pretty much anything you want:

```
  EXPECT_CALL(mock_buzzer_, MakeBuzz("x"))
      .WillRepeatedly(Invoke([](const std::string& text) {
        return std::make_unique<Buzz>(AccessLevel::kInternal);
      }));

  EXPECT_NE(nullptr, mock_buzzer_.MakeBuzz("x"));
  EXPECT_NE(nullptr, mock_buzzer_.MakeBuzz("x"));
```

Every time this `EXPECT_CALL` fires, a new `unique_ptr<Buzz>` will be created and returned.  You cannot do this with `Return(ByMove(...))`.

Now there’s one topic we haven’t covered: how do you set expectations on `ShareBuzz()`, which takes a move-only-typed parameter?  The answer is you don’t.  Instead, you set expectations on the `DoShareBuzz()` mock method (remember that we defined a `MOCK_METHOD` for `DoShareBuzz()`, not `ShareBuzz()`):

```
  EXPECT_CALL(mock_buzzer_, DoShareBuzz(NotNull(), _));

  // When one calls ShareBuzz() on the MockBuzzer like this, the call is
  // forwarded to DoShareBuzz(), which is mocked.  Therefore this statement
  // will trigger the above EXPECT_CALL.
  mock_buzzer_.ShareBuzz(MakeUnique<Buzz>(AccessLevel::kInternal),
                         ::base::Now());
```

Some of you may have spotted one problem with this approach: the `DoShareBuzz()` mock method differs from the real `ShareBuzz()` method in that it cannot take ownership of the buzz parameter - `ShareBuzz()` will always delete buzz after `DoShareBuzz()` returns.  What if you need to save the buzz object somewhere for later use when `ShareBuzz()` is called?  Indeed, you'd be stuck.

Another problem with the `DoShareBuzz()` we had is that it can surprise people reading or maintaining the test, as one would expect that `DoShareBuzz()` has (logically) the same contract as `ShareBuzz()`.

Fortunately, these problems can be fixed with a bit more code.  Let's try to get it right this time:

```
class MockBuzzer : public Buzzer {
 public:
  MockBuzzer() {
    // Since DoShareBuzz(buzz, time) is supposed to take ownership of
    // buzz, define a default behavior for DoShareBuzz(buzz, time) to
    // delete buzz.
    ON_CALL(*this, DoShareBuzz(_, _))
        .WillByDefault(Invoke([](Buzz* buzz, Time timestamp) {
          delete buzz;
          return true;
        }));
  }

  MOCK_METHOD1(MakeBuzz, std::unique_ptr<Buzz>(const std::string& text));

  // Takes ownership of buzz.
  MOCK_METHOD2(DoShareBuzz, bool(Buzz* buzz, Time timestamp));
  bool ShareBuzz(std::unique_ptr<Buzz> buzz, Time timestamp) {
    return DoShareBuzz(buzz.release(), timestamp);
  }
};
```

Now, the mock `DoShareBuzz()` method is free to save the buzz argument for later use if this is what you want:

```
  std::unique_ptr<Buzz> intercepted_buzz;
  EXPECT_CALL(mock_buzzer_, DoShareBuzz(NotNull(), _))
      .WillOnce(Invoke([&intercepted_buzz](Buzz* buzz, Time timestamp) {
        // Save buzz in intercepted_buzz for analysis later.
        intercepted_buzz.reset(buzz);
        return false;
      }));

  mock_buzzer_.ShareBuzz(std::make_unique<Buzz>(AccessLevel::kInternal),
                         Now());
  EXPECT_NE(nullptr, intercepted_buzz);
```

Using the tricks covered in this recipe, you are now able to mock methods that take and/or return move-only types.  Put your newly-acquired power to good use - when you design a new API, you can now feel comfortable using `unique_ptrs` as appropriate, without fearing that doing so will compromise your tests.

## Making the Compilation Faster ##

Believe it or not, the _vast majority_ of the time spent on compiling
a mock class is in generating its constructor and destructor, as they
perform non-trivial tasks (e.g. verification of the
expectations). What's more, mock methods with different signatures
have different types and thus their constructors/destructors need to
be generated by the compiler separately. As a result, if you mock many
different types of methods, compiling your mock class can get really
slow.

If you are experiencing slow compilation, you can move the definition
of your mock class' constructor and destructor out of the class body
and into a `.cpp` file. This way, even if you `#include` your mock
class in N files, the compiler only needs to generate its constructor
and destructor once, resulting in a much faster compilation.

Let's illustrate the idea using an example. Here's the definition of a
mock class before applying this recipe:

```
// File mock_foo.h.
...
class MockFoo : public Foo {
 public:
  // Since we don't declare the constructor or the destructor,
  // the compiler will generate them in every translation unit
  // where this mock class is used.

  MOCK_METHOD0(DoThis, int());
  MOCK_METHOD1(DoThat, bool(const char* str));
  ... more mock methods ...
};
```

After the change, it would look like:

```
// File mock_foo.h.
...
class MockFoo : public Foo {
 public:
  // The constructor and destructor are declared, but not defined, here.
  MockFoo();
  virtual ~MockFoo();

  MOCK_METHOD0(DoThis, int());
  MOCK_METHOD1(DoThat, bool(const char* str));
  ... more mock methods ...
};
```
and
```
// File mock_foo.cpp.
#include "path/to/mock_foo.h"

// The definitions may appear trivial, but the functions actually do a
// lot of things through the constructors/destructors of the member
// variables used to implement the mock methods.
MockFoo::MockFoo() {}
MockFoo::~MockFoo() {}
```

## Forcing a Verification ##

When it's being destroyed, your friendly mock object will automatically
verify that all expectations on it have been satisfied, and will
generate [Google Test](../../googletest/) failures
if not. This is convenient as it leaves you with one less thing to
worry about. That is, unless you are not sure if your mock object will
be destroyed.

How could it be that your mock object won't eventually be destroyed?
Well, it might be created on the heap and owned by the code you are
testing. Suppose there's a bug in that code and it doesn't delete the
mock object properly - you could end up with a passing test when
there's actually a bug.

Using a heap checker is a good idea and can alleviate the concern, but
its implementation may not be 100% reliable. So, sometimes you do want
to _force_ Google Mock to verify a mock object before it is
(hopefully) destructed. You can do this with
`Mock::VerifyAndClearExpectations(&mock_object)`:

```
TEST(MyServerTest, ProcessesRequest) {
  using ::testing::Mock;

  MockFoo* const foo = new MockFoo;
  EXPECT_CALL(*foo, ...)...;
  // ... other expectations ...

  // server now owns foo.
  MyServer server(foo);
  server.ProcessRequest(...);

  // In case that server's destructor will forget to delete foo,
  // this will verify the expectations anyway.
  Mock::VerifyAndClearExpectations(foo);
}  // server is destroyed when it goes out of scope here.
```

**Tip:** The `Mock::VerifyAndClearExpectations()` function returns a
`bool` to indicate whether the verification was successful (`true` for
yes), so you can wrap that function call inside a `ASSERT_TRUE()` if
there is no point going further when the verification has failed.

## Using Check Points ##

Sometimes you may want to "reset" a mock object at various check
points in your test: at each check point, you verify that all existing
expectations on the mock object have been satisfied, and then you set
some new expectations on it as if it's newly created. This allows you
to work with a mock object in "phases" whose sizes are each
manageable.

One such scenario is that in your test's `SetUp()` function, you may
want to put the object you are testing into a certain state, with the
help from a mock object. Once in the desired state, you want to clear
all expectations on the mock, such that in the `TEST_F` body you can
set fresh expectations on it.

As you may have figured out, the `Mock::VerifyAndClearExpectations()`
function we saw in the previous recipe can help you here. Or, if you
are using `ON_CALL()` to set default actions on the mock object and
want to clear the default actions as well, use
`Mock::VerifyAndClear(&mock_object)` instead. This function does what
`Mock::VerifyAndClearExpectations(&mock_object)` does and returns the
same `bool`, **plus** it clears the `ON_CALL()` statements on
`mock_object` too.

Another trick you can use to achieve the same effect is to put the
expectations in sequences and insert calls to a dummy "check-point"
function at specific places. Then you can verify that the mock
function calls do happen at the right time. For example, if you are
exercising code:

```
Foo(1);
Foo(2);
Foo(3);
```

and want to verify that `Foo(1)` and `Foo(3)` both invoke
`mock.Bar("a")`, but `Foo(2)` doesn't invoke anything. You can write:

```
using ::testing::MockFunction;

TEST(FooTest, InvokesBarCorrectly) {
  MyMock mock;
  // Class MockFunction<F> has exactly one mock method.  It is named
  // Call() and has type F.
  MockFunction<void(string check_point_name)> check;
  {
    InSequence s;

    EXPECT_CALL(mock, Bar("a"));
    EXPECT_CALL(check, Call("1"));
    EXPECT_CALL(check, Call("2"));
    EXPECT_CALL(mock, Bar("a"));
  }
  Foo(1);
  check.Call("1");
  Foo(2);
  check.Call("2");
  Foo(3);
}
```

The expectation spec says that the first `Bar("a")` must happen before
check point "1", the second `Bar("a")` must happen after check point "2",
and nothing should happen between the two check points. The explicit
check points make it easy to tell which `Bar("a")` is called by which
call to `Foo()`.

## Mocking Destructors ##

Sometimes you want to make sure a mock object is destructed at the
right time, e.g. after `bar->A()` is called but before `bar->B()` is
called. We already know that you can specify constraints on the order
of mock function calls, so all we need to do is to mock the destructor
of the mock function.

This sounds simple, except for one problem: a destructor is a special
function with special syntax and special semantics, and the
`MOCK_METHOD0` macro doesn't work for it:

```
  MOCK_METHOD0(~MockFoo, void());  // Won't compile!
```

The good news is that you can use a simple pattern to achieve the same
effect. First, add a mock function `Die()` to your mock class and call
it in the destructor, like this:

```
class MockFoo : public Foo {
  ...
  // Add the following two lines to the mock class.
  MOCK_METHOD0(Die, void());
  virtual ~MockFoo() { Die(); }
};
```

(If the name `Die()` clashes with an existing symbol, choose another
name.) Now, we have translated the problem of testing when a `MockFoo`
object dies to testing when its `Die()` method is called:

```
  MockFoo* foo = new MockFoo;
  MockBar* bar = new MockBar;
  ...
  {
    InSequence s;

    // Expects *foo to die after bar->A() and before bar->B().
    EXPECT_CALL(*bar, A());
    EXPECT_CALL(*foo, Die());
    EXPECT_CALL(*bar, B());
  }
```

And that's that.

## Using Google Mock and Threads ##

**IMPORTANT NOTE:** What we describe in this recipe is **ONLY** true on
platforms where Google Mock is thread-safe. Currently these are only
platforms that support the pthreads library (this includes Linux and Mac).
To make it thread-safe on other platforms we only need to implement
some synchronization operations in `"gtest/internal/gtest-port.h"`.

In a **unit** test, it's best if you could isolate and test a piece of
code in a single-threaded context. That avoids race conditions and
dead locks, and makes debugging your test much easier.

Yet many programs are multi-threaded, and sometimes to test something
we need to pound on it from more than one thread. Google Mock works
for this purpose too.

Remember the steps for using a mock:

  1. Create a mock object `foo`.
  1. Set its default actions and expectations using `ON_CALL()` and `EXPECT_CALL()`.
  1. The code under test calls methods of `foo`.
  1. Optionally, verify and reset the mock.
  1. Destroy the mock yourself, or let the code under test destroy it. The destructor will automatically verify it.

If you follow the following simple rules, your mocks and threads can
live happily together:

  * Execute your _test code_ (as opposed to the code being tested) in _one_ thread. This makes your test easy to follow.
  * Obviously, you can do step #1 without locking.
  * When doing step #2 and #5, make sure no other thread is accessing `foo`. Obvious too, huh?
  * #3 and #4 can be done either in one thread or in multiple threads - anyway you want. Google Mock takes care of the locking, so you don't have to do any - unless required by your test logic.

If you violate the rules (for example, if you set expectations on a
mock while another thread is calling its methods), you get undefined
behavior. That's not fun, so don't do it.

Google Mock guarantees that the action for a mock function is done in
the same thread that called the mock function. For example, in

```
  EXPECT_CALL(mock, Foo(1))
      .WillOnce(action1);
  EXPECT_CALL(mock, Foo(2))
      .WillOnce(action2);
```

if `Foo(1)` is called in thread 1 and `Foo(2)` is called in thread 2,
Google Mock will execute `action1` in thread 1 and `action2` in thread
2.

Google Mock does _not_ impose a sequence on actions performed in
different threads (doing so may create deadlocks as the actions may
need to cooperate). This means that the execution of `action1` and
`action2` in the above example _may_ interleave. If this is a problem,
you should add proper synchronization logic to `action1` and `action2`
to make the test thread-safe.


Also, remember that `DefaultValue<T>` is a global resource that
potentially affects _all_ living mock objects in your
program. Naturally, you won't want to mess with it from multiple
threads or when there still are mocks in action.

## Controlling How Much Information Google Mock Prints ##

When Google Mock sees something that has the potential of being an
error (e.g. a mock function with no expectation is called, a.k.a. an
uninteresting call, which is allowed but perhaps you forgot to
explicitly ban the call), it prints some warning messages, including
the arguments of the function and the return value. Hopefully this
will remind you to take a look and see if there is indeed a problem.

Sometimes you are confident that your tests are correct and may not
appreciate such friendly messages. Some other times, you are debugging
your tests or learning about the behavior of the code you are testing,
and wish you could observe every mock call that happens (including
argument values and the return value). Clearly, one size doesn't fit
all.

You can control how much Google Mock tells you using the
`--gmock_verbose=LEVEL` command-line flag, where `LEVEL` is a string
with three possible values:

  * `info`: Google Mock will print all informational messages, warnings, and errors (most verbose). At this setting, Google Mock will also log any calls to the `ON_CALL/EXPECT_CALL` macros.
  * `warning`: Google Mock will print both warnings and errors (less verbose). This is the default.
  * `error`: Google Mock will print errors only (least verbose).

Alternatively, you can adjust the value of that flag from within your
tests like so:

```
  ::testing::FLAGS_gmock_verbose = "error";
```

Now, judiciously use the right flag to enable Google Mock serve you better!

## Gaining Super Vision into Mock Calls ##

You have a test using Google Mock. It fails: Google Mock tells you
that some expectations aren't satisfied. However, you aren't sure why:
Is there a typo somewhere in the matchers? Did you mess up the order
of the `EXPECT_CALL`s? Or is the code under test doing something
wrong?  How can you find out the cause?

Won't it be nice if you have X-ray vision and can actually see the
trace of all `EXPECT_CALL`s and mock method calls as they are made?
For each call, would you like to see its actual argument values and
which `EXPECT_CALL` Google Mock thinks it matches?

You can unlock this power by running your test with the
`--gmock_verbose=info` flag. For example, given the test program:

```
using testing::_;
using testing::HasSubstr;
using testing::Return;

class MockFoo {
 public:
  MOCK_METHOD2(F, void(const string& x, const string& y));
};

TEST(Foo, Bar) {
  MockFoo mock;
  EXPECT_CALL(mock, F(_, _)).WillRepeatedly(Return());
  EXPECT_CALL(mock, F("a", "b"));
  EXPECT_CALL(mock, F("c", HasSubstr("d")));

  mock.F("a", "good");
  mock.F("a", "b");
}
```

if you run it with `--gmock_verbose=info`, you will see this output:

```
[ RUN      ] Foo.Bar

foo_test.cc:14: EXPECT_CALL(mock, F(_, _)) invoked
foo_test.cc:15: EXPECT_CALL(mock, F("a", "b")) invoked
foo_test.cc:16: EXPECT_CALL(mock, F("c", HasSubstr("d"))) invoked
foo_test.cc:14: Mock function call matches EXPECT_CALL(mock, F(_, _))...
    Function call: F(@0x7fff7c8dad40"a", @0x7fff7c8dad10"good")
foo_test.cc:15: Mock function call matches EXPECT_CALL(mock, F("a", "b"))...
    Function call: F(@0x7fff7c8dada0"a", @0x7fff7c8dad70"b")
foo_test.cc:16: Failure
Actual function call count doesn't match EXPECT_CALL(mock, F("c", HasSubstr("d")))...
         Expected: to be called once
           Actual: never called - unsatisfied and active
[  FAILED  ] Foo.Bar
```

Suppose the bug is that the `"c"` in the third `EXPECT_CALL` is a typo
and should actually be `"a"`. With the above message, you should see
that the actual `F("a", "good")` call is matched by the first
`EXPECT_CALL`, not the third as you thought. From that it should be
obvious that the third `EXPECT_CALL` is written wrong. Case solved.

## Running Tests in Emacs ##

If you build and run your tests in Emacs, the source file locations of
Google Mock and [Google Test](../../googletest/)
errors will be highlighted. Just press `<Enter>` on one of them and
you'll be taken to the offending line. Or, you can just type `C-x ``
to jump to the next error.

To make it even easier, you can add the following lines to your
`~/.emacs` file:

```
(global-set-key "\M-m"   'compile)  ; m is for make
(global-set-key [M-down] 'next-error)
(global-set-key [M-up]   '(lambda () (interactive) (next-error -1)))
```

Then you can type `M-m` to start a build, or `M-up`/`M-down` to move
back and forth between errors.

## Fusing Google Mock Source Files ##

Google Mock's implementation consists of dozens of files (excluding
its own tests).  Sometimes you may want them to be packaged up in
fewer files instead, such that you can easily copy them to a new
machine and start hacking there.  For this we provide an experimental
Python script `fuse_gmock_files.py` in the `scripts/` directory
(starting with release 1.2.0).  Assuming you have Python 2.4 or above
installed on your machine, just go to that directory and run
```
python fuse_gmock_files.py OUTPUT_DIR
```

and you should see an `OUTPUT_DIR` directory being created with files
`gtest/gtest.h`, `gmock/gmock.h`, and `gmock-gtest-all.cc` in it.
These three files contain everything you need to use Google Mock (and
Google Test).  Just copy them to anywhere you want and you are ready
to write tests and use mocks.  You can use the
[scrpts/test/Makefile](../scripts/test/Makefile) file as an example on how to compile your tests
against them.

# Extending Google Mock #

## Writing New Matchers Quickly ##

The `MATCHER*` family of macros can be used to define custom matchers
easily.  The syntax:

```
MATCHER(name, description_string_expression) { statements; }
```

will define a matcher with the given name that executes the
statements, which must return a `bool` to indicate if the match
succeeds.  Inside the statements, you can refer to the value being
matched by `arg`, and refer to its type by `arg_type`.

The description string is a `string`-typed expression that documents
what the matcher does, and is used to generate the failure message
when the match fails.  It can (and should) reference the special
`bool` variable `negation`, and should evaluate to the description of
the matcher when `negation` is `false`, or that of the matcher's
negation when `negation` is `true`.

For convenience, we allow the description string to be empty (`""`),
in which case Google Mock will use the sequence of words in the
matcher name as the description.

For example:
```
MATCHER(IsDivisibleBy7, "") { return (arg % 7) == 0; }
```
allows you to write
```
  // Expects mock_foo.Bar(n) to be called where n is divisible by 7.
  EXPECT_CALL(mock_foo, Bar(IsDivisibleBy7()));
```
or,
```
using ::testing::Not;
...
  EXPECT_THAT(some_expression, IsDivisibleBy7());
  EXPECT_THAT(some_other_expression, Not(IsDivisibleBy7()));
```
If the above assertions fail, they will print something like:
```
  Value of: some_expression
  Expected: is divisible by 7
    Actual: 27
...
  Value of: some_other_expression
  Expected: not (is divisible by 7)
    Actual: 21
```
where the descriptions `"is divisible by 7"` and `"not (is divisible
by 7)"` are automatically calculated from the matcher name
`IsDivisibleBy7`.

As you may have noticed, the auto-generated descriptions (especially
those for the negation) may not be so great. You can always override
them with a string expression of your own:
```
MATCHER(IsDivisibleBy7, std::string(negation ? "isn't" : "is") +
                        " divisible by 7") {
  return (arg % 7) == 0;
}
```

Optionally, you can stream additional information to a hidden argument
named `result_listener` to explain the match result. For example, a
better definition of `IsDivisibleBy7` is:
```
MATCHER(IsDivisibleBy7, "") {
  if ((arg % 7) == 0)
    return true;

  *result_listener << "the remainder is " << (arg % 7);
  return false;
}
```

With this definition, the above assertion will give a better message:
```
  Value of: some_expression
  Expected: is divisible by 7
    Actual: 27 (the remainder is 6)
```

You should let `MatchAndExplain()` print _any additional information_
that can help a user understand the match result. Note that it should
explain why the match succeeds in case of a success (unless it's
obvious) - this is useful when the matcher is used inside
`Not()`. There is no need to print the argument value itself, as
Google Mock already prints it for you.

**Notes:**

  1. The type of the value being matched (`arg_type`) is determined by the context in which you use the matcher and is supplied to you by the compiler, so you don't need to worry about declaring it (nor can you).  This allows the matcher to be polymorphic.  For example, `IsDivisibleBy7()` can be used to match any type where the value of `(arg % 7) == 0` can be implicitly converted to a `bool`.  In the `Bar(IsDivisibleBy7())` example above, if method `Bar()` takes an `int`, `arg_type` will be `int`; if it takes an `unsigned long`, `arg_type` will be `unsigned long`; and so on.
  1. Google Mock doesn't guarantee when or how many times a matcher will be invoked. Therefore the matcher logic must be _purely functional_ (i.e. it cannot have any side effect, and the result must not depend on anything other than the value being matched and the matcher parameters). This requirement must be satisfied no matter how you define the matcher (e.g. using one of the methods described in the following recipes). In particular, a matcher can never call a mock function, as that will affect the state of the mock object and Google Mock.

## Writing New Parameterized Matchers Quickly ##

Sometimes you'll want to define a matcher that has parameters.  For that you
can use the macro:
```
MATCHER_P(name, param_name, description_string) { statements; }
```
where the description string can be either `""` or a string expression
that references `negation` and `param_name`.

For example:
```
MATCHER_P(HasAbsoluteValue, value, "") { return abs(arg) == value; }
```
will allow you to write:
```
  EXPECT_THAT(Blah("a"), HasAbsoluteValue(n));
```
which may lead to this message (assuming `n` is 10):
```
  Value of: Blah("a")
  Expected: has absolute value 10
    Actual: -9
```

Note that both the matcher description and its parameter are
printed, making the message human-friendly.

In the matcher definition body, you can write `foo_type` to
reference the type of a parameter named `foo`.  For example, in the
body of `MATCHER_P(HasAbsoluteValue, value)` above, you can write
`value_type` to refer to the type of `value`.

Google Mock also provides `MATCHER_P2`, `MATCHER_P3`, ..., up to
`MATCHER_P10` to support multi-parameter matchers:
```
MATCHER_Pk(name, param_1, ..., param_k, description_string) { statements; }
```

Please note that the custom description string is for a particular
**instance** of the matcher, where the parameters have been bound to
actual values.  Therefore usually you'll want the parameter values to
be part of the description.  Google Mock lets you do that by
referencing the matcher parameters in the description string
expression.

For example,
```
  using ::testing::PrintToString;
  MATCHER_P2(InClosedRange, low, hi,
             std::string(negation ? "isn't" : "is") + " in range [" +
             PrintToString(low) + ", " + PrintToString(hi) + "]") {
    return low <= arg && arg <= hi;
  }
  ...
  EXPECT_THAT(3, InClosedRange(4, 6));
```
would generate a failure that contains the message:
```
  Expected: is in range [4, 6]
```

If you specify `""` as the description, the failure message will
contain the sequence of words in the matcher name followed by the
parameter values printed as a tuple.  For example,
```
  MATCHER_P2(InClosedRange, low, hi, "") { ... }
  ...
  EXPECT_THAT(3, InClosedRange(4, 6));
```
would generate a failure that contains the text:
```
  Expected: in closed range (4, 6)
```

For the purpose of typing, you can view
```
MATCHER_Pk(Foo, p1, ..., pk, description_string) { ... }
```
as shorthand for
```
template <typename p1_type, ..., typename pk_type>
FooMatcherPk<p1_type, ..., pk_type>
Foo(p1_type p1, ..., pk_type pk) { ... }
```

When you write `Foo(v1, ..., vk)`, the compiler infers the types of
the parameters `v1`, ..., and `vk` for you.  If you are not happy with
the result of the type inference, you can specify the types by
explicitly instantiating the template, as in `Foo<long, bool>(5, false)`.
As said earlier, you don't get to (or need to) specify
`arg_type` as that's determined by the context in which the matcher
is used.

You can assign the result of expression `Foo(p1, ..., pk)` to a
variable of type `FooMatcherPk<p1_type, ..., pk_type>`.  This can be
useful when composing matchers.  Matchers that don't have a parameter
or have only one parameter have special types: you can assign `Foo()`
to a `FooMatcher`-typed variable, and assign `Foo(p)` to a
`FooMatcherP<p_type>`-typed variable.

While you can instantiate a matcher template with reference types,
passing the parameters by pointer usually makes your code more
readable.  If, however, you still want to pass a parameter by
reference, be aware that in the failure message generated by the
matcher you will see the value of the referenced object but not its
address.

You can overload matchers with different numbers of parameters:
```
MATCHER_P(Blah, a, description_string_1) { ... }
MATCHER_P2(Blah, a, b, description_string_2) { ... }
```

While it's tempting to always use the `MATCHER*` macros when defining
a new matcher, you should also consider implementing
`MatcherInterface` or using `MakePolymorphicMatcher()` instead (see
the recipes that follow), especially if you need to use the matcher a
lot.  While these approaches require more work, they give you more
control on the types of the value being matched and the matcher
parameters, which in general leads to better compiler error messages
that pay off in the long run.  They also allow overloading matchers
based on parameter types (as opposed to just based on the number of
parameters).

## Writing New Monomorphic Matchers ##

A matcher of argument type `T` implements
`::testing::MatcherInterface<T>` and does two things: it tests whether a
value of type `T` matches the matcher, and can describe what kind of
values it matches. The latter ability is used for generating readable
error messages when expectations are violated.

The interface looks like this:

```
class MatchResultListener {
 public:
  ...
  // Streams x to the underlying ostream; does nothing if the ostream
  // is NULL.
  template <typename T>
  MatchResultListener& operator<<(const T& x);

  // Returns the underlying ostream.
  ::std::ostream* stream();
};

template <typename T>
class MatcherInterface {
 public:
  virtual ~MatcherInterface();

  // Returns true iff the matcher matches x; also explains the match
  // result to 'listener'.
  virtual bool MatchAndExplain(T x, MatchResultListener* listener) const = 0;

  // Describes this matcher to an ostream.
  virtual void DescribeTo(::std::ostream* os) const = 0;

  // Describes the negation of this matcher to an ostream.
  virtual void DescribeNegationTo(::std::ostream* os) const;
};
```

If you need a custom matcher but `Truly()` is not a good option (for
example, you may not be happy with the way `Truly(predicate)`
describes itself, or you may want your matcher to be polymorphic as
`Eq(value)` is), you can define a matcher to do whatever you want in
two steps: first implement the matcher interface, and then define a
factory function to create a matcher instance. The second step is not
strictly needed but it makes the syntax of using the matcher nicer.

For example, you can define a matcher to test whether an `int` is
divisible by 7 and then use it like this:
```
using ::testing::MakeMatcher;
using ::testing::Matcher;
using ::testing::MatcherInterface;
using ::testing::MatchResultListener;

class DivisibleBy7Matcher : public MatcherInterface<int> {
 public:
  virtual bool MatchAndExplain(int n, MatchResultListener* listener) const {
    return (n % 7) == 0;
  }

  virtual void DescribeTo(::std::ostream* os) const {
    *os << "is divisible by 7";
  }

  virtual void DescribeNegationTo(::std::ostream* os) const {
    *os << "is not divisible by 7";
  }
};

inline Matcher<int> DivisibleBy7() {
  return MakeMatcher(new DivisibleBy7Matcher);
}
...

  EXPECT_CALL(foo, Bar(DivisibleBy7()));
```

You may improve the matcher message by streaming additional
information to the `listener` argument in `MatchAndExplain()`:

```
class DivisibleBy7Matcher : public MatcherInterface<int> {
 public:
  virtual bool MatchAndExplain(int n,
                               MatchResultListener* listener) const {
    const int remainder = n % 7;
    if (remainder != 0) {
      *listener << "the remainder is " << remainder;
    }
    return remainder == 0;
  }
  ...
};
```

Then, `EXPECT_THAT(x, DivisibleBy7());` may general a message like this:
```
Value of: x
Expected: is divisible by 7
  Actual: 23 (the remainder is 2)
```

## Writing New Polymorphic Matchers ##

You've learned how to write your own matchers in the previous
recipe. Just one problem: a matcher created using `MakeMatcher()` only
works for one particular type of arguments. If you want a
_polymorphic_ matcher that works with arguments of several types (for
instance, `Eq(x)` can be used to match a `value` as long as `value` ==
`x` compiles -- `value` and `x` don't have to share the same type),
you can learn the trick from `"gmock/gmock-matchers.h"` but it's a bit
involved.

Fortunately, most of the time you can define a polymorphic matcher
easily with the help of `MakePolymorphicMatcher()`. Here's how you can
define `NotNull()` as an example:

```
using ::testing::MakePolymorphicMatcher;
using ::testing::MatchResultListener;
using ::testing::NotNull;
using ::testing::PolymorphicMatcher;

class NotNullMatcher {
 public:
  // To implement a polymorphic matcher, first define a COPYABLE class
  // that has three members MatchAndExplain(), DescribeTo(), and
  // DescribeNegationTo(), like the following.

  // In this example, we want to use NotNull() with any pointer, so
  // MatchAndExplain() accepts a pointer of any type as its first argument.
  // In general, you can define MatchAndExplain() as an ordinary method or
  // a method template, or even overload it.
  template <typename T>
  bool MatchAndExplain(T* p,
                       MatchResultListener* /* listener */) const {
    return p != NULL;
  }

  // Describes the property of a value matching this matcher.
  void DescribeTo(::std::ostream* os) const { *os << "is not NULL"; }

  // Describes the property of a value NOT matching this matcher.
  void DescribeNegationTo(::std::ostream* os) const { *os << "is NULL"; }
};

// To construct a polymorphic matcher, pass an instance of the class
// to MakePolymorphicMatcher().  Note the return type.
inline PolymorphicMatcher<NotNullMatcher> NotNull() {
  return MakePolymorphicMatcher(NotNullMatcher());
}
...

  EXPECT_CALL(foo, Bar(NotNull()));  // The argument must be a non-NULL pointer.
```

**Note:** Your polymorphic matcher class does **not** need to inherit from
`MatcherInterface` or any other class, and its methods do **not** need
to be virtual.

Like in a monomorphic matcher, you may explain the match result by
streaming additional information to the `listener` argument in
`MatchAndExplain()`.

## Writing New Cardinalities ##

A cardinality is used in `Times()` to tell Google Mock how many times
you expect a call to occur. It doesn't have to be exact. For example,
you can say `AtLeast(5)` or `Between(2, 4)`.

If the built-in set of cardinalities doesn't suit you, you are free to
define your own by implementing the following interface (in namespace
`testing`):

```
class CardinalityInterface {
 public:
  virtual ~CardinalityInterface();

  // Returns true iff call_count calls will satisfy this cardinality.
  virtual bool IsSatisfiedByCallCount(int call_count) const = 0;

  // Returns true iff call_count calls will saturate this cardinality.
  virtual bool IsSaturatedByCallCount(int call_count) const = 0;

  // Describes self to an ostream.
  virtual void DescribeTo(::std::ostream* os) const = 0;
};
```

For example, to specify that a call must occur even number of times,
you can write

```
using ::testing::Cardinality;
using ::testing::CardinalityInterface;
using ::testing::MakeCardinality;

class EvenNumberCardinality : public CardinalityInterface {
 public:
  virtual bool IsSatisfiedByCallCount(int call_count) const {
    return (call_count % 2) == 0;
  }

  virtual bool IsSaturatedByCallCount(int call_count) const {
    return false;
  }

  virtual void DescribeTo(::std::ostream* os) const {
    *os << "called even number of times";
  }
};

Cardinality EvenNumber() {
  return MakeCardinality(new EvenNumberCardinality);
}
...

  EXPECT_CALL(foo, Bar(3))
      .Times(EvenNumber());
```

## Writing New Actions Quickly ##

If the built-in actions don't work for you, and you find it
inconvenient to use `Invoke()`, you can use a macro from the `ACTION*`
family to quickly define a new action that can be used in your code as
if it's a built-in action.

By writing
```
ACTION(name) { statements; }
```
in a namespace scope (i.e. not inside a class or function), you will
define an action with the given name that executes the statements.
The value returned by `statements` will be used as the return value of
the action.  Inside the statements, you can refer to the K-th
(0-based) argument of the mock function as `argK`.  For example:
```
ACTION(IncrementArg1) { return ++(*arg1); }
```
allows you to write
```
... WillOnce(IncrementArg1());
```

Note that you don't need to specify the types of the mock function
arguments.  Rest assured that your code is type-safe though:
you'll get a compiler error if `*arg1` doesn't support the `++`
operator, or if the type of `++(*arg1)` isn't compatible with the mock
function's return type.

Another example:
```
ACTION(Foo) {
  (*arg2)(5);
  Blah();
  *arg1 = 0;
  return arg0;
}
```
defines an action `Foo()` that invokes argument #2 (a function pointer)
with 5, calls function `Blah()`, sets the value pointed to by argument
#1 to 0, and returns argument #0.

For more convenience and flexibility, you can also use the following
pre-defined symbols in the body of `ACTION`:

| `argK_type` | The type of the K-th (0-based) argument of the mock function |
|:------------|:-------------------------------------------------------------|
| `args`      | All arguments of the mock function as a tuple                |
| `args_type` | The type of all arguments of the mock function as a tuple    |
| `return_type` | The return type of the mock function                         |
| `function_type` | The type of the mock function                                |

For example, when using an `ACTION` as a stub action for mock function:
```
int DoSomething(bool flag, int* ptr);
```
we have:

| **Pre-defined Symbol** | **Is Bound To** |
|:-----------------------|:----------------|
| `arg0`                 | the value of `flag` |
| `arg0_type`            | the type `bool` |
| `arg1`                 | the value of `ptr` |
| `arg1_type`            | the type `int*` |
| `args`                 | the tuple `(flag, ptr)` |
| `args_type`            | the type `::testing::tuple<bool, int*>` |
| `return_type`          | the type `int`  |
| `function_type`        | the type `int(bool, int*)` |

## Writing New Parameterized Actions Quickly ##

Sometimes you'll want to parameterize an action you define.  For that
we have another macro
```
ACTION_P(name, param) { statements; }
```

For example,
```
ACTION_P(Add, n) { return arg0 + n; }
```
will allow you to write
```
// Returns argument #0 + 5.
... WillOnce(Add(5));
```

For convenience, we use the term _arguments_ for the values used to
invoke the mock function, and the term _parameters_ for the values
used to instantiate an action.

Note that you don't need to provide the type of the parameter either.
Suppose the parameter is named `param`, you can also use the
Google-Mock-defined symbol `param_type` to refer to the type of the
parameter as inferred by the compiler.  For example, in the body of
`ACTION_P(Add, n)` above, you can write `n_type` for the type of `n`.

Google Mock also provides `ACTION_P2`, `ACTION_P3`, and etc to support
multi-parameter actions.  For example,
```
ACTION_P2(ReturnDistanceTo, x, y) {
  double dx = arg0 - x;
  double dy = arg1 - y;
  return sqrt(dx*dx + dy*dy);
}
```
lets you write
```
... WillOnce(ReturnDistanceTo(5.0, 26.5));
```

You can view `ACTION` as a degenerated parameterized action where the
number of parameters is 0.

You can also easily define actions overloaded on the number of parameters:
```
ACTION_P(Plus, a) { ... }
ACTION_P2(Plus, a, b) { ... }
```

## Restricting the Type of an Argument or Parameter in an ACTION ##

For maximum brevity and reusability, the `ACTION*` macros don't ask
you to provide the types of the mock function arguments and the action
parameters.  Instead, we let the compiler infer the types for us.

Sometimes, however, we may want to be more explicit about the types.
There are several tricks to do that.  For example:
```
ACTION(Foo) {
  // Makes sure arg0 can be converted to int.
  int n = arg0;
  ... use n instead of arg0 here ...
}

ACTION_P(Bar, param) {
  // Makes sure the type of arg1 is const char*.
  ::testing::StaticAssertTypeEq<const char*, arg1_type>();

  // Makes sure param can be converted to bool.
  bool flag = param;
}
```
where `StaticAssertTypeEq` is a compile-time assertion in Google Test
that verifies two types are the same.

## Writing New Action Templates Quickly ##

Sometimes you want to give an action explicit template parameters that
cannot be inferred from its value parameters.  `ACTION_TEMPLATE()`
supports that and can be viewed as an extension to `ACTION()` and
`ACTION_P*()`.

The syntax:
```
ACTION_TEMPLATE(ActionName,
                HAS_m_TEMPLATE_PARAMS(kind1, name1, ..., kind_m, name_m),
                AND_n_VALUE_PARAMS(p1, ..., p_n)) { statements; }
```

defines an action template that takes _m_ explicit template parameters
and _n_ value parameters, where _m_ is between 1 and 10, and _n_ is
between 0 and 10.  `name_i` is the name of the i-th template
parameter, and `kind_i` specifies whether it's a `typename`, an
integral constant, or a template.  `p_i` is the name of the i-th value
parameter.

Example:
```
// DuplicateArg<k, T>(output) converts the k-th argument of the mock
// function to type T and copies it to *output.
ACTION_TEMPLATE(DuplicateArg,
                // Note the comma between int and k:
                HAS_2_TEMPLATE_PARAMS(int, k, typename, T),
                AND_1_VALUE_PARAMS(output)) {
  *output = T(::testing::get<k>(args));
}
```

To create an instance of an action template, write:
```
  ActionName<t1, ..., t_m>(v1, ..., v_n)
```
where the `t`s are the template arguments and the
`v`s are the value arguments.  The value argument
types are inferred by the compiler.  For example:
```
using ::testing::_;
...
  int n;
  EXPECT_CALL(mock, Foo(_, _))
      .WillOnce(DuplicateArg<1, unsigned char>(&n));
```

If you want to explicitly specify the value argument types, you can
provide additional template arguments:
```
  ActionName<t1, ..., t_m, u1, ..., u_k>(v1, ..., v_n)
```
where `u_i` is the desired type of `v_i`.

`ACTION_TEMPLATE` and `ACTION`/`ACTION_P*` can be overloaded on the
number of value parameters, but not on the number of template
parameters.  Without the restriction, the meaning of the following is
unclear:

```
  OverloadedAction<int, bool>(x);
```

Are we using a single-template-parameter action where `bool` refers to
the type of `x`, or a two-template-parameter action where the compiler
is asked to infer the type of `x`?

## Using the ACTION Object's Type ##

If you are writing a function that returns an `ACTION` object, you'll
need to know its type.  The type depends on the macro used to define
the action and the parameter types.  The rule is relatively simple:

| **Given Definition** | **Expression** | **Has Type** |
|:---------------------|:---------------|:-------------|
| `ACTION(Foo)`        | `Foo()`        | `FooAction`  |
| `ACTION_TEMPLATE(Foo, HAS_m_TEMPLATE_PARAMS(...), AND_0_VALUE_PARAMS())` |	`Foo<t1, ..., t_m>()` | `FooAction<t1, ..., t_m>` |
| `ACTION_P(Bar, param)` | `Bar(int_value)` | `BarActionP<int>` |
| `ACTION_TEMPLATE(Bar, HAS_m_TEMPLATE_PARAMS(...), AND_1_VALUE_PARAMS(p1))` | `Bar<t1, ..., t_m>(int_value)` | `FooActionP<t1, ..., t_m, int>` |
| `ACTION_P2(Baz, p1, p2)` | `Baz(bool_value, int_value)` | `BazActionP2<bool, int>` |
| `ACTION_TEMPLATE(Baz, HAS_m_TEMPLATE_PARAMS(...), AND_2_VALUE_PARAMS(p1, p2))`| `Baz<t1, ..., t_m>(bool_value, int_value)` | `FooActionP2<t1, ..., t_m, bool, int>` |
| ...                  | ...            | ...          |

Note that we have to pick different suffixes (`Action`, `ActionP`,
`ActionP2`, and etc) for actions with different numbers of value
parameters, or the action definitions cannot be overloaded on the
number of them.

## Writing New Monomorphic Actions ##

While the `ACTION*` macros are very convenient, sometimes they are
inappropriate.  For example, despite the tricks shown in the previous
recipes, they don't let you directly specify the types of the mock
function arguments and the action parameters, which in general leads
to unoptimized compiler error messages that can baffle unfamiliar
users.  They also don't allow overloading actions based on parameter
types without jumping through some hoops.

An alternative to the `ACTION*` macros is to implement
`::testing::ActionInterface<F>`, where `F` is the type of the mock
function in which the action will be used. For example:

```
template <typename F>class ActionInterface {
 public:
  virtual ~ActionInterface();

  // Performs the action.  Result is the return type of function type
  // F, and ArgumentTuple is the tuple of arguments of F.
  //
  // For example, if F is int(bool, const string&), then Result would
  // be int, and ArgumentTuple would be ::testing::tuple<bool, const string&>.
  virtual Result Perform(const ArgumentTuple& args) = 0;
};

using ::testing::_;
using ::testing::Action;
using ::testing::ActionInterface;
using ::testing::MakeAction;

typedef int IncrementMethod(int*);

class IncrementArgumentAction : public ActionInterface<IncrementMethod> {
 public:
  virtual int Perform(const ::testing::tuple<int*>& args) {
    int* p = ::testing::get<0>(args);  // Grabs the first argument.
    return *p++;
  }
};

Action<IncrementMethod> IncrementArgument() {
  return MakeAction(new IncrementArgumentAction);
}
...

  EXPECT_CALL(foo, Baz(_))
      .WillOnce(IncrementArgument());

  int n = 5;
  foo.Baz(&n);  // Should return 5 and change n to 6.
```

## Writing New Polymorphic Actions ##

The previous recipe showed you how to define your own action. This is
all good, except that you need to know the type of the function in
which the action will be used. Sometimes that can be a problem. For
example, if you want to use the action in functions with _different_
types (e.g. like `Return()` and `SetArgPointee()`).

If an action can be used in several types of mock functions, we say
it's _polymorphic_. The `MakePolymorphicAction()` function template
makes it easy to define such an action:

```
namespace testing {

template <typename Impl>
PolymorphicAction<Impl> MakePolymorphicAction(const Impl& impl);

}  // namespace testing
```

As an example, let's define an action that returns the second argument
in the mock function's argument list. The first step is to define an
implementation class:

```
class ReturnSecondArgumentAction {
 public:
  template <typename Result, typename ArgumentTuple>
  Result Perform(const ArgumentTuple& args) const {
    // To get the i-th (0-based) argument, use ::testing::get<i>(args).
    return ::testing::get<1>(args);
  }
};
```

This implementation class does _not_ need to inherit from any
particular class. What matters is that it must have a `Perform()`
method template. This method template takes the mock function's
arguments as a tuple in a **single** argument, and returns the result of
the action. It can be either `const` or not, but must be invokable
with exactly one template argument, which is the result type. In other
words, you must be able to call `Perform<R>(args)` where `R` is the
mock function's return type and `args` is its arguments in a tuple.

Next, we use `MakePolymorphicAction()` to turn an instance of the
implementation class into the polymorphic action we need. It will be
convenient to have a wrapper for this:

```
using ::testing::MakePolymorphicAction;
using ::testing::PolymorphicAction;

PolymorphicAction<ReturnSecondArgumentAction> ReturnSecondArgument() {
  return MakePolymorphicAction(ReturnSecondArgumentAction());
}
```

Now, you can use this polymorphic action the same way you use the
built-in ones:

```
using ::testing::_;

class MockFoo : public Foo {
 public:
  MOCK_METHOD2(DoThis, int(bool flag, int n));
  MOCK_METHOD3(DoThat, string(int x, const char* str1, const char* str2));
};
...

  MockFoo foo;
  EXPECT_CALL(foo, DoThis(_, _))
      .WillOnce(ReturnSecondArgument());
  EXPECT_CALL(foo, DoThat(_, _, _))
      .WillOnce(ReturnSecondArgument());
  ...
  foo.DoThis(true, 5);         // Will return 5.
  foo.DoThat(1, "Hi", "Bye");  // Will return "Hi".
```

## Teaching Google Mock How to Print Your Values ##

When an uninteresting or unexpected call occurs, Google Mock prints the
argument values and the stack trace to help you debug.  Assertion
macros like `EXPECT_THAT` and `EXPECT_EQ` also print the values in
question when the assertion fails.  Google Mock and Google Test do this using
Google Test's user-extensible value printer.

This printer knows how to print built-in C++ types, native arrays, STL
containers, and any type that supports the `<<` operator.  For other
types, it prints the raw bytes in the value and hopes that you the
user can figure it out.
[Google Test's advanced guide](../../googletest/docs/AdvancedGuide.md#teaching-google-test-how-to-print-your-values)
explains how to extend the printer to do a better job at
printing your particular type than to dump the bytes.
This page discusses the design of new Google Mock features.



# Macros for Defining Actions #

## Problem ##

Due to the lack of closures in C++, it currently requires some
non-trivial effort to define a custom action in Google Mock.  For
example, suppose you want to "increment the value pointed to by the
second argument of the mock function and return it", you could write:

```
int IncrementArg1(Unused, int* p, Unused) {
  return ++(*p);
}

... WillOnce(Invoke(IncrementArg1));
```

There are several things unsatisfactory about this approach:

  * Even though the action only cares about the second argument of the mock function, its definition needs to list other arguments as dummies.  This is tedious.
  * The defined action is usable only in mock functions that takes exactly 3 arguments - an unnecessary restriction.
  * To use the action, one has to say `Invoke(IncrementArg1)`, which isn't as nice as `IncrementArg1()`.

The latter two problems can be overcome using `MakePolymorphicAction()`,
but it requires much more boilerplate code:

```
class IncrementArg1Action {
 public:
  template <typename Result, typename ArgumentTuple>
  Result Perform(const ArgumentTuple& args) const {
    return ++(*tr1::get<1>(args));
  }
};

PolymorphicAction<IncrementArg1Action> IncrementArg1() {
  return MakePolymorphicAction(IncrementArg1Action());
}

... WillOnce(IncrementArg1());
```

Our goal is to allow defining custom actions with the least amount of
boiler-plate C++ requires.

## Solution ##

We propose to introduce a new macro:
```
ACTION(name) { statements; }
```

Using this in a namespace scope will define an action with the given
name that executes the statements.  Inside the statements, you can
refer to the K-th (0-based) argument of the mock function as `argK`.
For example:
```
ACTION(IncrementArg1) { return ++(*arg1); }
```
allows you to write
```
... WillOnce(IncrementArg1());
```

Note that you don't need to specify the types of the mock function
arguments, as brevity is a top design goal here.  Rest assured that
your code is still type-safe though: you'll get a compiler error if
`*arg1` doesn't support the `++` operator, or if the type of
`++(*arg1)` isn't compatible with the mock function's return type.

Another example:
```
ACTION(Foo) {
  (*arg2)(5);
  Blah();
  *arg1 = 0;
  return arg0;
}
```
defines an action `Foo()` that invokes argument #2 (a function pointer)
with 5, calls function `Blah()`, sets the value pointed to by argument
#1 to 0, and returns argument #0.

For more convenience and flexibility, you can also use the following
pre-defined symbols in the body of `ACTION`:

| `argK_type` | The type of the K-th (0-based) argument of the mock function |
|:------------|:-------------------------------------------------------------|
| `args`      | All arguments of the mock function as a tuple                |
| `args_type` | The type of all arguments of the mock function as a tuple    |
| `return_type` | The return type of the mock function                         |
| `function_type` | The type of the mock function                                |

For example, when using an `ACTION` as a stub action for mock function:
```
int DoSomething(bool flag, int* ptr);
```
we have:
| **Pre-defined Symbol** | **Is Bound To** |
|:-----------------------|:----------------|
| `arg0`                 | the value of `flag` |
| `arg0_type`            | the type `bool` |
| `arg1`                 | the value of `ptr` |
| `arg1_type`            | the type `int*` |
| `args`                 | the tuple `(flag, ptr)` |
| `args_type`            | the type `std::tr1::tuple<bool, int*>` |
| `return_type`          | the type `int`  |
| `function_type`        | the type `int(bool, int*)` |

## Parameterized actions ##

Sometimes you'll want to parameterize the action.   For that we propose
another macro
```
ACTION_P(name, param) { statements; }
```

For example,
```
ACTION_P(Add, n) { return arg0 + n; }
```
will allow you to write
```
// Returns argument #0 + 5.
... WillOnce(Add(5));
```

For convenience, we use the term _arguments_ for the values used to
invoke the mock function, and the term _parameters_ for the values
used to instantiate an action.

Note that you don't need to provide the type of the parameter either.
Suppose the parameter is named `param`, you can also use the
Google-Mock-defined symbol `param_type` to refer to the type of the
parameter as inferred by the compiler.

We will also provide `ACTION_P2`, `ACTION_P3`, and etc to support
multi-parameter actions.  For example,
```
ACTION_P2(ReturnDistanceTo, x, y) {
  double dx = arg0 - x;
  double dy = arg1 - y;
  return sqrt(dx*dx + dy*dy);
}
```
lets you write
```
... WillOnce(ReturnDistanceTo(5.0, 26.5));
```

You can view `ACTION` as a degenerated parameterized action where the
number of parameters is 0.

## Advanced Usages ##

### Overloading Actions ###

You can easily define actions overloaded on the number of parameters:
```
ACTION_P(Plus, a) { ... }
ACTION_P2(Plus, a, b) { ... }
```

### Restricting the Type of an Argument or Parameter ###

For maximum brevity and reusability, the `ACTION*` macros don't let
you specify the types of the mock function arguments and the action
parameters.  Instead, we let the compiler infer the types for us.

Sometimes, however, we may want to be more explicit about the types.
There are several tricks to do that.  For example:
```
ACTION(Foo) {
  // Makes sure arg0 can be converted to int.
  int n = arg0;
  ... use n instead of arg0 here ...
}

ACTION_P(Bar, param) {
  // Makes sure the type of arg1 is const char*.
  ::testing::StaticAssertTypeEq<const char*, arg1_type>();

  // Makes sure param can be converted to bool.
  bool flag = param;
}
```
where `StaticAssertTypeEq` is a compile-time assertion we plan to add to
Google Test (the name is chosen to match `static_assert` in C++0x).

### Using the ACTION Object's Type ###

If you are writing a function that returns an `ACTION` object, you'll
need to know its type.  The type depends on the macro used to define
the action and the parameter types.  The rule is relatively simple:
| **Given Definition** | **Expression** | **Has Type** |
|:---------------------|:---------------|:-------------|
| `ACTION(Foo)`        | `Foo()`        | `FooAction`  |
| `ACTION_P(Bar, param)` | `Bar(int_value)` | `BarActionP<int>` |
| `ACTION_P2(Baz, p1, p2)` | `Baz(bool_value, int_value)` | `BazActionP2<bool, int>` |
| ...                  | ...            | ...          |

Note that we have to pick different suffixes (`Action`, `ActionP`,
`ActionP2`, and etc) for actions with different numbers of parameters,
or the action definitions cannot be overloaded on the number of
parameters.

## When to Use ##

While the new macros are very convenient, please also consider other
means of implementing actions (e.g. via `ActionInterface` or
`MakePolymorphicAction()`), especially if you need to use the defined
action a lot.  While the other approaches require more work, they give
you more control on the types of the mock function arguments and the
action parameters, which in general leads to better compiler error
messages that pay off in the long run.  They also allow overloading
actions based on parameter types, as opposed to just the number of
parameters.

## Related Work ##

As you may have realized, the `ACTION*` macros resemble closures (also
known as lambda expressions or anonymous functions).  Indeed, both of
them seek to lower the syntactic overhead for defining a function.

C++0x will support lambdas, but they are not part of C++ right now.
Some non-standard libraries (most notably BLL or Boost Lambda Library)
try to alleviate this problem.  However, they are not a good choice
for defining actions as:

  * They are non-standard and not widely installed.  Google Mock only depends on standard libraries and `tr1::tuple`, which is part of the new C++ standard and comes with gcc 4+.  We want to keep it that way.
  * They are not trivial to learn.
  * They will become obsolete when C++0x's lambda feature is widely supported.  We don't want to make our users use a dying library.
  * Since they are based on operators, they are rather ad hoc: you cannot use statements, and you cannot pass the lambda arguments to a function, for example.
  * They have subtle semantics that easily confuses new users.  For example, in expression `_1++ + foo++`, `foo` will be incremented only once where the expression is evaluated, while `_1` will be incremented every time the unnamed function is invoked.  This is far from intuitive.

`ACTION*` avoid all these problems.

## Future Improvements ##

There may be a need for composing `ACTION*` definitions (i.e. invoking
another `ACTION` inside the definition of one `ACTION*`).  We are not
sure we want it yet, as one can get a similar effect by putting
`ACTION` definitions in function templates and composing the function
templates.  We'll revisit this based on user feedback.

The reason we don't allow `ACTION*()` inside a function body is that
the current C++ standard doesn't allow function-local types to be used
to instantiate templates.  The upcoming C++0x standard will lift this
restriction.  Once this feature is widely supported by compilers, we
can revisit the implementation and add support for using `ACTION*()`
inside a function.

C++0x will also support lambda expressions.  When they become
available, we may want to support using lambdas as actions.

# Macros for Defining Matchers #

Once the macros for defining actions are implemented, we plan to do
the same for matchers:

```
MATCHER(name) { statements; }
```

where you can refer to the value being matched as `arg`.  For example,
given:

```
MATCHER(IsPositive) { return arg > 0; }
```

you can use `IsPositive()` as a matcher that matches a value iff it is
greater than 0.

We will also add `MATCHER_P`, `MATCHER_P2`, and etc for parameterized
matchers.

If you are interested in understanding the internals of Google Mock,
building from source, or contributing ideas or modifications to the
project, then this document is for you.

# Introduction #

First, let's give you some background of the project.

## Licensing ##

All Google Mock source and pre-built packages are provided under the [New BSD License](http://www.opensource.org/licenses/bsd-license.php).

## The Google Mock Community ##

The Google Mock community exists primarily through the [discussion group](http://groups.google.com/group/googlemock), the
[issue tracker](https://github.com/google/googletest/issues) and, to a lesser extent, the [source control repository](../). You are definitely encouraged to contribute to the
discussion and you can also help us to keep the effectiveness of the
group high by following and promoting the guidelines listed here.

### Please Be Friendly ###

Showing courtesy and respect to others is a vital part of the Google
culture, and we strongly encourage everyone participating in Google
Mock development to join us in accepting nothing less. Of course,
being courteous is not the same as failing to constructively disagree
with each other, but it does mean that we should be respectful of each
other when enumerating the 42 technical reasons that a particular
proposal may not be the best choice. There's never a reason to be
antagonistic or dismissive toward anyone who is sincerely trying to
contribute to a discussion.

Sure, C++ testing is serious business and all that, but it's also
a lot of fun. Let's keep it that way. Let's strive to be one of the
friendliest communities in all of open source.

### Where to Discuss Google Mock ###

As always, discuss Google Mock in the official [Google C++ Mocking Framework discussion group](http://groups.google.com/group/googlemock).  You don't have to actually submit
code in order to sign up. Your participation itself is a valuable
contribution.

# Working with the Code #

If you want to get your hands dirty with the code inside Google Mock,
this is the section for you.

## Checking Out the Source from Subversion ##

Checking out the Google Mock source is most useful if you plan to
tweak it yourself.  You check out the source for Google Mock using a
[Subversion](http://subversion.tigris.org/) client as you would for any
other project hosted on Google Code.  Please see the instruction on
the [source code access page](../) for how to do it.

## Compiling from Source ##

Once you check out the code, you can find instructions on how to
compile it in the [README](../README.md) file.

## Testing ##

A mocking framework is of no good if itself is not thoroughly tested.
Tests should be written for any new code, and changes should be
verified to not break existing tests before they are submitted for
review. To perform the tests, follow the instructions in [README](../README.md) and
verify that there are no failures.

# Contributing Code #

We are excited that Google Mock is now open source, and hope to get
great patches from the community. Before you fire up your favorite IDE
and begin hammering away at that new feature, though, please take the
time to read this section and understand the process. While it seems
rigorous, we want to keep a high standard of quality in the code
base.

## Contributor License Agreements ##

You must sign a Contributor License Agreement (CLA) before we can
accept any code.  The CLA protects you and us.

  * If you are an individual writing original source code and you're sure you own the intellectual property, then you'll need to sign an [individual CLA](http://code.google.com/legal/individual-cla-v1.0.html).
  * If you work for a company that wants to allow you to contribute your work to Google Mock, then you'll need to sign a [corporate CLA](http://code.google.com/legal/corporate-cla-v1.0.html).

Follow either of the two links above to access the appropriate CLA and
instructions for how to sign and return it.

## Coding Style ##

To keep the source consistent, readable, diffable and easy to merge,
we use a fairly rigid coding style, as defined by the [google-styleguide](https://github.com/google/styleguide) project.  All patches will be expected
to conform to the style outlined [here](https://google.github.io/styleguide/cppguide.html).

## Submitting Patches ##

Please do submit code. Here's what you need to do:

  1. Normally you should make your change against the SVN trunk instead of a branch or a tag, as the latter two are for release control and should be treated mostly as read-only.
  1. Decide which code you want to submit. A submission should be a set of changes that addresses one issue in the [Google Mock issue tracker](https://github.com/google/googletest/issues). Please don't mix more than one logical change per submittal, because it makes the history hard to follow. If you want to make a change that doesn't have a corresponding issue in the issue tracker, please create one.
  1. Also, coordinate with team members that are listed on the issue in question. This ensures that work isn't being duplicated and communicating your plan early also generally leads to better patches.
  1. Ensure that your code adheres to the [Google Mock source code style](#Coding_Style.md).
  1. Ensure that there are unit tests for your code.
  1. Sign a Contributor License Agreement.
  1. Create a patch file using `svn diff`.
  1. We use [Rietveld](http://codereview.appspot.com/) to do web-based code reviews.  You can read about the tool [here](https://github.com/rietveld-codereview/rietveld/wiki).  When you are ready, upload your patch via Rietveld and notify `googlemock@googlegroups.com` to review it.  There are several ways to upload the patch.  We recommend using the [upload\_gmock.py](../scripts/upload_gmock.py) script, which you can find in the `scripts/` folder in the SVN trunk.

## Google Mock Committers ##

The current members of the Google Mock engineering team are the only
committers at present. In the great tradition of eating one's own
dogfood, we will be requiring each new Google Mock engineering team
member to earn the right to become a committer by following the
procedures in this document, writing consistently great code, and
demonstrating repeatedly that he or she truly gets the zen of Google
Mock.

# Release Process #

We follow the typical release process for Subversion-based projects:

  1. A release branch named `release-X.Y` is created.
  1. Bugs are fixed and features are added in trunk; those individual patches are merged into the release branch until it's stable.
  1. An individual point release (the `Z` in `X.Y.Z`) is made by creating a tag from the branch.
  1. Repeat steps 2 and 3 throughout one release cycle (as determined by features or time).
  1. Go back to step 1 to create another release branch and so on.


---

This page is based on the [Making GWT Better](http://code.google.com/webtoolkit/makinggwtbetter.html) guide from the [Google Web Toolkit](http://code.google.com/webtoolkit/) project.  Except as otherwise [noted](http://code.google.com/policies.html#restrictions), the content of this page is licensed under the [Creative Commons Attribution 2.5 License](http://creativecommons.org/licenses/by/2.5/).
This page lists all documentation markdown files for Google Mock **(the
current git version)**
-- **if you use a former version of Google Mock, please read the
documentation for that specific version instead (e.g. by checking out
the respective git branch/tag).**

  * [ForDummies](ForDummies.md) -- start here if you are new to Google Mock.
  * [CheatSheet](CheatSheet.md) -- a quick reference.
  * [CookBook](CookBook.md) -- recipes for doing various tasks using Google Mock.
  * [FrequentlyAskedQuestions](FrequentlyAskedQuestions.md) -- check here before asking a question on the mailing list.

To contribute code to Google Mock, read:

  * [DevGuide](DevGuide.md) -- read this _before_ writing your first patch.
  * [Pump Manual](../../googletest/docs/PumpManual.md) -- how we generate some of Google Mock's source files.


(**Note:** If you get compiler errors that you don't understand, be sure to consult [Google Mock Doctor](FrequentlyAskedQuestions.md#how-am-i-supposed-to-make-sense-of-these-horrible-template-errors).)

# What Is Google C++ Mocking Framework? #
When you write a prototype or test, often it's not feasible or wise to rely on real objects entirely. A **mock object** implements the same interface as a real object (so it can be used as one), but lets you specify at run time how it will be used and what it should do (which methods will be called? in which order? how many times? with what arguments? what will they return? etc).

**Note:** It is easy to confuse the term _fake objects_ with mock objects. Fakes and mocks actually mean very different things in the Test-Driven Development (TDD) community:

  * **Fake** objects have working implementations, but usually take some shortcut (perhaps to make the operations less expensive), which makes them not suitable for production. An in-memory file system would be an example of a fake.
  * **Mocks** are objects pre-programmed with _expectations_, which form a specification of the calls they are expected to receive.

If all this seems too abstract for you, don't worry - the most important thing to remember is that a mock allows you to check the _interaction_ between itself and code that uses it. The difference between fakes and mocks will become much clearer once you start to use mocks.

**Google C++ Mocking Framework** (or **Google Mock** for short) is a library (sometimes we also call it a "framework" to make it sound cool) for creating mock classes and using them. It does to C++ what [jMock](http://www.jmock.org/) and [EasyMock](http://www.easymock.org/) do to Java.

Using Google Mock involves three basic steps:

  1. Use some simple macros to describe the interface you want to mock, and they will expand to the implementation of your mock class;
  1. Create some mock objects and specify its expectations and behavior using an intuitive syntax;
  1. Exercise code that uses the mock objects. Google Mock will catch any violation of the expectations as soon as it arises.

# Why Google Mock? #
While mock objects help you remove unnecessary dependencies in tests and make them fast and reliable, using mocks manually in C++ is _hard_:

  * Someone has to implement the mocks. The job is usually tedious and error-prone. No wonder people go great distances to avoid it.
  * The quality of those manually written mocks is a bit, uh, unpredictable. You may see some really polished ones, but you may also see some that were hacked up in a hurry and have all sorts of ad-hoc restrictions.
  * The knowledge you gained from using one mock doesn't transfer to the next.

In contrast, Java and Python programmers have some fine mock frameworks, which automate the creation of mocks. As a result, mocking is a proven effective technique and widely adopted practice in those communities. Having the right tool absolutely makes the difference.

Google Mock was built to help C++ programmers. It was inspired by [jMock](http://www.jmock.org/) and [EasyMock](http://www.easymock.org/), but designed with C++'s specifics in mind. It is your friend if any of the following problems is bothering you:

  * You are stuck with a sub-optimal design and wish you had done more prototyping before it was too late, but prototyping in C++ is by no means "rapid".
  * Your tests are slow as they depend on too many libraries or use expensive resources (e.g. a database).
  * Your tests are brittle as some resources they use are unreliable (e.g. the network).
  * You want to test how your code handles a failure (e.g. a file checksum error), but it's not easy to cause one.
  * You need to make sure that your module interacts with other modules in the right way, but it's hard to observe the interaction; therefore you resort to observing the side effects at the end of the action, which is awkward at best.
  * You want to "mock out" your dependencies, except that they don't have mock implementations yet; and, frankly, you aren't thrilled by some of those hand-written mocks.

We encourage you to use Google Mock as:

  * a _design_ tool, for it lets you experiment with your interface design early and often. More iterations lead to better designs!
  * a _testing_ tool to cut your tests' outbound dependencies and probe the interaction between your module and its collaborators.

# Getting Started #
Using Google Mock is easy! Inside your C++ source file, just `#include` `"gtest/gtest.h"` and `"gmock/gmock.h"`, and you are ready to go.

# A Case for Mock Turtles #
Let's look at an example. Suppose you are developing a graphics program that relies on a LOGO-like API for drawing. How would you test that it does the right thing? Well, you can run it and compare the screen with a golden screen snapshot, but let's admit it: tests like this are expensive to run and fragile (What if you just upgraded to a shiny new graphics card that has better anti-aliasing? Suddenly you have to update all your golden images.). It would be too painful if all your tests are like this. Fortunately, you learned about Dependency Injection and know the right thing to do: instead of having your application talk to the drawing API directly, wrap the API in an interface (say, `Turtle`) and code to that interface:

```
class Turtle {
  ...
  virtual ~Turtle() {}
  virtual void PenUp() = 0;
  virtual void PenDown() = 0;
  virtual void Forward(int distance) = 0;
  virtual void Turn(int degrees) = 0;
  virtual void GoTo(int x, int y) = 0;
  virtual int GetX() const = 0;
  virtual int GetY() const = 0;
};
```

(Note that the destructor of `Turtle` **must** be virtual, as is the case for **all** classes you intend to inherit from - otherwise the destructor of the derived class will not be called when you delete an object through a base pointer, and you'll get corrupted program states like memory leaks.)

You can control whether the turtle's movement will leave a trace using `PenUp()` and `PenDown()`, and control its movement using `Forward()`, `Turn()`, and `GoTo()`. Finally, `GetX()` and `GetY()` tell you the current position of the turtle.

Your program will normally use a real implementation of this interface. In tests, you can use a mock implementation instead. This allows you to easily check what drawing primitives your program is calling, with what arguments, and in which order. Tests written this way are much more robust (they won't break because your new machine does anti-aliasing differently), easier to read and maintain (the intent of a test is expressed in the code, not in some binary images), and run _much, much faster_.

# Writing the Mock Class #
If you are lucky, the mocks you need to use have already been implemented by some nice people. If, however, you find yourself in the position to write a mock class, relax - Google Mock turns this task into a fun game! (Well, almost.)

## How to Define It ##
Using the `Turtle` interface as example, here are the simple steps you need to follow:

  1. Derive a class `MockTurtle` from `Turtle`.
  1. Take a _virtual_ function of `Turtle` (while it's possible to [mock non-virtual methods using templates](CookBook.md#mocking-nonvirtual-methods), it's much more involved). Count how many arguments it has.
  1. In the `public:` section of the child class, write `MOCK_METHODn();` (or `MOCK_CONST_METHODn();` if you are mocking a `const` method), where `n` is the number of the arguments; if you counted wrong, shame on you, and a compiler error will tell you so.
  1. Now comes the fun part: you take the function signature, cut-and-paste the _function name_ as the _first_ argument to the macro, and leave what's left as the _second_ argument (in case you're curious, this is the _type of the function_).
  1. Repeat until all virtual functions you want to mock are done.

After the process, you should have something like:

```
#include "gmock/gmock.h"  // Brings in Google Mock.
class MockTurtle : public Turtle {
 public:
  ...
  MOCK_METHOD0(PenUp, void());
  MOCK_METHOD0(PenDown, void());
  MOCK_METHOD1(Forward, void(int distance));
  MOCK_METHOD1(Turn, void(int degrees));
  MOCK_METHOD2(GoTo, void(int x, int y));
  MOCK_CONST_METHOD0(GetX, int());
  MOCK_CONST_METHOD0(GetY, int());
};
```

You don't need to define these mock methods somewhere else - the `MOCK_METHOD*` macros will generate the definitions for you. It's that simple! Once you get the hang of it, you can pump out mock classes faster than your source-control system can handle your check-ins.

**Tip:** If even this is too much work for you, you'll find the
`gmock_gen.py` tool in Google Mock's `scripts/generator/` directory (courtesy of the [cppclean](http://code.google.com/p/cppclean/) project) useful.  This command-line
tool requires that you have Python 2.4 installed.  You give it a C++ file and the name of an abstract class defined in it,
and it will print the definition of the mock class for you.  Due to the
complexity of the C++ language, this script may not always work, but
it can be quite handy when it does.  For more details, read the [user documentation](../scripts/generator/README).

## Where to Put It ##
When you define a mock class, you need to decide where to put its definition. Some people put it in a `*_test.cc`. This is fine when the interface being mocked (say, `Foo`) is owned by the same person or team. Otherwise, when the owner of `Foo` changes it, your test could break. (You can't really expect `Foo`'s maintainer to fix every test that uses `Foo`, can you?)

So, the rule of thumb is: if you need to mock `Foo` and it's owned by others, define the mock class in `Foo`'s package (better, in a `testing` sub-package such that you can clearly separate production code and testing utilities), and put it in a `mock_foo.h`. Then everyone can reference `mock_foo.h` from their tests. If `Foo` ever changes, there is only one copy of `MockFoo` to change, and only tests that depend on the changed methods need to be fixed.

Another way to do it: you can introduce a thin layer `FooAdaptor` on top of `Foo` and code to this new interface. Since you own `FooAdaptor`, you can absorb changes in `Foo` much more easily. While this is more work initially, carefully choosing the adaptor interface can make your code easier to write and more readable (a net win in the long run), as you can choose `FooAdaptor` to fit your specific domain much better than `Foo` does.

# Using Mocks in Tests #
Once you have a mock class, using it is easy. The typical work flow is:

  1. Import the Google Mock names from the `testing` namespace such that you can use them unqualified (You only have to do it once per file. Remember that namespaces are a good idea and good for your health.).
  1. Create some mock objects.
  1. Specify your expectations on them (How many times will a method be called? With what arguments? What should it do? etc.).
  1. Exercise some code that uses the mocks; optionally, check the result using Google Test assertions. If a mock method is called more than expected or with wrong arguments, you'll get an error immediately.
  1. When a mock is destructed, Google Mock will automatically check whether all expectations on it have been satisfied.

Here's an example:

```
#include "path/to/mock-turtle.h"
#include "gmock/gmock.h"
#include "gtest/gtest.h"
using ::testing::AtLeast;                     // #1

TEST(PainterTest, CanDrawSomething) {
  MockTurtle turtle;                          // #2
  EXPECT_CALL(turtle, PenDown())              // #3
      .Times(AtLeast(1));

  Painter painter(&turtle);                   // #4

  EXPECT_TRUE(painter.DrawCircle(0, 0, 10));
}                                             // #5

int main(int argc, char** argv) {
  // The following line must be executed to initialize Google Mock
  // (and Google Test) before running the tests.
  ::testing::InitGoogleMock(&argc, argv);
  return RUN_ALL_TESTS();
}
```

As you might have guessed, this test checks that `PenDown()` is called at least once. If the `painter` object didn't call this method, your test will fail with a message like this:

```
path/to/my_test.cc:119: Failure
Actual function call count doesn't match this expectation:
Actually: never called;
Expected: called at least once.
```

**Tip 1:** If you run the test from an Emacs buffer, you can hit `<Enter>` on the line number displayed in the error message to jump right to the failed expectation.

**Tip 2:** If your mock objects are never deleted, the final verification won't happen. Therefore it's a good idea to use a heap leak checker in your tests when you allocate mocks on the heap.

**Important note:** Google Mock requires expectations to be set **before** the mock functions are called, otherwise the behavior is **undefined**. In particular, you mustn't interleave `EXPECT_CALL()`s and calls to the mock functions.

This means `EXPECT_CALL()` should be read as expecting that a call will occur _in the future_, not that a call has occurred. Why does Google Mock work like that? Well, specifying the expectation beforehand allows Google Mock to report a violation as soon as it arises, when the context (stack trace, etc) is still available. This makes debugging much easier.

Admittedly, this test is contrived and doesn't do much. You can easily achieve the same effect without using Google Mock. However, as we shall reveal soon, Google Mock allows you to do _much more_ with the mocks.

## Using Google Mock with Any Testing Framework ##
If you want to use something other than Google Test (e.g. [CppUnit](http://sourceforge.net/projects/cppunit/) or
[CxxTest](http://cxxtest.tigris.org/)) as your testing framework, just change the `main()` function in the previous section to:
```
int main(int argc, char** argv) {
  // The following line causes Google Mock to throw an exception on failure,
  // which will be interpreted by your testing framework as a test failure.
  ::testing::GTEST_FLAG(throw_on_failure) = true;
  ::testing::InitGoogleMock(&argc, argv);
  ... whatever your testing framework requires ...
}
```

This approach has a catch: it makes Google Mock throw an exception
from a mock object's destructor sometimes.  With some compilers, this
sometimes causes the test program to crash.  You'll still be able to
notice that the test has failed, but it's not a graceful failure.

A better solution is to use Google Test's
[event listener API](../../googletest/docs/AdvancedGuide.md#extending-google-test-by-handling-test-events)
to report a test failure to your testing framework properly.  You'll need to
implement the `OnTestPartResult()` method of the event listener interface, but it
should be straightforward.

If this turns out to be too much work, we suggest that you stick with
Google Test, which works with Google Mock seamlessly (in fact, it is
technically part of Google Mock.).  If there is a reason that you
cannot use Google Test, please let us know.

# Setting Expectations #
The key to using a mock object successfully is to set the _right expectations_ on it. If you set the expectations too strict, your test will fail as the result of unrelated changes. If you set them too loose, bugs can slip through. You want to do it just right such that your test can catch exactly the kind of bugs you intend it to catch. Google Mock provides the necessary means for you to do it "just right."

## General Syntax ##
In Google Mock we use the `EXPECT_CALL()` macro to set an expectation on a mock method. The general syntax is:

```
EXPECT_CALL(mock_object, method(matchers))
    .Times(cardinality)
    .WillOnce(action)
    .WillRepeatedly(action);
```

The macro has two arguments: first the mock object, and then the method and its arguments. Note that the two are separated by a comma (`,`), not a period (`.`). (Why using a comma? The answer is that it was necessary for technical reasons.)

The macro can be followed by some optional _clauses_ that provide more information about the expectation. We'll discuss how each clause works in the coming sections.

This syntax is designed to make an expectation read like English. For example, you can probably guess that

```
using ::testing::Return;
...
EXPECT_CALL(turtle, GetX())
    .Times(5)
    .WillOnce(Return(100))
    .WillOnce(Return(150))
    .WillRepeatedly(Return(200));
```

says that the `turtle` object's `GetX()` method will be called five times, it will return 100 the first time, 150 the second time, and then 200 every time. Some people like to call this style of syntax a Domain-Specific Language (DSL).

**Note:** Why do we use a macro to do this? It serves two purposes: first it makes expectations easily identifiable (either by `grep` or by a human reader), and second it allows Google Mock to include the source file location of a failed expectation in messages, making debugging easier.

## Matchers: What Arguments Do We Expect? ##
When a mock function takes arguments, we must specify what arguments we are expecting; for example:

```
// Expects the turtle to move forward by 100 units.
EXPECT_CALL(turtle, Forward(100));
```

Sometimes you may not want to be too specific (Remember that talk about tests being too rigid? Over specification leads to brittle tests and obscures the intent of tests. Therefore we encourage you to specify only what's necessary - no more, no less.). If you care to check that `Forward()` will be called but aren't interested in its actual argument, write `_` as the argument, which means "anything goes":

```
using ::testing::_;
...
// Expects the turtle to move forward.
EXPECT_CALL(turtle, Forward(_));
```

`_` is an instance of what we call **matchers**. A matcher is like a predicate and can test whether an argument is what we'd expect. You can use a matcher inside `EXPECT_CALL()` wherever a function argument is expected.

A list of built-in matchers can be found in the [CheatSheet](CheatSheet.md). For example, here's the `Ge` (greater than or equal) matcher:

```
using ::testing::Ge;
...
EXPECT_CALL(turtle, Forward(Ge(100)));
```

This checks that the turtle will be told to go forward by at least 100 units.

## Cardinalities: How Many Times Will It Be Called? ##
The first clause we can specify following an `EXPECT_CALL()` is `Times()`. We call its argument a **cardinality** as it tells _how many times_ the call should occur. It allows us to repeat an expectation many times without actually writing it as many times. More importantly, a cardinality can be "fuzzy", just like a matcher can be. This allows a user to express the intent of a test exactly.

An interesting special case is when we say `Times(0)`. You may have guessed - it means that the function shouldn't be called with the given arguments at all, and Google Mock will report a Google Test failure whenever the function is (wrongfully) called.

We've seen `AtLeast(n)` as an example of fuzzy cardinalities earlier. For the list of built-in cardinalities you can use, see the [CheatSheet](CheatSheet.md).

The `Times()` clause can be omitted. **If you omit `Times()`, Google Mock will infer the cardinality for you.** The rules are easy to remember:

  * If **neither** `WillOnce()` **nor** `WillRepeatedly()` is in the `EXPECT_CALL()`, the inferred cardinality is `Times(1)`.
  * If there are `n WillOnce()`'s but **no** `WillRepeatedly()`, where `n` >= 1, the cardinality is `Times(n)`.
  * If there are `n WillOnce()`'s and **one** `WillRepeatedly()`, where `n` >= 0, the cardinality is `Times(AtLeast(n))`.

**Quick quiz:** what do you think will happen if a function is expected to be called twice but actually called four times?

## Actions: What Should It Do? ##
Remember that a mock object doesn't really have a working implementation? We as users have to tell it what to do when a method is invoked. This is easy in Google Mock.

First, if the return type of a mock function is a built-in type or a pointer, the function has a **default action** (a `void` function will just return, a `bool` function will return `false`, and other functions will return 0). In addition, in C++ 11 and above, a mock function whose return type is default-constructible (i.e. has a default constructor) has a default action of returning a default-constructed value.  If you don't say anything, this behavior will be used.

Second, if a mock function doesn't have a default action, or the default action doesn't suit you, you can specify the action to be taken each time the expectation matches using a series of `WillOnce()` clauses followed by an optional `WillRepeatedly()`. For example,

```
using ::testing::Return;
...
EXPECT_CALL(turtle, GetX())
    .WillOnce(Return(100))
    .WillOnce(Return(200))
    .WillOnce(Return(300));
```

This says that `turtle.GetX()` will be called _exactly three times_ (Google Mock inferred this from how many `WillOnce()` clauses we've written, since we didn't explicitly write `Times()`), and will return 100, 200, and 300 respectively.

```
using ::testing::Return;
...
EXPECT_CALL(turtle, GetY())
    .WillOnce(Return(100))
    .WillOnce(Return(200))
    .WillRepeatedly(Return(300));
```

says that `turtle.GetY()` will be called _at least twice_ (Google Mock knows this as we've written two `WillOnce()` clauses and a `WillRepeatedly()` while having no explicit `Times()`), will return 100 the first time, 200 the second time, and 300 from the third time on.

Of course, if you explicitly write a `Times()`, Google Mock will not try to infer the cardinality itself. What if the number you specified is larger than there are `WillOnce()` clauses? Well, after all `WillOnce()`s are used up, Google Mock will do the _default_ action for the function every time (unless, of course, you have a `WillRepeatedly()`.).

What can we do inside `WillOnce()` besides `Return()`? You can return a reference using `ReturnRef(variable)`, or invoke a pre-defined function, among [others](CheatSheet.md#actions).

**Important note:** The `EXPECT_CALL()` statement evaluates the action clause only once, even though the action may be performed many times. Therefore you must be careful about side effects. The following may not do what you want:

```
int n = 100;
EXPECT_CALL(turtle, GetX())
.Times(4)
.WillRepeatedly(Return(n++));
```

Instead of returning 100, 101, 102, ..., consecutively, this mock function will always return 100 as `n++` is only evaluated once. Similarly, `Return(new Foo)` will create a new `Foo` object when the `EXPECT_CALL()` is executed, and will return the same pointer every time. If you want the side effect to happen every time, you need to define a custom action, which we'll teach in the [CookBook](CookBook.md).

Time for another quiz! What do you think the following means?

```
using ::testing::Return;
...
EXPECT_CALL(turtle, GetY())
.Times(4)
.WillOnce(Return(100));
```

Obviously `turtle.GetY()` is expected to be called four times. But if you think it will return 100 every time, think twice! Remember that one `WillOnce()` clause will be consumed each time the function is invoked and the default action will be taken afterwards. So the right answer is that `turtle.GetY()` will return 100 the first time, but **return 0 from the second time on**, as returning 0 is the default action for `int` functions.

## Using Multiple Expectations ##
So far we've only shown examples where you have a single expectation. More realistically, you're going to specify expectations on multiple mock methods, which may be from multiple mock objects.

By default, when a mock method is invoked, Google Mock will search the expectations in the **reverse order** they are defined, and stop when an active expectation that matches the arguments is found (you can think of it as "newer rules override older ones."). If the matching expectation cannot take any more calls, you will get an upper-bound-violated failure. Here's an example:

```
using ::testing::_;
...
EXPECT_CALL(turtle, Forward(_));  // #1
EXPECT_CALL(turtle, Forward(10))  // #2
    .Times(2);
```

If `Forward(10)` is called three times in a row, the third time it will be an error, as the last matching expectation (#2) has been saturated. If, however, the third `Forward(10)` call is replaced by `Forward(20)`, then it would be OK, as now #1 will be the matching expectation.

**Side note:** Why does Google Mock search for a match in the _reverse_ order of the expectations? The reason is that this allows a user to set up the default expectations in a mock object's constructor or the test fixture's set-up phase and then customize the mock by writing more specific expectations in the test body. So, if you have two expectations on the same method, you want to put the one with more specific matchers **after** the other, or the more specific rule would be shadowed by the more general one that comes after it.

## Ordered vs Unordered Calls ##
By default, an expectation can match a call even though an earlier expectation hasn't been satisfied. In other words, the calls don't have to occur in the order the expectations are specified.

Sometimes, you may want all the expected calls to occur in a strict order. To say this in Google Mock is easy:

```
using ::testing::InSequence;
...
TEST(FooTest, DrawsLineSegment) {
  ...
  {
    InSequence dummy;

    EXPECT_CALL(turtle, PenDown());
    EXPECT_CALL(turtle, Forward(100));
    EXPECT_CALL(turtle, PenUp());
  }
  Foo();
}
```

By creating an object of type `InSequence`, all expectations in its scope are put into a _sequence_ and have to occur _sequentially_. Since we are just relying on the constructor and destructor of this object to do the actual work, its name is really irrelevant.

In this example, we test that `Foo()` calls the three expected functions in the order as written. If a call is made out-of-order, it will be an error.

(What if you care about the relative order of some of the calls, but not all of them? Can you specify an arbitrary partial order? The answer is ... yes! If you are impatient, the details can be found in the [CookBook](CookBook.md#expecting-partially-ordered-calls).)

## All Expectations Are Sticky (Unless Said Otherwise) ##
Now let's do a quick quiz to see how well you can use this mock stuff already. How would you test that the turtle is asked to go to the origin _exactly twice_ (you want to ignore any other instructions it receives)?

After you've come up with your answer, take a look at ours and compare notes (solve it yourself first - don't cheat!):

```
using ::testing::_;
...
EXPECT_CALL(turtle, GoTo(_, _))  // #1
    .Times(AnyNumber());
EXPECT_CALL(turtle, GoTo(0, 0))  // #2
    .Times(2);
```

Suppose `turtle.GoTo(0, 0)` is called three times. In the third time, Google Mock will see that the arguments match expectation #2 (remember that we always pick the last matching expectation). Now, since we said that there should be only two such calls, Google Mock will report an error immediately. This is basically what we've told you in the "Using Multiple Expectations" section above.

This example shows that **expectations in Google Mock are "sticky" by default**, in the sense that they remain active even after we have reached their invocation upper bounds. This is an important rule to remember, as it affects the meaning of the spec, and is **different** to how it's done in many other mocking frameworks (Why'd we do that? Because we think our rule makes the common cases easier to express and understand.).

Simple? Let's see if you've really understood it: what does the following code say?

```
using ::testing::Return;
...
for (int i = n; i > 0; i--) {
  EXPECT_CALL(turtle, GetX())
      .WillOnce(Return(10*i));
}
```

If you think it says that `turtle.GetX()` will be called `n` times and will return 10, 20, 30, ..., consecutively, think twice! The problem is that, as we said, expectations are sticky. So, the second time `turtle.GetX()` is called, the last (latest) `EXPECT_CALL()` statement will match, and will immediately lead to an "upper bound exceeded" error - this piece of code is not very useful!

One correct way of saying that `turtle.GetX()` will return 10, 20, 30, ..., is to explicitly say that the expectations are _not_ sticky. In other words, they should _retire_ as soon as they are saturated:

```
using ::testing::Return;
...
for (int i = n; i > 0; i--) {
  EXPECT_CALL(turtle, GetX())
    .WillOnce(Return(10*i))
    .RetiresOnSaturation();
}
```

And, there's a better way to do it: in this case, we expect the calls to occur in a specific order, and we line up the actions to match the order. Since the order is important here, we should make it explicit using a sequence:

```
using ::testing::InSequence;
using ::testing::Return;
...
{
  InSequence s;

  for (int i = 1; i <= n; i++) {
    EXPECT_CALL(turtle, GetX())
        .WillOnce(Return(10*i))
        .RetiresOnSaturation();
  }
}
```

By the way, the other situation where an expectation may _not_ be sticky is when it's in a sequence - as soon as another expectation that comes after it in the sequence has been used, it automatically retires (and will never be used to match any call).

## Uninteresting Calls ##
A mock object may have many methods, and not all of them are that interesting. For example, in some tests we may not care about how many times `GetX()` and `GetY()` get called.

In Google Mock, if you are not interested in a method, just don't say anything about it. If a call to this method occurs, you'll see a warning in the test output, but it won't be a failure.

# What Now? #
Congratulations! You've learned enough about Google Mock to start using it. Now, you might want to join the [googlemock](http://groups.google.com/group/googlemock) discussion group and actually write some tests using Google Mock - it will be fun. Hey, it may even be addictive - you've been warned.

Then, if you feel like increasing your mock quotient, you should move on to the [CookBook](CookBook.md). You can learn many advanced features of Google Mock there -- and advance your level of enjoyment and testing bliss.


Please send your questions to the
[googlemock](http://groups.google.com/group/googlemock) discussion
group. If you need help with compiler errors, make sure you have
tried [Google Mock Doctor](#How_am_I_supposed_to_make_sense_of_these_horrible_template_error.md) first.

## When I call a method on my mock object, the method for the real object is invoked instead.  What's the problem? ##

In order for a method to be mocked, it must be _virtual_, unless you use the [high-perf dependency injection technique](CookBook.md#mocking-nonvirtual-methods).

## I wrote some matchers.  After I upgraded to a new version of Google Mock, they no longer compile.  What's going on? ##

After version 1.4.0 of Google Mock was released, we had an idea on how
to make it easier to write matchers that can generate informative
messages efficiently.  We experimented with this idea and liked what
we saw.  Therefore we decided to implement it.

Unfortunately, this means that if you have defined your own matchers
by implementing `MatcherInterface` or using `MakePolymorphicMatcher()`,
your definitions will no longer compile.  Matchers defined using the
`MATCHER*` family of macros are not affected.

Sorry for the hassle if your matchers are affected.  We believe it's
in everyone's long-term interest to make this change sooner than
later.  Fortunately, it's usually not hard to migrate an existing
matcher to the new API.  Here's what you need to do:

If you wrote your matcher like this:
```
// Old matcher definition that doesn't work with the latest
// Google Mock.
using ::testing::MatcherInterface;
...
class MyWonderfulMatcher : public MatcherInterface<MyType> {
 public:
  ...
  virtual bool Matches(MyType value) const {
    // Returns true if value matches.
    return value.GetFoo() > 5;
  }
  ...
};
```

you'll need to change it to:
```
// New matcher definition that works with the latest Google Mock.
using ::testing::MatcherInterface;
using ::testing::MatchResultListener;
...
class MyWonderfulMatcher : public MatcherInterface<MyType> {
 public:
  ...
  virtual bool MatchAndExplain(MyType value,
                               MatchResultListener* listener) const {
    // Returns true if value matches.
    return value.GetFoo() > 5;
  }
  ...
};
```
(i.e. rename `Matches()` to `MatchAndExplain()` and give it a second
argument of type `MatchResultListener*`.)

If you were also using `ExplainMatchResultTo()` to improve the matcher
message:
```
// Old matcher definition that doesn't work with the lastest
// Google Mock.
using ::testing::MatcherInterface;
...
class MyWonderfulMatcher : public MatcherInterface<MyType> {
 public:
  ...
  virtual bool Matches(MyType value) const {
    // Returns true if value matches.
    return value.GetFoo() > 5;
  }

  virtual void ExplainMatchResultTo(MyType value,
                                    ::std::ostream* os) const {
    // Prints some helpful information to os to help
    // a user understand why value matches (or doesn't match).
    *os << "the Foo property is " << value.GetFoo();
  }
  ...
};
```

you should move the logic of `ExplainMatchResultTo()` into
`MatchAndExplain()`, using the `MatchResultListener` argument where
the `::std::ostream` was used:
```
// New matcher definition that works with the latest Google Mock.
using ::testing::MatcherInterface;
using ::testing::MatchResultListener;
...
class MyWonderfulMatcher : public MatcherInterface<MyType> {
 public:
  ...
  virtual bool MatchAndExplain(MyType value,
                               MatchResultListener* listener) const {
    // Returns true if value matches.
    *listener << "the Foo property is " << value.GetFoo();
    return value.GetFoo() > 5;
  }
  ...
};
```

If your matcher is defined using `MakePolymorphicMatcher()`:
```
// Old matcher definition that doesn't work with the latest
// Google Mock.
using ::testing::MakePolymorphicMatcher;
...
class MyGreatMatcher {
 public:
  ...
  bool Matches(MyType value) const {
    // Returns true if value matches.
    return value.GetBar() < 42;
  }
  ...
};
... MakePolymorphicMatcher(MyGreatMatcher()) ...
```

you should rename the `Matches()` method to `MatchAndExplain()` and
add a `MatchResultListener*` argument (the same as what you need to do
for matchers defined by implementing `MatcherInterface`):
```
// New matcher definition that works with the latest Google Mock.
using ::testing::MakePolymorphicMatcher;
using ::testing::MatchResultListener;
...
class MyGreatMatcher {
 public:
  ...
  bool MatchAndExplain(MyType value,
                       MatchResultListener* listener) const {
    // Returns true if value matches.
    return value.GetBar() < 42;
  }
  ...
};
... MakePolymorphicMatcher(MyGreatMatcher()) ...
```

If your polymorphic matcher uses `ExplainMatchResultTo()` for better
failure messages:
```
// Old matcher definition that doesn't work with the latest
// Google Mock.
using ::testing::MakePolymorphicMatcher;
...
class MyGreatMatcher {
 public:
  ...
  bool Matches(MyType value) const {
    // Returns true if value matches.
    return value.GetBar() < 42;
  }
  ...
};
void ExplainMatchResultTo(const MyGreatMatcher& matcher,
                          MyType value,
                          ::std::ostream* os) {
  // Prints some helpful information to os to help
  // a user understand why value matches (or doesn't match).
  *os << "the Bar property is " << value.GetBar();
}
... MakePolymorphicMatcher(MyGreatMatcher()) ...
```

you'll need to move the logic inside `ExplainMatchResultTo()` to
`MatchAndExplain()`:
```
// New matcher definition that works with the latest Google Mock.
using ::testing::MakePolymorphicMatcher;
using ::testing::MatchResultListener;
...
class MyGreatMatcher {
 public:
  ...
  bool MatchAndExplain(MyType value,
                       MatchResultListener* listener) const {
    // Returns true if value matches.
    *listener << "the Bar property is " << value.GetBar();
    return value.GetBar() < 42;
  }
  ...
};
... MakePolymorphicMatcher(MyGreatMatcher()) ...
```

For more information, you can read these
[two](CookBook.md#writing-new-monomorphic-matchers)
[recipes](CookBook.md#writing-new-polymorphic-matchers)
from the cookbook.  As always, you
are welcome to post questions on `googlemock@googlegroups.com` if you
need any help.

## When using Google Mock, do I have to use Google Test as the testing framework?  I have my favorite testing framework and don't want to switch. ##

Google Mock works out of the box with Google Test.  However, it's easy
to configure it to work with any testing framework of your choice.
[Here](ForDummies.md#using-google-mock-with-any-testing-framework) is how.

## How am I supposed to make sense of these horrible template errors? ##

If you are confused by the compiler errors gcc threw at you,
try consulting the _Google Mock Doctor_ tool first.  What it does is to
scan stdin for gcc error messages, and spit out diagnoses on the
problems (we call them diseases) your code has.

To "install", run command:
```
alias gmd='<path to googlemock>/scripts/gmock_doctor.py'
```

To use it, do:
```
<your-favorite-build-command> <your-test> 2>&1 | gmd
```

For example:
```
make my_test 2>&1 | gmd
```

Or you can run `gmd` and copy-n-paste gcc's error messages to it.

## Can I mock a variadic function? ##

You cannot mock a variadic function (i.e. a function taking ellipsis
(`...`) arguments) directly in Google Mock.

The problem is that in general, there is _no way_ for a mock object to
know how many arguments are passed to the variadic method, and what
the arguments' types are.  Only the _author of the base class_ knows
the protocol, and we cannot look into their head.

Therefore, to mock such a function, the _user_ must teach the mock
object how to figure out the number of arguments and their types.  One
way to do it is to provide overloaded versions of the function.

Ellipsis arguments are inherited from C and not really a C++ feature.
They are unsafe to use and don't work with arguments that have
constructors or destructors.  Therefore we recommend to avoid them in
C++ as much as possible.

## MSVC gives me warning C4301 or C4373 when I define a mock method with a const parameter.  Why? ##

If you compile this using Microsoft Visual C++ 2005 SP1:
```
class Foo {
  ...
  virtual void Bar(const int i) = 0;
};

class MockFoo : public Foo {
  ...
  MOCK_METHOD1(Bar, void(const int i));
};
```
You may get the following warning:
```
warning C4301: 'MockFoo::Bar': overriding virtual function only differs from 'Foo::Bar' by const/volatile qualifier
```

This is a MSVC bug.  The same code compiles fine with gcc ,for
example.  If you use Visual C++ 2008 SP1, you would get the warning:
```
warning C4373: 'MockFoo::Bar': virtual function overrides 'Foo::Bar', previous versions of the compiler did not override when parameters only differed by const/volatile qualifiers
```

In C++, if you _declare_ a function with a `const` parameter, the
`const` modifier is _ignored_.  Therefore, the `Foo` base class above
is equivalent to:
```
class Foo {
  ...
  virtual void Bar(int i) = 0;  // int or const int?  Makes no difference.
};
```

In fact, you can _declare_ Bar() with an `int` parameter, and _define_
it with a `const int` parameter.  The compiler will still match them
up.

Since making a parameter `const` is meaningless in the method
_declaration_, we recommend to remove it in both `Foo` and `MockFoo`.
That should workaround the VC bug.

Note that we are talking about the _top-level_ `const` modifier here.
If the function parameter is passed by pointer or reference, declaring
the _pointee_ or _referee_ as `const` is still meaningful.  For
example, the following two declarations are _not_ equivalent:
```
void Bar(int* p);        // Neither p nor *p is const.
void Bar(const int* p);  // p is not const, but *p is.
```

## I have a huge mock class, and Microsoft Visual C++ runs out of memory when compiling it.  What can I do? ##

We've noticed that when the `/clr` compiler flag is used, Visual C++
uses 5~6 times as much memory when compiling a mock class.  We suggest
to avoid `/clr` when compiling native C++ mocks.

## I can't figure out why Google Mock thinks my expectations are not satisfied.  What should I do? ##

You might want to run your test with
`--gmock_verbose=info`.  This flag lets Google Mock print a trace
of every mock function call it receives.  By studying the trace,
you'll gain insights on why the expectations you set are not met.

## How can I assert that a function is NEVER called? ##

```
EXPECT_CALL(foo, Bar(_))
    .Times(0);
```

## I have a failed test where Google Mock tells me TWICE that a particular expectation is not satisfied.  Isn't this redundant? ##

When Google Mock detects a failure, it prints relevant information
(the mock function arguments, the state of relevant expectations, and
etc) to help the user debug.  If another failure is detected, Google
Mock will do the same, including printing the state of relevant
expectations.

Sometimes an expectation's state didn't change between two failures,
and you'll see the same description of the state twice.  They are
however _not_ redundant, as they refer to _different points in time_.
The fact they are the same _is_ interesting information.

## I get a heap check failure when using a mock object, but using a real object is fine.  What can be wrong? ##

Does the class (hopefully a pure interface) you are mocking have a
virtual destructor?

Whenever you derive from a base class, make sure its destructor is
virtual.  Otherwise Bad Things will happen.  Consider the following
code:

```
class Base {
 public:
  // Not virtual, but should be.
  ~Base() { ... }
  ...
};

class Derived : public Base {
 public:
  ...
 private:
  std::string value_;
};

...
  Base* p = new Derived;
  ...
  delete p;  // Surprise! ~Base() will be called, but ~Derived() will not
             // - value_ is leaked.
```

By changing `~Base()` to virtual, `~Derived()` will be correctly
called when `delete p` is executed, and the heap checker
will be happy.

## The "newer expectations override older ones" rule makes writing expectations awkward.  Why does Google Mock do that? ##

When people complain about this, often they are referring to code like:

```
// foo.Bar() should be called twice, return 1 the first time, and return
// 2 the second time.  However, I have to write the expectations in the
// reverse order.  This sucks big time!!!
EXPECT_CALL(foo, Bar())
    .WillOnce(Return(2))
    .RetiresOnSaturation();
EXPECT_CALL(foo, Bar())
    .WillOnce(Return(1))
    .RetiresOnSaturation();
```

The problem is that they didn't pick the **best** way to express the test's
intent.

By default, expectations don't have to be matched in _any_ particular
order.  If you want them to match in a certain order, you need to be
explicit.  This is Google Mock's (and jMock's) fundamental philosophy: it's
easy to accidentally over-specify your tests, and we want to make it
harder to do so.

There are two better ways to write the test spec.  You could either
put the expectations in sequence:

```
// foo.Bar() should be called twice, return 1 the first time, and return
// 2 the second time.  Using a sequence, we can write the expectations
// in their natural order.
{
  InSequence s;
  EXPECT_CALL(foo, Bar())
      .WillOnce(Return(1))
      .RetiresOnSaturation();
  EXPECT_CALL(foo, Bar())
      .WillOnce(Return(2))
      .RetiresOnSaturation();
}
```

or you can put the sequence of actions in the same expectation:

```
// foo.Bar() should be called twice, return 1 the first time, and return
// 2 the second time.
EXPECT_CALL(foo, Bar())
    .WillOnce(Return(1))
    .WillOnce(Return(2))
    .RetiresOnSaturation();
```

Back to the original questions: why does Google Mock search the
expectations (and `ON_CALL`s) from back to front?  Because this
allows a user to set up a mock's behavior for the common case early
(e.g. in the mock's constructor or the test fixture's set-up phase)
and customize it with more specific rules later.  If Google Mock
searches from front to back, this very useful pattern won't be
possible.

## Google Mock prints a warning when a function without EXPECT\_CALL is called, even if I have set its behavior using ON\_CALL.  Would it be reasonable not to show the warning in this case? ##

When choosing between being neat and being safe, we lean toward the
latter.  So the answer is that we think it's better to show the
warning.

Often people write `ON_CALL`s in the mock object's
constructor or `SetUp()`, as the default behavior rarely changes from
test to test.  Then in the test body they set the expectations, which
are often different for each test.  Having an `ON_CALL` in the set-up
part of a test doesn't mean that the calls are expected.  If there's
no `EXPECT_CALL` and the method is called, it's possibly an error.  If
we quietly let the call go through without notifying the user, bugs
may creep in unnoticed.

If, however, you are sure that the calls are OK, you can write

```
EXPECT_CALL(foo, Bar(_))
    .WillRepeatedly(...);
```

instead of

```
ON_CALL(foo, Bar(_))
    .WillByDefault(...);
```

This tells Google Mock that you do expect the calls and no warning should be
printed.

Also, you can control the verbosity using the `--gmock_verbose` flag.
If you find the output too noisy when debugging, just choose a less
verbose level.

## How can I delete the mock function's argument in an action? ##

If you find yourself needing to perform some action that's not
supported by Google Mock directly, remember that you can define your own
actions using
[MakeAction()](CookBook.md#writing-new-actions) or
[MakePolymorphicAction()](CookBook.md#writing_new_polymorphic_actions),
or you can write a stub function and invoke it using
[Invoke()](CookBook.md#using-functions_methods_functors).

## MOCK\_METHODn()'s second argument looks funny.  Why don't you use the MOCK\_METHODn(Method, return\_type, arg\_1, ..., arg\_n) syntax? ##

What?!  I think it's beautiful. :-)

While which syntax looks more natural is a subjective matter to some
extent, Google Mock's syntax was chosen for several practical advantages it
has.

Try to mock a function that takes a map as an argument:
```
virtual int GetSize(const map<int, std::string>& m);
```

Using the proposed syntax, it would be:
```
MOCK_METHOD1(GetSize, int, const map<int, std::string>& m);
```

Guess what?  You'll get a compiler error as the compiler thinks that
`const map<int, std::string>& m` are **two**, not one, arguments. To work
around this you can use `typedef` to give the map type a name, but
that gets in the way of your work.  Google Mock's syntax avoids this
problem as the function's argument types are protected inside a pair
of parentheses:
```
// This compiles fine.
MOCK_METHOD1(GetSize, int(const map<int, std::string>& m));
```

You still need a `typedef` if the return type contains an unprotected
comma, but that's much rarer.

Other advantages include:
  1. `MOCK_METHOD1(Foo, int, bool)` can leave a reader wonder whether the method returns `int` or `bool`, while there won't be such confusion using Google Mock's syntax.
  1. The way Google Mock describes a function type is nothing new, although many people may not be familiar with it.  The same syntax was used in C, and the `function` library in `tr1` uses this syntax extensively.  Since `tr1` will become a part of the new version of STL, we feel very comfortable to be consistent with it.
  1. The function type syntax is also used in other parts of Google Mock's API (e.g. the action interface) in order to make the implementation tractable. A user needs to learn it anyway in order to utilize Google Mock's more advanced features.  We'd as well stick to the same syntax in `MOCK_METHOD*`!

## My code calls a static/global function.  Can I mock it? ##

You can, but you need to make some changes.

In general, if you find yourself needing to mock a static function,
it's a sign that your modules are too tightly coupled (and less
flexible, less reusable, less testable, etc).  You are probably better
off defining a small interface and call the function through that
interface, which then can be easily mocked.  It's a bit of work
initially, but usually pays for itself quickly.

This Google Testing Blog
[post](http://googletesting.blogspot.com/2008/06/defeat-static-cling.html)
says it excellently.  Check it out.

## My mock object needs to do complex stuff.  It's a lot of pain to specify the actions.  Google Mock sucks! ##

I know it's not a question, but you get an answer for free any way. :-)

With Google Mock, you can create mocks in C++ easily.  And people might be
tempted to use them everywhere. Sometimes they work great, and
sometimes you may find them, well, a pain to use. So, what's wrong in
the latter case?

When you write a test without using mocks, you exercise the code and
assert that it returns the correct value or that the system is in an
expected state.  This is sometimes called "state-based testing".

Mocks are great for what some call "interaction-based" testing:
instead of checking the system state at the very end, mock objects
verify that they are invoked the right way and report an error as soon
as it arises, giving you a handle on the precise context in which the
error was triggered.  This is often more effective and economical to
do than state-based testing.

If you are doing state-based testing and using a test double just to
simulate the real object, you are probably better off using a fake.
Using a mock in this case causes pain, as it's not a strong point for
mocks to perform complex actions.  If you experience this and think
that mocks suck, you are just not using the right tool for your
problem. Or, you might be trying to solve the wrong problem. :-)

## I got a warning "Uninteresting function call encountered - default action taken.."  Should I panic? ##

By all means, NO!  It's just an FYI.

What it means is that you have a mock function, you haven't set any
expectations on it (by Google Mock's rule this means that you are not
interested in calls to this function and therefore it can be called
any number of times), and it is called.  That's OK - you didn't say
it's not OK to call the function!

What if you actually meant to disallow this function to be called, but
forgot to write `EXPECT_CALL(foo, Bar()).Times(0)`?  While
one can argue that it's the user's fault, Google Mock tries to be nice and
prints you a note.

So, when you see the message and believe that there shouldn't be any
uninteresting calls, you should investigate what's going on.  To make
your life easier, Google Mock prints the function name and arguments
when an uninteresting call is encountered.

## I want to define a custom action.  Should I use Invoke() or implement the action interface? ##

Either way is fine - you want to choose the one that's more convenient
for your circumstance.

Usually, if your action is for a particular function type, defining it
using `Invoke()` should be easier; if your action can be used in
functions of different types (e.g. if you are defining
`Return(value)`), `MakePolymorphicAction()` is
easiest.  Sometimes you want precise control on what types of
functions the action can be used in, and implementing
`ActionInterface` is the way to go here. See the implementation of
`Return()` in `include/gmock/gmock-actions.h` for an example.

## I'm using the set-argument-pointee action, and the compiler complains about "conflicting return type specified".  What does it mean? ##

You got this error as Google Mock has no idea what value it should return
when the mock method is called.  `SetArgPointee()` says what the
side effect is, but doesn't say what the return value should be.  You
need `DoAll()` to chain a `SetArgPointee()` with a `Return()`.

See this [recipe](CookBook.md#mocking_side_effects) for more details and an example.


## My question is not in your FAQ! ##

If you cannot find the answer to your question in this FAQ, there are
some other resources you can use:

  1. read other [documentation](Documentation.md),
  1. search the mailing list [archive](http://groups.google.com/group/googlemock/topics),
  1. ask it on [googlemock@googlegroups.com](mailto:googlemock@googlegroups.com) and someone will answer it (to prevent spam, we require you to join the [discussion group](http://groups.google.com/group/googlemock) before you can post.).

Please note that creating an issue in the
[issue tracker](https://github.com/google/googletest/issues) is _not_
a good way to get your answer, as it is monitored infrequently by a
very small number of people.

When asking a question, it's helpful to provide as much of the
following information as possible (people cannot help you if there's
not enough information in your question):

  * the version (or the revision number if you check out from SVN directly) of Google Mock you use (Google Mock is under active development, so it's possible that your problem has been solved in a later version),
  * your operating system,
  * the name and version of your compiler,
  * the complete command line flags you give to your compiler,
  * the complete compiler error messages (if the question is about compilation),
  * the _actual_ code (ideally, a minimal but complete program) that has the problem you encounter.
As any non-trivial software system, Google Mock has some known limitations and problems.  We are working on improving it, and welcome your help!  The follow is a list of issues we know about.



## README contains outdated information on Google Mock's compatibility with other testing frameworks ##

The `README` file in release 1.1.0 still says that Google Mock only works with Google Test.  Actually, you can configure Google Mock to work with any testing framework you choose.

## Tests failing on machines using Power PC CPUs (e.g. some Macs) ##

`gmock_output_test` and `gmock-printers_test` are known to fail with Power PC CPUs.  This is due to portability issues with these tests, and is not an indication of problems in Google Mock itself.  You can safely ignore them.

## Failed to resolve libgtest.so.0 in tests when built against installed Google Test ##

This only applies if you manually built and installed Google Test, and then built a Google Mock against it (either explicitly, or because gtest-config was in your path post-install). In this situation, Libtool has a known issue with certain systems' ldconfig setup:

http://article.gmane.org/gmane.comp.sysutils.automake.general/9025

This requires a manual run of "sudo ldconfig" after the "sudo make install" for Google Test before any binaries which link against it can be executed. This isn't a bug in our install, but we should at least have documented it or hacked a work-around into our install. We should have one of these solutions in our next release.
                                 Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/

   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
      and distribution as defined by Sections 1 through 9 of this document.

      "Licensor" shall mean the copyright owner or entity authorized by
      the copyright owner that is granting the License.

      "Legal Entity" shall mean the union of the acting entity and all
      other entities that control, are controlled by, or are under common
      control with that entity. For the purposes of this definition,
      "control" means (i) the power, direct or indirect, to cause the
      direction or management of such entity, whether by contract or
      otherwise, or (ii) ownership of fifty percent (50%) or more of the
      outstanding shares, or (iii) beneficial ownership of such entity.

      "You" (or "Your") shall mean an individual or Legal Entity
      exercising permissions granted by this License.

      "Source" form shall mean the preferred form for making modifications,
      including but not limited to software source code, documentation
      source, and configuration files.

      "Object" form shall mean any form resulting from mechanical
      transformation or translation of a Source form, including but
      not limited to compiled object code, generated documentation,
      and conversions to other media types.

      "Work" shall mean the work of authorship, whether in Source or
      Object form, made available under the License, as indicated by a
      copyright notice that is included in or attached to the work
      (an example is provided in the Appendix below).

      "Derivative Works" shall mean any work, whether in Source or Object
      form, that is based on (or derived from) the Work and for which the
      editorial revisions, annotations, elaborations, or other modifications
      represent, as a whole, an original work of authorship. For the purposes
      of this License, Derivative Works shall not include works that remain
      separable from, or merely link (or bind by name) to the interfaces of,
      the Work and Derivative Works thereof.

      "Contribution" shall mean any work of authorship, including
      the original version of the Work and any modifications or additions
      to that Work or Derivative Works thereof, that is intentionally
      submitted to Licensor for inclusion in the Work by the copyright owner
      or by an individual or Legal Entity authorized to submit on behalf of
      the copyright owner. For the purposes of this definition, "submitted"
      means any form of electronic, verbal, or written communication sent
      to the Licensor or its representatives, including but not limited to
      communication on electronic mailing lists, source code control systems,
      and issue tracking systems that are managed by, or on behalf of, the
      Licensor for the purpose of discussing and improving the Work, but
      excluding communication that is conspicuously marked or otherwise
      designated in writing by the copyright owner as "Not a Contribution."

      "Contributor" shall mean Licensor and any individual or Legal Entity
      on behalf of whom a Contribution has been received by Licensor and
      subsequently incorporated within the Work.

   2. Grant of Copyright License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      copyright license to reproduce, prepare Derivative Works of,
      publicly display, publicly perform, sublicense, and distribute the
      Work and such Derivative Works in Source or Object form.

   3. Grant of Patent License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      (except as stated in this section) patent license to make, have made,
      use, offer to sell, sell, import, and otherwise transfer the Work,
      where such license applies only to those patent claims licensable
      by such Contributor that are necessarily infringed by their
      Contribution(s) alone or by combination of their Contribution(s)
      with the Work to which such Contribution(s) was submitted. If You
      institute patent litigation against any entity (including a
      cross-claim or counterclaim in a lawsuit) alleging that the Work
      or a Contribution incorporated within the Work constitutes direct
      or contributory patent infringement, then any patent licenses
      granted to You under this License for that Work shall terminate
      as of the date such litigation is filed.

   4. Redistribution. You may reproduce and distribute copies of the
      Work or Derivative Works thereof in any medium, with or without
      modifications, and in Source or Object form, provided that You
      meet the following conditions:

      (a) You must give any other recipients of the Work or
          Derivative Works a copy of this License; and

      (b) You must cause any modified files to carry prominent notices
          stating that You changed the files; and

      (c) You must retain, in the Source form of any Derivative Works
          that You distribute, all copyright, patent, trademark, and
          attribution notices from the Source form of the Work,
          excluding those notices that do not pertain to any part of
          the Derivative Works; and

      (d) If the Work includes a "NOTICE" text file as part of its
          distribution, then any Derivative Works that You distribute must
          include a readable copy of the attribution notices contained
          within such NOTICE file, excluding those notices that do not
          pertain to any part of the Derivative Works, in at least one
          of the following places: within a NOTICE text file distributed
          as part of the Derivative Works; within the Source form or
          documentation, if provided along with the Derivative Works; or,
          within a display generated by the Derivative Works, if and
          wherever such third-party notices normally appear. The contents
          of the NOTICE file are for informational purposes only and
          do not modify the License. You may add Your own attribution
          notices within Derivative Works that You distribute, alongside
          or as an addendum to the NOTICE text from the Work, provided
          that such additional attribution notices cannot be construed
          as modifying the License.

      You may add Your own copyright statement to Your modifications and
      may provide additional or different license terms and conditions
      for use, reproduction, or distribution of Your modifications, or
      for any such Derivative Works as a whole, provided Your use,
      reproduction, and distribution of the Work otherwise complies with
      the conditions stated in this License.

   5. Submission of Contributions. Unless You explicitly state otherwise,
      any Contribution intentionally submitted for inclusion in the Work
      by You to the Licensor shall be under the terms and conditions of
      this License, without any additional terms or conditions.
      Notwithstanding the above, nothing herein shall supersede or modify
      the terms of any separate license agreement you may have executed
      with Licensor regarding such Contributions.

   6. Trademarks. This License does not grant permission to use the trade
      names, trademarks, service marks, or product names of the Licensor,
      except as required for reasonable and customary use in describing the
      origin of the Work and reproducing the content of the NOTICE file.

   7. Disclaimer of Warranty. Unless required by applicable law or
      agreed to in writing, Licensor provides the Work (and each
      Contributor provides its Contributions) on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
      implied, including, without limitation, any warranties or conditions
      of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A
      PARTICULAR PURPOSE. You are solely responsible for determining the
      appropriateness of using or redistributing the Work and assume any
      risks associated with Your exercise of permissions under this License.

   8. Limitation of Liability. In no event and under no legal theory,
      whether in tort (including negligence), contract, or otherwise,
      unless required by applicable law (such as deliberate and grossly
      negligent acts) or agreed to in writing, shall any Contributor be
      liable to You for damages, including any direct, indirect, special,
      incidental, or consequential damages of any character arising as a
      result of this License or out of the use or inability to use the
      Work (including but not limited to damages for loss of goodwill,
      work stoppage, computer failure or malfunction, or any and all
      other commercial damages or losses), even if such Contributor
      has been advised of the possibility of such damages.

   9. Accepting Warranty or Additional Liability. While redistributing
      the Work or Derivative Works thereof, You may choose to offer,
      and charge a fee for, acceptance of support, warranty, indemnity,
      or other liability obligations and/or rights consistent with this
      License. However, in accepting such obligations, You may act only
      on Your own behalf and on Your sole responsibility, not on behalf
      of any other Contributor, and only if You agree to indemnify,
      defend, and hold each Contributor harmless for any liability
      incurred by, or claims asserted against, such Contributor by reason
      of your accepting any such warranty or additional liability.

   END OF TERMS AND CONDITIONS

   APPENDIX: How to apply the Apache License to your work.

      To apply the Apache License to your work, attach the following
      boilerplate notice, with the fields enclosed by brackets "[]"
      replaced with your own identifying information. (Don't include
      the brackets!)  The text should be enclosed in the appropriate
      comment syntax for the file format. We also recommend that a
      file or class name and description of purpose be included on the
      same "printed page" as the copyright notice for easier
      identification within third-party archives.

   Copyright [2007] Neal Norwitz
   Portions Copyright [2007] Google Inc.

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.

The Google Mock class generator is an application that is part of cppclean.
For more information about cppclean, see the README.cppclean file or
visit http://code.google.com/p/cppclean/

cppclean requires Python 2.3.5 or later.  If you don't have Python installed
on your system, you will also need to install it.  You can download Python
from:  http://www.python.org/download/releases/

To use the Google Mock class generator, you need to call it
on the command line passing the header file and class for which you want
to generate a Google Mock class.

Make sure to install the scripts somewhere in your path.  Then you can
run the program.

  gmock_gen.py header-file.h [ClassName]...

If no ClassNames are specified, all classes in the file are emitted.

To change the indentation from the default of 2, set INDENT in
the environment.  For example to use an indent of 4 spaces:

INDENT=4 gmock_gen.py header-file.h ClassName

This version was made from SVN revision 281 in the cppclean repository.

Known Limitations
-----------------
Not all code will be generated properly.  For example, when mocking templated
classes, the template information is lost.  You will need to add the template
information manually.

Not all permutations of using multiple pointers/references will be rendered
properly.  These will also have to be fixed manually.
Goal:
-----
  CppClean attempts to find problems in C++ source that slow development
  in large code bases, for example various forms of unused code.
  Unused code can be unused functions, methods, data members, types, etc
  to unnecessary #include directives.  Unnecessary #includes can cause
  considerable extra compiles increasing the edit-compile-run cycle.

  The project home page is:   http://code.google.com/p/cppclean/


Features:
---------
 * Find and print C++ language constructs: classes, methods, functions, etc.
 * Find classes with virtual methods, no virtual destructor, and no bases
 * Find global/static data that are potential problems when using threads
 * Unnecessary forward class declarations
 * Unnecessary function declarations
 * Undeclared function definitions
 * (planned) Find unnecessary header files #included
   - No direct reference to anything in the header
   - Header is unnecessary if classes were forward declared instead
 * (planned) Source files that reference headers not directly #included,
   ie, files that rely on a transitive #include from another header
 * (planned) Unused members (private, protected, & public) methods and data
 * (planned) Store AST in a SQL database so relationships can be queried

AST is Abstract Syntax Tree, a representation of parsed source code.
http://en.wikipedia.org/wiki/Abstract_syntax_tree


System Requirements:
--------------------
 * Python 2.4 or later (2.3 probably works too)
 * Works on Windows (untested), Mac OS X, and Unix


How to Run:
-----------
  For all examples, it is assumed that cppclean resides in a directory called
  /cppclean.

  To print warnings for classes with virtual methods, no virtual destructor and
  no base classes:

      /cppclean/run.sh nonvirtual_dtors.py file1.h file2.h file3.cc ...

  To print all the functions defined in header file(s):

      /cppclean/run.sh functions.py file1.h file2.h ...

  All the commands take multiple files on the command line.  Other programs
  include: find_warnings, headers, methods, and types.  Some other programs
  are available, but used primarily for debugging.

  run.sh is a simple wrapper that sets PYTHONPATH to /cppclean and then
  runs the program in /cppclean/cpp/PROGRAM.py.  There is currently
  no equivalent for Windows.  Contributions for a run.bat file
  would be greatly appreciated.


How to Configure:
-----------------
  You can add a siteheaders.py file in /cppclean/cpp to configure where
  to look for other headers (typically -I options passed to a compiler).
  Currently two values are supported:  _TRANSITIVE and GetIncludeDirs.
  _TRANSITIVE should be set to a boolean value (True or False) indicating
  whether to transitively process all header files.  The default is False.

  GetIncludeDirs is a function that takes a single argument and returns
  a sequence of directories to include.  This can be a generator or
  return a static list.

      def GetIncludeDirs(filename):
          return ['/some/path/with/other/headers']

      # Here is a more complicated example.
      def GetIncludeDirs(filename):
          yield '/path1'
          yield os.path.join('/path2', os.path.dirname(filename))
          yield '/path3'


How to Test:
------------
  For all examples, it is assumed that cppclean resides in a directory called
  /cppclean.  The tests require

  cd /cppclean
  make test
  # To generate expected results after a change:
  make expected


Current Status:
---------------
  The parser works pretty well for header files, parsing about 99% of Google's
  header files.  Anything which inspects structure of C++ source files should
  work reasonably well.  Function bodies are not transformed to an AST,
  but left as tokens.  Much work is still needed on finding unused header files
  and storing an AST in a database.


Non-goals:
----------
 * Parsing all valid C++ source
 * Handling invalid C++ source gracefully
 * Compiling to machine code (or anything beyond an AST)


Contact:
--------
  If you used cppclean, I would love to hear about your experiences
  cppclean@googlegroups.com.  Even if you don't use cppclean, I'd like to
  hear from you.  :-)  (You can contact me directly at:  nnorwitz@gmail.com)
[ RUN      ] GMockOutputTest.ExpectedCall

FILE:#: EXPECT_CALL(foo_, Bar2(0, _)) invoked
Stack trace:

FILE:#: Mock function call matches EXPECT_CALL(foo_, Bar2(0, _))...
    Function call: Bar2(0, 0)
          Returns: false
Stack trace:
[       OK ] GMockOutputTest.ExpectedCall
[ RUN      ] GMockOutputTest.ExpectedCallToVoidFunction

FILE:#: EXPECT_CALL(foo_, Bar3(0, _)) invoked
Stack trace:

FILE:#: Mock function call matches EXPECT_CALL(foo_, Bar3(0, _))...
    Function call: Bar3(0, 0)
Stack trace:
[       OK ] GMockOutputTest.ExpectedCallToVoidFunction
[ RUN      ] GMockOutputTest.ExplicitActionsRunOut

GMOCK WARNING:
FILE:#: Too few actions specified in EXPECT_CALL(foo_, Bar2(_, _))...
Expected to be called twice, but has only 1 WillOnce().
GMOCK WARNING:
FILE:#: Actions ran out in EXPECT_CALL(foo_, Bar2(_, _))...
Called 2 times, but only 1 WillOnce() is specified - returning default value.
Stack trace:
[       OK ] GMockOutputTest.ExplicitActionsRunOut
[ RUN      ] GMockOutputTest.UnexpectedCall
unknown file: Failure

Unexpected mock function call - returning default value.
    Function call: Bar2(1, 0)
          Returns: false
Google Mock tried the following 1 expectation, but it didn't match:

FILE:#: EXPECT_CALL(foo_, Bar2(0, _))...
  Expected arg #0: is equal to 0
           Actual: 1
         Expected: to be called once
           Actual: never called - unsatisfied and active
[  FAILED  ] GMockOutputTest.UnexpectedCall
[ RUN      ] GMockOutputTest.UnexpectedCallToVoidFunction
unknown file: Failure

Unexpected mock function call - returning directly.
    Function call: Bar3(1, 0)
Google Mock tried the following 1 expectation, but it didn't match:

FILE:#: EXPECT_CALL(foo_, Bar3(0, _))...
  Expected arg #0: is equal to 0
           Actual: 1
         Expected: to be called once
           Actual: never called - unsatisfied and active
[  FAILED  ] GMockOutputTest.UnexpectedCallToVoidFunction
[ RUN      ] GMockOutputTest.ExcessiveCall
FILE:#: Failure
Mock function called more times than expected - returning default value.
    Function call: Bar2(0, 1)
          Returns: false
         Expected: to be called once
           Actual: called twice - over-saturated and active
[  FAILED  ] GMockOutputTest.ExcessiveCall
[ RUN      ] GMockOutputTest.ExcessiveCallToVoidFunction
FILE:#: Failure
Mock function called more times than expected - returning directly.
    Function call: Bar3(0, 1)
         Expected: to be called once
           Actual: called twice - over-saturated and active
[  FAILED  ] GMockOutputTest.ExcessiveCallToVoidFunction
[ RUN      ] GMockOutputTest.UninterestingCall

GMOCK WARNING:
Uninteresting mock function call - returning default value.
    Function call: Bar2(0, 1)
          Returns: false
NOTE: You can safely ignore the above warning unless this call should not happen.  Do not suppress it by blindly adding an EXPECT_CALL() if you don't mean to enforce the call.  See https://github.com/google/googletest/blob/master/googlemock/docs/CookBook.md#knowing-when-to-expect for details.
[       OK ] GMockOutputTest.UninterestingCall
[ RUN      ] GMockOutputTest.UninterestingCallToVoidFunction

GMOCK WARNING:
Uninteresting mock function call - returning directly.
    Function call: Bar3(0, 1)
NOTE: You can safely ignore the above warning unless this call should not happen.  Do not suppress it by blindly adding an EXPECT_CALL() if you don't mean to enforce the call.  See https://github.com/google/googletest/blob/master/googlemock/docs/CookBook.md#knowing-when-to-expect for details.
[       OK ] GMockOutputTest.UninterestingCallToVoidFunction
[ RUN      ] GMockOutputTest.RetiredExpectation
unknown file: Failure

Unexpected mock function call - returning default value.
    Function call: Bar2(1, 1)
          Returns: false
Google Mock tried the following 2 expectations, but none matched:

FILE:#: tried expectation #0: EXPECT_CALL(foo_, Bar2(_, _))...
         Expected: the expectation is active
           Actual: it is retired
         Expected: to be called once
           Actual: called once - saturated and retired
FILE:#: tried expectation #1: EXPECT_CALL(foo_, Bar2(0, 0))...
  Expected arg #0: is equal to 0
           Actual: 1
  Expected arg #1: is equal to 0
           Actual: 1
         Expected: to be called once
           Actual: never called - unsatisfied and active
[  FAILED  ] GMockOutputTest.RetiredExpectation
[ RUN      ] GMockOutputTest.UnsatisfiedPrerequisite
unknown file: Failure

Unexpected mock function call - returning default value.
    Function call: Bar2(1, 0)
          Returns: false
Google Mock tried the following 2 expectations, but none matched:

FILE:#: tried expectation #0: EXPECT_CALL(foo_, Bar2(0, 0))...
  Expected arg #0: is equal to 0
           Actual: 1
         Expected: to be called once
           Actual: never called - unsatisfied and active
FILE:#: tried expectation #1: EXPECT_CALL(foo_, Bar2(1, _))...
         Expected: all pre-requisites are satisfied
           Actual: the following immediate pre-requisites are not satisfied:
FILE:#: pre-requisite #0
                   (end of pre-requisites)
         Expected: to be called once
           Actual: never called - unsatisfied and active
[  FAILED  ] GMockOutputTest.UnsatisfiedPrerequisite
[ RUN      ] GMockOutputTest.UnsatisfiedPrerequisites
unknown file: Failure

Unexpected mock function call - returning default value.
    Function call: Bar2(1, 0)
          Returns: false
Google Mock tried the following 2 expectations, but none matched:

FILE:#: tried expectation #0: EXPECT_CALL(foo_, Bar2(0, 0))...
  Expected arg #0: is equal to 0
           Actual: 1
         Expected: to be called once
           Actual: never called - unsatisfied and active
FILE:#: tried expectation #1: EXPECT_CALL(foo_, Bar2(1, _))...
         Expected: all pre-requisites are satisfied
           Actual: the following immediate pre-requisites are not satisfied:
FILE:#: pre-requisite #0
FILE:#: pre-requisite #1
                   (end of pre-requisites)
         Expected: to be called once
           Actual: never called - unsatisfied and active
[  FAILED  ] GMockOutputTest.UnsatisfiedPrerequisites
[ RUN      ] GMockOutputTest.UnsatisfiedWith
FILE:#: Failure
Actual function call count doesn't match EXPECT_CALL(foo_, Bar2(_, _))...
    Expected args: are a pair where the first >= the second
         Expected: to be called once
           Actual: never called - unsatisfied and active
[  FAILED  ] GMockOutputTest.UnsatisfiedWith
[ RUN      ] GMockOutputTest.UnsatisfiedExpectation
FILE:#: Failure
Actual function call count doesn't match EXPECT_CALL(foo_, Bar2(0, _))...
         Expected: to be called twice
           Actual: called once - unsatisfied and active
FILE:#: Failure
Actual function call count doesn't match EXPECT_CALL(foo_, Bar(_, _, _))...
         Expected: to be called once
           Actual: never called - unsatisfied and active
[  FAILED  ] GMockOutputTest.UnsatisfiedExpectation
[ RUN      ] GMockOutputTest.MismatchArguments
unknown file: Failure

Unexpected mock function call - returning default value.
    Function call: Bar(@0x# "Ho", 0, -0.1)
          Returns: '\0'
Google Mock tried the following 1 expectation, but it didn't match:

FILE:#: EXPECT_CALL(foo_, Bar(Ref(s), _, Ge(0)))...
  Expected arg #0: references the variable @0x# "Hi"
           Actual: "Ho", which is located @0x#
  Expected arg #2: is >= 0
           Actual: -0.1
         Expected: to be called once
           Actual: never called - unsatisfied and active
[  FAILED  ] GMockOutputTest.MismatchArguments
[ RUN      ] GMockOutputTest.MismatchWith
unknown file: Failure

Unexpected mock function call - returning default value.
    Function call: Bar2(2, 3)
          Returns: false
Google Mock tried the following 1 expectation, but it didn't match:

FILE:#: EXPECT_CALL(foo_, Bar2(Ge(2), Ge(1)))...
    Expected args: are a pair where the first >= the second
           Actual: don't match
         Expected: to be called once
           Actual: never called - unsatisfied and active
[  FAILED  ] GMockOutputTest.MismatchWith
[ RUN      ] GMockOutputTest.MismatchArgumentsAndWith
unknown file: Failure

Unexpected mock function call - returning default value.
    Function call: Bar2(1, 3)
          Returns: false
Google Mock tried the following 1 expectation, but it didn't match:

FILE:#: EXPECT_CALL(foo_, Bar2(Ge(2), Ge(1)))...
  Expected arg #0: is >= 2
           Actual: 1
    Expected args: are a pair where the first >= the second
           Actual: don't match
         Expected: to be called once
           Actual: never called - unsatisfied and active
[  FAILED  ] GMockOutputTest.MismatchArgumentsAndWith
[ RUN      ] GMockOutputTest.UnexpectedCallWithDefaultAction
unknown file: Failure

Unexpected mock function call - taking default action specified at:
FILE:#:
    Function call: Bar2(1, 0)
          Returns: false
Google Mock tried the following 1 expectation, but it didn't match:

FILE:#: EXPECT_CALL(foo_, Bar2(2, 2))...
  Expected arg #0: is equal to 2
           Actual: 1
  Expected arg #1: is equal to 2
           Actual: 0
         Expected: to be called once
           Actual: never called - unsatisfied and active
unknown file: Failure

Unexpected mock function call - taking default action specified at:
FILE:#:
    Function call: Bar2(0, 0)
          Returns: true
Google Mock tried the following 1 expectation, but it didn't match:

FILE:#: EXPECT_CALL(foo_, Bar2(2, 2))...
  Expected arg #0: is equal to 2
           Actual: 0
  Expected arg #1: is equal to 2
           Actual: 0
         Expected: to be called once
           Actual: never called - unsatisfied and active
[  FAILED  ] GMockOutputTest.UnexpectedCallWithDefaultAction
[ RUN      ] GMockOutputTest.ExcessiveCallWithDefaultAction
FILE:#: Failure
Mock function called more times than expected - taking default action specified at:
FILE:#:
    Function call: Bar2(2, 2)
          Returns: true
         Expected: to be called once
           Actual: called twice - over-saturated and active
FILE:#: Failure
Mock function called more times than expected - taking default action specified at:
FILE:#:
    Function call: Bar2(1, 1)
          Returns: false
         Expected: to be called once
           Actual: called twice - over-saturated and active
[  FAILED  ] GMockOutputTest.ExcessiveCallWithDefaultAction
[ RUN      ] GMockOutputTest.UninterestingCallWithDefaultAction

GMOCK WARNING:
Uninteresting mock function call - taking default action specified at:
FILE:#:
    Function call: Bar2(2, 2)
          Returns: true
NOTE: You can safely ignore the above warning unless this call should not happen.  Do not suppress it by blindly adding an EXPECT_CALL() if you don't mean to enforce the call.  See https://github.com/google/googletest/blob/master/googlemock/docs/CookBook.md#knowing-when-to-expect for details.

GMOCK WARNING:
Uninteresting mock function call - taking default action specified at:
FILE:#:
    Function call: Bar2(1, 1)
          Returns: false
NOTE: You can safely ignore the above warning unless this call should not happen.  Do not suppress it by blindly adding an EXPECT_CALL() if you don't mean to enforce the call.  See https://github.com/google/googletest/blob/master/googlemock/docs/CookBook.md#knowing-when-to-expect for details.
[       OK ] GMockOutputTest.UninterestingCallWithDefaultAction
[ RUN      ] GMockOutputTest.ExplicitActionsRunOutWithDefaultAction

GMOCK WARNING:
FILE:#: Too few actions specified in EXPECT_CALL(foo_, Bar2(_, _))...
Expected to be called twice, but has only 1 WillOnce().
GMOCK WARNING:
FILE:#: Actions ran out in EXPECT_CALL(foo_, Bar2(_, _))...
Called 2 times, but only 1 WillOnce() is specified - taking default action specified at:
FILE:#:
Stack trace:
[       OK ] GMockOutputTest.ExplicitActionsRunOutWithDefaultAction
[ RUN      ] GMockOutputTest.CatchesLeakedMocks
[       OK ] GMockOutputTest.CatchesLeakedMocks
[  FAILED  ] GMockOutputTest.UnexpectedCall
[  FAILED  ] GMockOutputTest.UnexpectedCallToVoidFunction
[  FAILED  ] GMockOutputTest.ExcessiveCall
[  FAILED  ] GMockOutputTest.ExcessiveCallToVoidFunction
[  FAILED  ] GMockOutputTest.RetiredExpectation
[  FAILED  ] GMockOutputTest.UnsatisfiedPrerequisite
[  FAILED  ] GMockOutputTest.UnsatisfiedPrerequisites
[  FAILED  ] GMockOutputTest.UnsatisfiedWith
[  FAILED  ] GMockOutputTest.UnsatisfiedExpectation
[  FAILED  ] GMockOutputTest.MismatchArguments
[  FAILED  ] GMockOutputTest.MismatchWith
[  FAILED  ] GMockOutputTest.MismatchArgumentsAndWith
[  FAILED  ] GMockOutputTest.UnexpectedCallWithDefaultAction
[  FAILED  ] GMockOutputTest.ExcessiveCallWithDefaultAction


FILE:#: ERROR: this mock object should be deleted but never is. Its address is @0x#.
FILE:#: ERROR: this mock object should be deleted but never is. Its address is @0x#.
FILE:#: ERROR: this mock object should be deleted but never is. Its address is @0x#.
ERROR: 3 leaked mock objects found at program exit.
########################################################################
# CMake build script for Google Test.
#
# To run the tests for Google Test itself on Linux, use 'make test' or
# ctest.  You can select which tests to run using 'ctest -R regex'.
# For more options, run 'ctest --help'.

# BUILD_SHARED_LIBS is a standard CMake variable, but we declare it here to
# make it prominent in the GUI.
option(BUILD_SHARED_LIBS "Build shared libraries (DLLs)." OFF)
set(BUILD_SHARED_LIBS OFF)

# When other libraries are using a shared version of runtime libraries,
# Google Test also has to use one.
option(
  gtest_force_shared_crt
  "Use shared (DLL) run-time lib even when Google Test is built as static lib."
  OFF)

option(gtest_build_tests "Build all of gtest's own tests." OFF)

option(gtest_build_samples "Build gtest's sample programs." OFF)

option(gtest_disable_pthreads "Disable uses of pthreads in gtest." OFF)

option(
  gtest_hide_internal_symbols
  "Build gtest with internal symbols hidden in shared libraries."
  OFF)

set(CMAKE_DEBUG_POSTFIX "d" CACHE STRING "Generate debug library name with a postfix.")

# Defines pre_project_set_up_hermetic_build() and set_up_hermetic_build().
include(cmake/hermetic_build.cmake OPTIONAL)

if (COMMAND pre_project_set_up_hermetic_build)
  pre_project_set_up_hermetic_build()
endif()

########################################################################
#
# Project-wide settings

# Name of the project.
#
# CMake files in this project can refer to the root source directory
# as ${gtest_SOURCE_DIR} and to the root binary directory as
# ${gtest_BINARY_DIR}.
# Language "C" is required for find_package(Threads).
if (CMAKE_VERSION VERSION_LESS 3.0)
  project(gtest CXX C)
else()
  cmake_policy(SET CMP0048 NEW)
  project(gtest VERSION 1.9.0 LANGUAGES CXX C)
endif()
cmake_minimum_required(VERSION 2.6.4)

if (POLICY CMP0063) # Visibility
  cmake_policy(SET CMP0063 NEW)
endif (POLICY CMP0063)

if (COMMAND set_up_hermetic_build)
  set_up_hermetic_build()
endif()

if (gtest_hide_internal_symbols)
  set(CMAKE_CXX_VISIBILITY_PRESET hidden)
  set(CMAKE_VISIBILITY_INLINES_HIDDEN 1)
endif()

# Define helper functions and macros used by Google Test.
include(cmake/internal_utils.cmake)

config_compiler_and_linker()  # Defined in internal_utils.cmake.

# Where Google Test's .h files can be found.
include_directories(
  ${gtest_SOURCE_DIR}/include
  ${gtest_SOURCE_DIR})

# Summary of tuple support for Microsoft Visual Studio:
# Compiler    version(MS)  version(cmake)  Support
# ----------  -----------  --------------  -----------------------------
# <= VS 2010  <= 10        <= 1600         Use Google Tests's own tuple.
# VS 2012     11           1700            std::tr1::tuple + _VARIADIC_MAX=10
# VS 2013     12           1800            std::tr1::tuple
# VS 2015     14           1900            std::tuple
# VS 2017     15           >= 1910         std::tuple
if (MSVC AND MSVC_VERSION EQUAL 1700)
  add_definitions(/D _VARIADIC_MAX=10)
endif()

########################################################################
#
# Defines the gtest & gtest_main libraries.  User tests should link
# with one of them.

set(CMAKE_MACOSX_RPATH OFF)

# Google Test libraries.  We build them using more strict warnings than what
# are used for other targets, to ensure that gtest can be compiled by a user
# aggressive about warnings.
cxx_library(gtest "${cxx_strict}" src/gtest-all.cc)
cxx_library(gtest_main "${cxx_strict}" src/gtest_main.cc)
target_link_libraries(gtest_main gtest)
set_target_properties(gtest_main PROPERTIES FOLDER "Tests")
set_target_properties(gtest      PROPERTIES FOLDER "Tests")

# If the CMake version supports it, attach header directory information
# to the targets for when we are part of a parent build (ie being pulled
# in via add_subdirectory() rather than being a standalone build).
if (DEFINED CMAKE_VERSION AND NOT "${CMAKE_VERSION}" VERSION_LESS "2.8.11")
  target_include_directories(gtest      SYSTEM INTERFACE "${gtest_SOURCE_DIR}/include")
  target_include_directories(gtest_main SYSTEM INTERFACE "${gtest_SOURCE_DIR}/include")
endif()

########################################################################
#
# Install rules
# if(INSTALL_GTEST)
#   install(TARGETS gtest gtest_main
#     RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
#     ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
#     LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})
#   install(DIRECTORY ${gtest_SOURCE_DIR}/include/gtest
#     DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

#   # configure and install pkgconfig files
#   configure_file(
#     cmake/gtest.pc.in
#     "${CMAKE_BINARY_DIR}/gtest.pc"
#     @ONLY)
#   configure_file(
#     cmake/gtest_main.pc.in
#     "${CMAKE_BINARY_DIR}/gtest_main.pc"
#     @ONLY)
#   install(FILES "${CMAKE_BINARY_DIR}/gtest.pc" "${CMAKE_BINARY_DIR}/gtest_main.pc"
#     DESTINATION "${CMAKE_INSTALL_LIBDIR}/pkgconfig")
# endif()

########################################################################
#
# Samples on how to link user tests with gtest or gtest_main.
#
# They are not built by default.  To build them, set the
# gtest_build_samples option to ON.  You can do it by running ccmake
# or specifying the -Dgtest_build_samples=ON flag when running cmake.

if (gtest_build_samples)
  cxx_executable(sample1_unittest samples gtest_main samples/sample1.cc)
  cxx_executable(sample2_unittest samples gtest_main samples/sample2.cc)
  cxx_executable(sample3_unittest samples gtest_main)
  cxx_executable(sample4_unittest samples gtest_main samples/sample4.cc)
  cxx_executable(sample5_unittest samples gtest_main samples/sample1.cc)
  cxx_executable(sample6_unittest samples gtest_main)
  cxx_executable(sample7_unittest samples gtest_main)
  cxx_executable(sample8_unittest samples gtest_main)
  cxx_executable(sample9_unittest samples gtest)
  cxx_executable(sample10_unittest samples gtest)
endif()

########################################################################
#
# Google Test's own tests.
#
# You can skip this section if you aren't interested in testing
# Google Test itself.
#
# The tests are not built by default.  To build them, set the
# gtest_build_tests option to ON.  You can do it by running ccmake
# or specifying the -Dgtest_build_tests=ON flag when running cmake.

if (gtest_build_tests)
  # This must be set in the root directory for the tests to be run by
  # 'make test' or ctest.
  enable_testing()

  ############################################################
  # C++ tests built with standard compiler flags.

  cxx_test(gtest-death-test_test gtest_main)
  cxx_test(gtest_environment_test gtest)
  cxx_test(gtest-filepath_test gtest_main)
  cxx_test(gtest-linked_ptr_test gtest_main)
  cxx_test(gtest-listener_test gtest_main)
  cxx_test(gtest_main_unittest gtest_main)
  cxx_test(gtest-message_test gtest_main)
  cxx_test(gtest_no_test_unittest gtest)
  cxx_test(gtest-options_test gtest_main)
  cxx_test(gtest-param-test_test gtest
    test/gtest-param-test2_test.cc)
  cxx_test(gtest-port_test gtest_main)
  cxx_test(gtest_pred_impl_unittest gtest_main)
  cxx_test(gtest_premature_exit_test gtest
    test/gtest_premature_exit_test.cc)
  cxx_test(gtest-printers_test gtest_main)
  cxx_test(gtest_prod_test gtest_main
    test/production.cc)
  cxx_test(gtest_repeat_test gtest)
  cxx_test(gtest_sole_header_test gtest_main)
  cxx_test(gtest_stress_test gtest)
  cxx_test(gtest-test-part_test gtest_main)
  cxx_test(gtest_throw_on_failure_ex_test gtest)
  cxx_test(gtest-typed-test_test gtest_main
    test/gtest-typed-test2_test.cc)
  cxx_test(gtest_unittest gtest_main)
  cxx_test(gtest-unittest-api_test gtest)

  ############################################################
  # C++ tests built with non-standard compiler flags.

  # MSVC 7.1 does not support STL with exceptions disabled.
  if (NOT MSVC OR MSVC_VERSION GREATER 1310)
    cxx_library(gtest_no_exception "${cxx_no_exception}"
      src/gtest-all.cc)
    cxx_library(gtest_main_no_exception "${cxx_no_exception}"
      src/gtest-all.cc src/gtest_main.cc)
  endif()
  cxx_library(gtest_main_no_rtti "${cxx_no_rtti}"
    src/gtest-all.cc src/gtest_main.cc)

  cxx_test_with_flags(gtest-death-test_ex_nocatch_test
    "${cxx_exception} -DGTEST_ENABLE_CATCH_EXCEPTIONS_=0"
    gtest test/gtest-death-test_ex_test.cc)
  cxx_test_with_flags(gtest-death-test_ex_catch_test
    "${cxx_exception} -DGTEST_ENABLE_CATCH_EXCEPTIONS_=1"
    gtest test/gtest-death-test_ex_test.cc)

  cxx_test_with_flags(gtest_no_rtti_unittest "${cxx_no_rtti}"
    gtest_main_no_rtti test/gtest_unittest.cc)

  cxx_shared_library(gtest_dll "${cxx_default}"
    src/gtest-all.cc src/gtest_main.cc)

  cxx_executable_with_flags(gtest_dll_test_ "${cxx_default}"
    gtest_dll test/gtest_all_test.cc)
  set_target_properties(gtest_dll_test_
                        PROPERTIES
                        COMPILE_DEFINITIONS "GTEST_LINKED_AS_SHARED_LIBRARY=1")

  if (NOT MSVC OR MSVC_VERSION LESS 1600)  # 1600 is Visual Studio 2010.
    # Visual Studio 2010, 2012, and 2013 define symbols in std::tr1 that
    # conflict with our own definitions. Therefore using our own tuple does not
    # work on those compilers.
    cxx_library(gtest_main_use_own_tuple "${cxx_use_own_tuple}"
      src/gtest-all.cc src/gtest_main.cc)

    cxx_test_with_flags(gtest-tuple_test "${cxx_use_own_tuple}"
      gtest_main_use_own_tuple test/gtest-tuple_test.cc)

    cxx_test_with_flags(gtest_use_own_tuple_test "${cxx_use_own_tuple}"
      gtest_main_use_own_tuple
      test/gtest-param-test_test.cc test/gtest-param-test2_test.cc)
  endif()

  ############################################################
  # Python tests.

  cxx_executable(gtest_break_on_failure_unittest_ test gtest)
  py_test(gtest_break_on_failure_unittest)

  # Visual Studio .NET 2003 does not support STL with exceptions disabled.
  if (NOT MSVC OR MSVC_VERSION GREATER 1310)  # 1310 is Visual Studio .NET 2003
    cxx_executable_with_flags(
      gtest_catch_exceptions_no_ex_test_
      "${cxx_no_exception}"
      gtest_main_no_exception
      test/gtest_catch_exceptions_test_.cc)
  endif()

  cxx_executable_with_flags(
    gtest_catch_exceptions_ex_test_
    "${cxx_exception}"
    gtest_main
    test/gtest_catch_exceptions_test_.cc)
  py_test(gtest_catch_exceptions_test)

  cxx_executable(gtest_color_test_ test gtest)
  py_test(gtest_color_test)

  cxx_executable(gtest_env_var_test_ test gtest)
  py_test(gtest_env_var_test)

  cxx_executable(gtest_filter_unittest_ test gtest)
  py_test(gtest_filter_unittest)

  cxx_executable(gtest_help_test_ test gtest_main)
  py_test(gtest_help_test)

  cxx_executable(gtest_list_tests_unittest_ test gtest)
  py_test(gtest_list_tests_unittest)

  cxx_executable(gtest_output_test_ test gtest)
  py_test(gtest_output_test)

  cxx_executable(gtest_shuffle_test_ test gtest)
  py_test(gtest_shuffle_test)

  # MSVC 7.1 does not support STL with exceptions disabled.
  if (NOT MSVC OR MSVC_VERSION GREATER 1310)
    cxx_executable(gtest_throw_on_failure_test_ test gtest_no_exception)
    set_target_properties(gtest_throw_on_failure_test_
      PROPERTIES
      COMPILE_FLAGS "${cxx_no_exception}")
    py_test(gtest_throw_on_failure_test)
  endif()

  cxx_executable(gtest_uninitialized_test_ test gtest)
  py_test(gtest_uninitialized_test)

  cxx_executable(gtest_xml_outfile1_test_ test gtest_main)
  cxx_executable(gtest_xml_outfile2_test_ test gtest_main)
  py_test(gtest_xml_outfiles_test)

  cxx_executable(gtest_xml_output_unittest_ test gtest)
  py_test(gtest_xml_output_unittest)
endif()
Copyright 2008, Google Inc.
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are
met:

    * Redistributions of source code must retain the above copyright
notice, this list of conditions and the following disclaimer.
    * Redistributions in binary form must reproduce the above
copyright notice, this list of conditions and the following disclaimer
in the documentation and/or other materials provided with the
distribution.
    * Neither the name of Google Inc. nor the names of its
contributors may be used to endorse or promote products derived from
this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
"AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

### Generic Build Instructions ###

#### Setup ####

To build Google Test and your tests that use it, you need to tell your
build system where to find its headers and source files.  The exact
way to do it depends on which build system you use, and is usually
straightforward.

#### Build ####

Suppose you put Google Test in directory `${GTEST_DIR}`.  To build it,
create a library build target (or a project as called by Visual Studio
and Xcode) to compile

    ${GTEST_DIR}/src/gtest-all.cc

with `${GTEST_DIR}/include` in the system header search path and `${GTEST_DIR}`
in the normal header search path.  Assuming a Linux-like system and gcc,
something like the following will do:

    g++ -isystem ${GTEST_DIR}/include -I${GTEST_DIR} \
        -pthread -c ${GTEST_DIR}/src/gtest-all.cc
    ar -rv libgtest.a gtest-all.o

(We need `-pthread` as Google Test uses threads.)

Next, you should compile your test source file with
`${GTEST_DIR}/include` in the system header search path, and link it
with gtest and any other necessary libraries:

    g++ -isystem ${GTEST_DIR}/include -pthread path/to/your_test.cc libgtest.a \
        -o your_test

As an example, the make/ directory contains a Makefile that you can
use to build Google Test on systems where GNU make is available
(e.g. Linux, Mac OS X, and Cygwin).  It doesn't try to build Google
Test's own tests.  Instead, it just builds the Google Test library and
a sample test.  You can use it as a starting point for your own build
script.

If the default settings are correct for your environment, the
following commands should succeed:

    cd ${GTEST_DIR}/make
    make
    ./sample1_unittest

If you see errors, try to tweak the contents of `make/Makefile` to make
them go away.  There are instructions in `make/Makefile` on how to do
it.

### Using CMake ###

Google Test comes with a CMake build script (
[CMakeLists.txt](CMakeLists.txt)) that can be used on a wide range of platforms ("C" stands for
cross-platform.). If you don't have CMake installed already, you can
download it for free from <http://www.cmake.org/>.

CMake works by generating native makefiles or build projects that can
be used in the compiler environment of your choice.  You can either
build Google Test as a standalone project or it can be incorporated
into an existing CMake build for another project.

#### Standalone CMake Project ####

When building Google Test as a standalone project, the typical
workflow starts with:

    mkdir mybuild       # Create a directory to hold the build output.
    cd mybuild
    cmake ${GTEST_DIR}  # Generate native build scripts.

If you want to build Google Test's samples, you should replace the
last command with

    cmake -Dgtest_build_samples=ON ${GTEST_DIR}

If you are on a \*nix system, you should now see a Makefile in the
current directory.  Just type 'make' to build gtest.

If you use Windows and have Visual Studio installed, a `gtest.sln` file
and several `.vcproj` files will be created.  You can then build them
using Visual Studio.

On Mac OS X with Xcode installed, a `.xcodeproj` file will be generated.

#### Incorporating Into An Existing CMake Project ####

If you want to use gtest in a project which already uses CMake, then a
more robust and flexible approach is to build gtest as part of that
project directly. This is done by making the GoogleTest source code
available to the main build and adding it using CMake's
`add_subdirectory()` command. This has the significant advantage that
the same compiler and linker settings are used between gtest and the
rest of your project, so issues associated with using incompatible
libraries (eg debug/release), etc. are avoided. This is particularly
useful on Windows. Making GoogleTest's source code available to the
main build can be done a few different ways:

* Download the GoogleTest source code manually and place it at a
  known location. This is the least flexible approach and can make
  it more difficult to use with continuous integration systems, etc.
* Embed the GoogleTest source code as a direct copy in the main
  project's source tree. This is often the simplest approach, but is
  also the hardest to keep up to date. Some organizations may not
  permit this method.
* Add GoogleTest as a git submodule or equivalent. This may not
  always be possible or appropriate. Git submodules, for example,
  have their own set of advantages and drawbacks.
* Use CMake to download GoogleTest as part of the build's configure
  step. This is just a little more complex, but doesn't have the
  limitations of the other methods.

The last of the above methods is implemented with a small piece
of CMake code in a separate file (e.g. `CMakeLists.txt.in`) which
is copied to the build area and then invoked as a sub-build
_during the CMake stage_. That directory is then pulled into the
main build with `add_subdirectory()`. For example:

New file `CMakeLists.txt.in`:

    cmake_minimum_required(VERSION 2.8.2)
 
    project(googletest-download NONE)
 
    include(ExternalProject)
    ExternalProject_Add(googletest
      GIT_REPOSITORY    https://github.com/google/googletest.git
      GIT_TAG           master
      SOURCE_DIR        "${CMAKE_BINARY_DIR}/googletest-src"
      BINARY_DIR        "${CMAKE_BINARY_DIR}/googletest-build"
      CONFIGURE_COMMAND ""
      BUILD_COMMAND     ""
      INSTALL_COMMAND   ""
      TEST_COMMAND      ""
    )
    
Existing build's `CMakeLists.txt`:

    # Download and unpack googletest at configure time
    configure_file(CMakeLists.txt.in googletest-download/CMakeLists.txt)
    execute_process(COMMAND ${CMAKE_COMMAND} -G "${CMAKE_GENERATOR}" .
      RESULT_VARIABLE result
      WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/googletest-download )
    if(result)
      message(FATAL_ERROR "CMake step for googletest failed: ${result}")
    endif()
    execute_process(COMMAND ${CMAKE_COMMAND} --build .
      RESULT_VARIABLE result
      WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/googletest-download )
    if(result)
      message(FATAL_ERROR "Build step for googletest failed: ${result}")
    endif()

    # Prevent overriding the parent project's compiler/linker
    # settings on Windows
    set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
    
    # Add googletest directly to our build. This defines
    # the gtest and gtest_main targets.
    add_subdirectory(${CMAKE_BINARY_DIR}/googletest-src
                     ${CMAKE_BINARY_DIR}/googletest-build
                     EXCLUDE_FROM_ALL)

    # The gtest/gtest_main targets carry header search path
    # dependencies automatically when using CMake 2.8.11 or
    # later. Otherwise we have to add them here ourselves.
    if (CMAKE_VERSION VERSION_LESS 2.8.11)
      include_directories("${gtest_SOURCE_DIR}/include")
    endif()

    # Now simply link against gtest or gtest_main as needed. Eg
    add_executable(example example.cpp)
    target_link_libraries(example gtest_main)
    add_test(NAME example_test COMMAND example)

Note that this approach requires CMake 2.8.2 or later due to
its use of the `ExternalProject_Add()` command. The above
technique is discussed in more detail in 
[this separate article](http://crascit.com/2015/07/25/cmake-gtest/)
which also contains a link to a fully generalized implementation
of the technique.

##### Visual Studio Dynamic vs Static Runtimes #####

By default, new Visual Studio projects link the C runtimes dynamically
but Google Test links them statically.
This will generate an error that looks something like the following:
    gtest.lib(gtest-all.obj) : error LNK2038: mismatch detected for 'RuntimeLibrary': value 'MTd_StaticDebug' doesn't match value 'MDd_DynamicDebug' in main.obj

Google Test already has a CMake option for this: `gtest_force_shared_crt`

Enabling this option will make gtest link the runtimes dynamically too,
and match the project in which it is included.

### Legacy Build Scripts ###

Before settling on CMake, we have been providing hand-maintained build
projects/scripts for Visual Studio, Xcode, and Autotools.  While we
continue to provide them for convenience, they are not actively
maintained any more.  We highly recommend that you follow the
instructions in the above sections to integrate Google Test
with your existing build system.

If you still need to use the legacy build scripts, here's how:

The msvc\ folder contains two solutions with Visual C++ projects.
Open the `gtest.sln` or `gtest-md.sln` file using Visual Studio, and you
are ready to build Google Test the same way you build any Visual
Studio project.  Files that have names ending with -md use DLL
versions of Microsoft runtime libraries (the /MD or the /MDd compiler
option).  Files without that suffix use static versions of the runtime
libraries (the /MT or the /MTd option).  Please note that one must use
the same option to compile both gtest and the test code.  If you use
Visual Studio 2005 or above, we recommend the -md version as /MD is
the default for new projects in these versions of Visual Studio.

On Mac OS X, open the `gtest.xcodeproj` in the `xcode/` folder using
Xcode.  Build the "gtest" target.  The universal binary framework will
end up in your selected build directory (selected in the Xcode
"Preferences..." -> "Building" pane and defaults to xcode/build).
Alternatively, at the command line, enter:

    xcodebuild

This will build the "Release" configuration of gtest.framework in your
default build location.  See the "xcodebuild" man page for more
information about building different configurations and building in
different locations.

If you wish to use the Google Test Xcode project with Xcode 4.x and
above, you need to either:

 * update the SDK configuration options in xcode/Config/General.xconfig.
   Comment options `SDKROOT`, `MACOS_DEPLOYMENT_TARGET`, and `GCC_VERSION`. If
   you choose this route you lose the ability to target earlier versions
   of MacOS X.
 * Install an SDK for an earlier version. This doesn't appear to be
   supported by Apple, but has been reported to work
   (http://stackoverflow.com/questions/5378518).

### Tweaking Google Test ###

Google Test can be used in diverse environments.  The default
configuration may not work (or may not work well) out of the box in
some environments.  However, you can easily tweak Google Test by
defining control macros on the compiler command line.  Generally,
these macros are named like `GTEST_XYZ` and you define them to either 1
or 0 to enable or disable a certain feature.

We list the most frequently used macros below.  For a complete list,
see file [include/gtest/internal/gtest-port.h](include/gtest/internal/gtest-port.h).

### Choosing a TR1 Tuple Library ###

Some Google Test features require the C++ Technical Report 1 (TR1)
tuple library, which is not yet available with all compilers.  The
good news is that Google Test implements a subset of TR1 tuple that's
enough for its own need, and will automatically use this when the
compiler doesn't provide TR1 tuple.

Usually you don't need to care about which tuple library Google Test
uses.  However, if your project already uses TR1 tuple, you need to
tell Google Test to use the same TR1 tuple library the rest of your
project uses, or the two tuple implementations will clash.  To do
that, add

    -DGTEST_USE_OWN_TR1_TUPLE=0

to the compiler flags while compiling Google Test and your tests.  If
you want to force Google Test to use its own tuple library, just add

    -DGTEST_USE_OWN_TR1_TUPLE=1

to the compiler flags instead.

If you don't want Google Test to use tuple at all, add

    -DGTEST_HAS_TR1_TUPLE=0

and all features using tuple will be disabled.

### Multi-threaded Tests ###

Google Test is thread-safe where the pthread library is available.
After `#include "gtest/gtest.h"`, you can check the `GTEST_IS_THREADSAFE`
macro to see whether this is the case (yes if the macro is `#defined` to
1, no if it's undefined.).

If Google Test doesn't correctly detect whether pthread is available
in your environment, you can force it with

    -DGTEST_HAS_PTHREAD=1

or

    -DGTEST_HAS_PTHREAD=0

When Google Test uses pthread, you may need to add flags to your
compiler and/or linker to select the pthread library, or you'll get
link errors.  If you use the CMake script or the deprecated Autotools
script, this is taken care of for you.  If you use your own build
script, you'll need to read your compiler and linker's manual to
figure out what flags to add.

### As a Shared Library (DLL) ###

Google Test is compact, so most users can build and link it as a
static library for the simplicity.  You can choose to use Google Test
as a shared library (known as a DLL on Windows) if you prefer.

To compile *gtest* as a shared library, add

    -DGTEST_CREATE_SHARED_LIBRARY=1

to the compiler flags.  You'll also need to tell the linker to produce
a shared library instead - consult your linker's manual for how to do
it.

To compile your *tests* that use the gtest shared library, add

    -DGTEST_LINKED_AS_SHARED_LIBRARY=1

to the compiler flags.

Note: while the above steps aren't technically necessary today when
using some compilers (e.g. GCC), they may become necessary in the
future, if we decide to improve the speed of loading the library (see
<http://gcc.gnu.org/wiki/Visibility> for details).  Therefore you are
recommended to always add the above flags when using Google Test as a
shared library.  Otherwise a future release of Google Test may break
your build script.

### Avoiding Macro Name Clashes ###

In C++, macros don't obey namespaces.  Therefore two libraries that
both define a macro of the same name will clash if you `#include` both
definitions.  In case a Google Test macro clashes with another
library, you can force Google Test to rename its macro to avoid the
conflict.

Specifically, if both Google Test and some other code define macro
FOO, you can add

    -DGTEST_DONT_DEFINE_FOO=1

to the compiler flags to tell Google Test to change the macro's name
from `FOO` to `GTEST_FOO`.  Currently `FOO` can be `FAIL`, `SUCCEED`,
or `TEST`.  For example, with `-DGTEST_DONT_DEFINE_TEST=1`, you'll
need to write

    GTEST_TEST(SomeTest, DoesThis) { ... }

instead of

    TEST(SomeTest, DoesThis) { ... }

in order to define a test.

## Developing Google Test ##

This section discusses how to make your own changes to Google Test.

### Testing Google Test Itself ###

To make sure your changes work as intended and don't break existing
functionality, you'll want to compile and run Google Test's own tests.
For that you can use CMake:

    mkdir mybuild
    cd mybuild
    cmake -Dgtest_build_tests=ON ${GTEST_DIR}

Make sure you have Python installed, as some of Google Test's tests
are written in Python.  If the cmake command complains about not being
able to find Python (`Could NOT find PythonInterp (missing:
PYTHON_EXECUTABLE)`), try telling it explicitly where your Python
executable can be found:

    cmake -DPYTHON_EXECUTABLE=path/to/python -Dgtest_build_tests=ON ${GTEST_DIR}

Next, you can build Google Test and all of its own tests.  On \*nix,
this is usually done by 'make'.  To run the tests, do

    make test

All tests should pass.

Normally you don't need to worry about regenerating the source files,
unless you need to modify them.  In that case, you should modify the
corresponding .pump files instead and run the pump.py Python script to
regenerate them.  You can find pump.py in the [scripts/](scripts/) directory.
Read the [Pump manual](docs/PumpManual.md) for how to use it.


Now that you have read [Primer](Primer.md) and learned how to write tests
using Google Test, it's time to learn some new tricks. This document
will show you more assertions as well as how to construct complex
failure messages, propagate fatal failures, reuse and speed up your
test fixtures, and use various flags with your tests.

# More Assertions #

This section covers some less frequently used, but still significant,
assertions.

## Explicit Success and Failure ##

These three assertions do not actually test a value or expression. Instead,
they generate a success or failure directly. Like the macros that actually
perform a test, you may stream a custom failure message into them.

| `SUCCEED();` |
|:-------------|

Generates a success. This does NOT make the overall test succeed. A test is
considered successful only if none of its assertions fail during its execution.

Note: `SUCCEED()` is purely documentary and currently doesn't generate any
user-visible output. However, we may add `SUCCEED()` messages to Google Test's
output in the future.

| `FAIL();`  | `ADD_FAILURE();` | `ADD_FAILURE_AT("`_file\_path_`", `_line\_number_`);` |
|:-----------|:-----------------|:------------------------------------------------------|

`FAIL()` generates a fatal failure, while `ADD_FAILURE()` and `ADD_FAILURE_AT()` generate a nonfatal
failure. These are useful when control flow, rather than a Boolean expression,
determines the test's success or failure. For example, you might want to write
something like:

```
switch(expression) {
  case 1: ... some checks ...
  case 2: ... some other checks
  ...
  default: FAIL() << "We shouldn't get here.";
}
```

Note: you can only use `FAIL()` in functions that return `void`. See the [Assertion Placement section](#assertion-placement) for more information.

_Availability_: Linux, Windows, Mac.

## Exception Assertions ##

These are for verifying that a piece of code throws (or does not
throw) an exception of the given type:

| **Fatal assertion** | **Nonfatal assertion** | **Verifies** |
|:--------------------|:-----------------------|:-------------|
| `ASSERT_THROW(`_statement_, _exception\_type_`);`  | `EXPECT_THROW(`_statement_, _exception\_type_`);`  | _statement_ throws an exception of the given type  |
| `ASSERT_ANY_THROW(`_statement_`);`                | `EXPECT_ANY_THROW(`_statement_`);`                | _statement_ throws an exception of any type        |
| `ASSERT_NO_THROW(`_statement_`);`                 | `EXPECT_NO_THROW(`_statement_`);`                 | _statement_ doesn't throw any exception            |

Examples:

```
ASSERT_THROW(Foo(5), bar_exception);

EXPECT_NO_THROW({
  int n = 5;
  Bar(&n);
});
```

_Availability_: Linux, Windows, Mac; since version 1.1.0.

## Predicate Assertions for Better Error Messages ##

Even though Google Test has a rich set of assertions, they can never be
complete, as it's impossible (nor a good idea) to anticipate all the scenarios
a user might run into. Therefore, sometimes a user has to use `EXPECT_TRUE()`
to check a complex expression, for lack of a better macro. This has the problem
of not showing you the values of the parts of the expression, making it hard to
understand what went wrong. As a workaround, some users choose to construct the
failure message by themselves, streaming it into `EXPECT_TRUE()`. However, this
is awkward especially when the expression has side-effects or is expensive to
evaluate.

Google Test gives you three different options to solve this problem:

### Using an Existing Boolean Function ###

If you already have a function or a functor that returns `bool` (or a type
that can be implicitly converted to `bool`), you can use it in a _predicate
assertion_ to get the function arguments printed for free:

| **Fatal assertion** | **Nonfatal assertion** | **Verifies** |
|:--------------------|:-----------------------|:-------------|
| `ASSERT_PRED1(`_pred1, val1_`);`       | `EXPECT_PRED1(`_pred1, val1_`);` | _pred1(val1)_ returns true |
| `ASSERT_PRED2(`_pred2, val1, val2_`);` | `EXPECT_PRED2(`_pred2, val1, val2_`);` |  _pred2(val1, val2)_ returns true |
|  ...                | ...                    | ...          |

In the above, _predn_ is an _n_-ary predicate function or functor, where
_val1_, _val2_, ..., and _valn_ are its arguments. The assertion succeeds
if the predicate returns `true` when applied to the given arguments, and fails
otherwise. When the assertion fails, it prints the value of each argument. In
either case, the arguments are evaluated exactly once.

Here's an example. Given

```
// Returns true iff m and n have no common divisors except 1.
bool MutuallyPrime(int m, int n) { ... }
const int a = 3;
const int b = 4;
const int c = 10;
```

the assertion `EXPECT_PRED2(MutuallyPrime, a, b);` will succeed, while the
assertion `EXPECT_PRED2(MutuallyPrime, b, c);` will fail with the message

<pre>
!MutuallyPrime(b, c) is false, where<br>
b is 4<br>
c is 10<br>
</pre>

**Notes:**

  1. If you see a compiler error "no matching function to call" when using `ASSERT_PRED*` or `EXPECT_PRED*`, please see [this FAQ](FAQ.md#the-compiler-complains-no-matching-function-to-call-when-i-use-assert_predn-how-do-i-fix-it) for how to resolve it.
  1. Currently we only provide predicate assertions of arity <= 5. If you need a higher-arity assertion, let us know.

_Availability_: Linux, Windows, Mac.

### Using a Function That Returns an AssertionResult ###

While `EXPECT_PRED*()` and friends are handy for a quick job, the
syntax is not satisfactory: you have to use different macros for
different arities, and it feels more like Lisp than C++.  The
`::testing::AssertionResult` class solves this problem.

An `AssertionResult` object represents the result of an assertion
(whether it's a success or a failure, and an associated message).  You
can create an `AssertionResult` using one of these factory
functions:

```
namespace testing {

// Returns an AssertionResult object to indicate that an assertion has
// succeeded.
AssertionResult AssertionSuccess();

// Returns an AssertionResult object to indicate that an assertion has
// failed.
AssertionResult AssertionFailure();

}
```

You can then use the `<<` operator to stream messages to the
`AssertionResult` object.

To provide more readable messages in Boolean assertions
(e.g. `EXPECT_TRUE()`), write a predicate function that returns
`AssertionResult` instead of `bool`. For example, if you define
`IsEven()` as:

```
::testing::AssertionResult IsEven(int n) {
  if ((n % 2) == 0)
    return ::testing::AssertionSuccess();
  else
    return ::testing::AssertionFailure() << n << " is odd";
}
```

instead of:

```
bool IsEven(int n) {
  return (n % 2) == 0;
}
```

the failed assertion `EXPECT_TRUE(IsEven(Fib(4)))` will print:

<pre>
Value of: IsEven(Fib(4))<br>
Actual: false (*3 is odd*)<br>
Expected: true<br>
</pre>

instead of a more opaque

<pre>
Value of: IsEven(Fib(4))<br>
Actual: false<br>
Expected: true<br>
</pre>

If you want informative messages in `EXPECT_FALSE` and `ASSERT_FALSE`
as well, and are fine with making the predicate slower in the success
case, you can supply a success message:

```
::testing::AssertionResult IsEven(int n) {
  if ((n % 2) == 0)
    return ::testing::AssertionSuccess() << n << " is even";
  else
    return ::testing::AssertionFailure() << n << " is odd";
}
```

Then the statement `EXPECT_FALSE(IsEven(Fib(6)))` will print

<pre>
Value of: IsEven(Fib(6))<br>
Actual: true (8 is even)<br>
Expected: false<br>
</pre>

_Availability_: Linux, Windows, Mac; since version 1.4.1.

### Using a Predicate-Formatter ###

If you find the default message generated by `(ASSERT|EXPECT)_PRED*` and
`(ASSERT|EXPECT)_(TRUE|FALSE)` unsatisfactory, or some arguments to your
predicate do not support streaming to `ostream`, you can instead use the
following _predicate-formatter assertions_ to _fully_ customize how the
message is formatted:

| **Fatal assertion** | **Nonfatal assertion** | **Verifies** |
|:--------------------|:-----------------------|:-------------|
| `ASSERT_PRED_FORMAT1(`_pred\_format1, val1_`);`        | `EXPECT_PRED_FORMAT1(`_pred\_format1, val1_`);` | _pred\_format1(val1)_ is successful |
| `ASSERT_PRED_FORMAT2(`_pred\_format2, val1, val2_`);` | `EXPECT_PRED_FORMAT2(`_pred\_format2, val1, val2_`);` | _pred\_format2(val1, val2)_ is successful |
| `...`               | `...`                  | `...`        |

The difference between this and the previous two groups of macros is that instead of
a predicate, `(ASSERT|EXPECT)_PRED_FORMAT*` take a _predicate-formatter_
(_pred\_formatn_), which is a function or functor with the signature:

`::testing::AssertionResult PredicateFormattern(const char* `_expr1_`, const char* `_expr2_`, ... const char* `_exprn_`, T1 `_val1_`, T2 `_val2_`, ... Tn `_valn_`);`

where _val1_, _val2_, ..., and _valn_ are the values of the predicate
arguments, and _expr1_, _expr2_, ..., and _exprn_ are the corresponding
expressions as they appear in the source code. The types `T1`, `T2`, ..., and
`Tn` can be either value types or reference types. For example, if an
argument has type `Foo`, you can declare it as either `Foo` or `const Foo&`,
whichever is appropriate.

A predicate-formatter returns a `::testing::AssertionResult` object to indicate
whether the assertion has succeeded or not. The only way to create such an
object is to call one of these factory functions:

As an example, let's improve the failure message in the previous example, which uses `EXPECT_PRED2()`:

```
// Returns the smallest prime common divisor of m and n,
// or 1 when m and n are mutually prime.
int SmallestPrimeCommonDivisor(int m, int n) { ... }

// A predicate-formatter for asserting that two integers are mutually prime.
::testing::AssertionResult AssertMutuallyPrime(const char* m_expr,
                                               const char* n_expr,
                                               int m,
                                               int n) {
  if (MutuallyPrime(m, n))
    return ::testing::AssertionSuccess();

  return ::testing::AssertionFailure()
      << m_expr << " and " << n_expr << " (" << m << " and " << n
      << ") are not mutually prime, " << "as they have a common divisor "
      << SmallestPrimeCommonDivisor(m, n);
}
```

With this predicate-formatter, we can use

```
EXPECT_PRED_FORMAT2(AssertMutuallyPrime, b, c);
```

to generate the message

<pre>
b and c (4 and 10) are not mutually prime, as they have a common divisor 2.<br>
</pre>

As you may have realized, many of the assertions we introduced earlier are
special cases of `(EXPECT|ASSERT)_PRED_FORMAT*`. In fact, most of them are
indeed defined using `(EXPECT|ASSERT)_PRED_FORMAT*`.

_Availability_: Linux, Windows, Mac.


## Floating-Point Comparison ##

Comparing floating-point numbers is tricky. Due to round-off errors, it is
very unlikely that two floating-points will match exactly. Therefore,
`ASSERT_EQ` 's naive comparison usually doesn't work. And since floating-points
can have a wide value range, no single fixed error bound works. It's better to
compare by a fixed relative error bound, except for values close to 0 due to
the loss of precision there.

In general, for floating-point comparison to make sense, the user needs to
carefully choose the error bound. If they don't want or care to, comparing in
terms of Units in the Last Place (ULPs) is a good default, and Google Test
provides assertions to do this. Full details about ULPs are quite long; if you
want to learn more, see
[this article on float comparison](https://randomascii.wordpress.com/2012/02/25/comparing-floating-point-numbers-2012-edition/).

### Floating-Point Macros ###

| **Fatal assertion** | **Nonfatal assertion** | **Verifies** |
|:--------------------|:-----------------------|:-------------|
| `ASSERT_FLOAT_EQ(`_val1, val2_`);`  | `EXPECT_FLOAT_EQ(`_val1, val2_`);` | the two `float` values are almost equal |
| `ASSERT_DOUBLE_EQ(`_val1, val2_`);` | `EXPECT_DOUBLE_EQ(`_val1, val2_`);` | the two `double` values are almost equal |

By "almost equal", we mean the two values are within 4 ULP's from each
other.

The following assertions allow you to choose the acceptable error bound:

| **Fatal assertion** | **Nonfatal assertion** | **Verifies** |
|:--------------------|:-----------------------|:-------------|
| `ASSERT_NEAR(`_val1, val2, abs\_error_`);` | `EXPECT_NEAR`_(val1, val2, abs\_error_`);` | the difference between _val1_ and _val2_ doesn't exceed the given absolute error |

_Availability_: Linux, Windows, Mac.

### Floating-Point Predicate-Format Functions ###

Some floating-point operations are useful, but not that often used. In order
to avoid an explosion of new macros, we provide them as predicate-format
functions that can be used in predicate assertion macros (e.g.
`EXPECT_PRED_FORMAT2`, etc).

```
EXPECT_PRED_FORMAT2(::testing::FloatLE, val1, val2);
EXPECT_PRED_FORMAT2(::testing::DoubleLE, val1, val2);
```

Verifies that _val1_ is less than, or almost equal to, _val2_. You can
replace `EXPECT_PRED_FORMAT2` in the above table with `ASSERT_PRED_FORMAT2`.

_Availability_: Linux, Windows, Mac.

## Windows HRESULT assertions ##

These assertions test for `HRESULT` success or failure.

| **Fatal assertion** | **Nonfatal assertion** | **Verifies** |
|:--------------------|:-----------------------|:-------------|
| `ASSERT_HRESULT_SUCCEEDED(`_expression_`);` | `EXPECT_HRESULT_SUCCEEDED(`_expression_`);` | _expression_ is a success `HRESULT` |
| `ASSERT_HRESULT_FAILED(`_expression_`);`    | `EXPECT_HRESULT_FAILED(`_expression_`);`    | _expression_ is a failure `HRESULT` |

The generated output contains the human-readable error message
associated with the `HRESULT` code returned by _expression_.

You might use them like this:

```
CComPtr shell;
ASSERT_HRESULT_SUCCEEDED(shell.CoCreateInstance(L"Shell.Application"));
CComVariant empty;
ASSERT_HRESULT_SUCCEEDED(shell->ShellExecute(CComBSTR(url), empty, empty, empty, empty));
```

_Availability_: Windows.

## Type Assertions ##

You can call the function
```
::testing::StaticAssertTypeEq<T1, T2>();
```
to assert that types `T1` and `T2` are the same.  The function does
nothing if the assertion is satisfied.  If the types are different,
the function call will fail to compile, and the compiler error message
will likely (depending on the compiler) show you the actual values of
`T1` and `T2`.  This is mainly useful inside template code.

_Caveat:_ When used inside a member function of a class template or a
function template, `StaticAssertTypeEq<T1, T2>()` is effective _only if_
the function is instantiated.  For example, given:
```
template <typename T> class Foo {
 public:
  void Bar() { ::testing::StaticAssertTypeEq<int, T>(); }
};
```
the code:
```
void Test1() { Foo<bool> foo; }
```
will _not_ generate a compiler error, as `Foo<bool>::Bar()` is never
actually instantiated.  Instead, you need:
```
void Test2() { Foo<bool> foo; foo.Bar(); }
```
to cause a compiler error.

_Availability:_ Linux, Windows, Mac; since version 1.3.0.

## Assertion Placement ##

You can use assertions in any C++ function. In particular, it doesn't
have to be a method of the test fixture class. The one constraint is
that assertions that generate a fatal failure (`FAIL*` and `ASSERT_*`)
can only be used in void-returning functions. This is a consequence of
Google Test not using exceptions. By placing it in a non-void function
you'll get a confusing compile error like
`"error: void value not ignored as it ought to be"`.

If you need to use assertions in a function that returns non-void, one option
is to make the function return the value in an out parameter instead. For
example, you can rewrite `T2 Foo(T1 x)` to `void Foo(T1 x, T2* result)`. You
need to make sure that `*result` contains some sensible value even when the
function returns prematurely. As the function now returns `void`, you can use
any assertion inside of it.

If changing the function's type is not an option, you should just use
assertions that generate non-fatal failures, such as `ADD_FAILURE*` and
`EXPECT_*`.

_Note_: Constructors and destructors are not considered void-returning
functions, according to the C++ language specification, and so you may not use
fatal assertions in them. You'll get a compilation error if you try. A simple
workaround is to transfer the entire body of the constructor or destructor to a
private void-returning method. However, you should be aware that a fatal
assertion failure in a constructor does not terminate the current test, as your
intuition might suggest; it merely returns from the constructor early, possibly
leaving your object in a partially-constructed state. Likewise, a fatal
assertion failure in a destructor may leave your object in a
partially-destructed state. Use assertions carefully in these situations!

# Teaching Google Test How to Print Your Values #

When a test assertion such as `EXPECT_EQ` fails, Google Test prints the
argument values to help you debug.  It does this using a
user-extensible value printer.

This printer knows how to print built-in C++ types, native arrays, STL
containers, and any type that supports the `<<` operator.  For other
types, it prints the raw bytes in the value and hopes that you the
user can figure it out.

As mentioned earlier, the printer is _extensible_.  That means
you can teach it to do a better job at printing your particular type
than to dump the bytes.  To do that, define `<<` for your type:

```
#include <iostream>

namespace foo {

class Bar { ... };  // We want Google Test to be able to print instances of this.

// It's important that the << operator is defined in the SAME
// namespace that defines Bar.  C++'s look-up rules rely on that.
::std::ostream& operator<<(::std::ostream& os, const Bar& bar) {
  return os << bar.DebugString();  // whatever needed to print bar to os
}

}  // namespace foo
```

Sometimes, this might not be an option: your team may consider it bad
style to have a `<<` operator for `Bar`, or `Bar` may already have a
`<<` operator that doesn't do what you want (and you cannot change
it).  If so, you can instead define a `PrintTo()` function like this:

```
#include <iostream>

namespace foo {

class Bar { ... };

// It's important that PrintTo() is defined in the SAME
// namespace that defines Bar.  C++'s look-up rules rely on that.
void PrintTo(const Bar& bar, ::std::ostream* os) {
  *os << bar.DebugString();  // whatever needed to print bar to os
}

}  // namespace foo
```

If you have defined both `<<` and `PrintTo()`, the latter will be used
when Google Test is concerned.  This allows you to customize how the value
appears in Google Test's output without affecting code that relies on the
behavior of its `<<` operator.

If you want to print a value `x` using Google Test's value printer
yourself, just call `::testing::PrintToString(`_x_`)`, which
returns an `std::string`:

```
vector<pair<Bar, int> > bar_ints = GetBarIntVector();

EXPECT_TRUE(IsCorrectBarIntVector(bar_ints))
    << "bar_ints = " << ::testing::PrintToString(bar_ints);
```

# Death Tests #

In many applications, there are assertions that can cause application failure
if a condition is not met. These sanity checks, which ensure that the program
is in a known good state, are there to fail at the earliest possible time after
some program state is corrupted. If the assertion checks the wrong condition,
then the program may proceed in an erroneous state, which could lead to memory
corruption, security holes, or worse. Hence it is vitally important to test
that such assertion statements work as expected.

Since these precondition checks cause the processes to die, we call such tests
_death tests_. More generally, any test that checks that a program terminates
(except by throwing an exception) in an expected fashion is also a death test.

Note that if a piece of code throws an exception, we don't consider it "death"
for the purpose of death tests, as the caller of the code could catch the exception
and avoid the crash. If you want to verify exceptions thrown by your code,
see [Exception Assertions](#exception-assertions).

If you want to test `EXPECT_*()/ASSERT_*()` failures in your test code, see [Catching Failures](#catching-failures).

## How to Write a Death Test ##

Google Test has the following macros to support death tests:

| **Fatal assertion** | **Nonfatal assertion** | **Verifies** |
|:--------------------|:-----------------------|:-------------|
| `ASSERT_DEATH(`_statement, regex_`);` | `EXPECT_DEATH(`_statement, regex_`);` | _statement_ crashes with the given error |
| `ASSERT_DEATH_IF_SUPPORTED(`_statement, regex_`);` | `EXPECT_DEATH_IF_SUPPORTED(`_statement, regex_`);` | if death tests are supported, verifies that _statement_ crashes with the given error; otherwise verifies nothing |
| `ASSERT_EXIT(`_statement, predicate, regex_`);` | `EXPECT_EXIT(`_statement, predicate, regex_`);` |_statement_ exits with the given error and its exit code matches _predicate_ |

where _statement_ is a statement that is expected to cause the process to
die, _predicate_ is a function or function object that evaluates an integer
exit status, and _regex_ is a regular expression that the stderr output of
_statement_ is expected to match. Note that _statement_ can be _any valid
statement_ (including _compound statement_) and doesn't have to be an
expression.

As usual, the `ASSERT` variants abort the current test function, while the
`EXPECT` variants do not.

**Note:** We use the word "crash" here to mean that the process
terminates with a _non-zero_ exit status code.  There are two
possibilities: either the process has called `exit()` or `_exit()`
with a non-zero value, or it may be killed by a signal.

This means that if _statement_ terminates the process with a 0 exit
code, it is _not_ considered a crash by `EXPECT_DEATH`.  Use
`EXPECT_EXIT` instead if this is the case, or if you want to restrict
the exit code more precisely.

A predicate here must accept an `int` and return a `bool`. The death test
succeeds only if the predicate returns `true`. Google Test defines a few
predicates that handle the most common cases:

```
::testing::ExitedWithCode(exit_code)
```

This expression is `true` if the program exited normally with the given exit
code.

```
::testing::KilledBySignal(signal_number)  // Not available on Windows.
```

This expression is `true` if the program was killed by the given signal.

The `*_DEATH` macros are convenient wrappers for `*_EXIT` that use a predicate
that verifies the process' exit code is non-zero.

Note that a death test only cares about three things:

  1. does _statement_ abort or exit the process?
  1. (in the case of `ASSERT_EXIT` and `EXPECT_EXIT`) does the exit status satisfy _predicate_?  Or (in the case of `ASSERT_DEATH` and `EXPECT_DEATH`) is the exit status non-zero?  And
  1. does the stderr output match _regex_?

In particular, if _statement_ generates an `ASSERT_*` or `EXPECT_*` failure, it will **not** cause the death test to fail, as Google Test assertions don't abort the process.

To write a death test, simply use one of the above macros inside your test
function. For example,

```
TEST(MyDeathTest, Foo) {
  // This death test uses a compound statement.
  ASSERT_DEATH({ int n = 5; Foo(&n); }, "Error on line .* of Foo()");
}
TEST(MyDeathTest, NormalExit) {
  EXPECT_EXIT(NormalExit(), ::testing::ExitedWithCode(0), "Success");
}
TEST(MyDeathTest, KillMyself) {
  EXPECT_EXIT(KillMyself(), ::testing::KilledBySignal(SIGKILL), "Sending myself unblockable signal");
}
```

verifies that:

  * calling `Foo(5)` causes the process to die with the given error message,
  * calling `NormalExit()` causes the process to print `"Success"` to stderr and exit with exit code 0, and
  * calling `KillMyself()` kills the process with signal `SIGKILL`.

The test function body may contain other assertions and statements as well, if
necessary.

_Important:_ We strongly recommend you to follow the convention of naming your
test case (not test) `*DeathTest` when it contains a death test, as
demonstrated in the above example. The `Death Tests And Threads` section below
explains why.

If a test fixture class is shared by normal tests and death tests, you
can use typedef to introduce an alias for the fixture class and avoid
duplicating its code:
```
class FooTest : public ::testing::Test { ... };

typedef FooTest FooDeathTest;

TEST_F(FooTest, DoesThis) {
  // normal test
}

TEST_F(FooDeathTest, DoesThat) {
  // death test
}
```

_Availability:_ Linux, Windows (requires MSVC 8.0 or above), Cygwin, and Mac (the latter three are supported since v1.3.0).  `(ASSERT|EXPECT)_DEATH_IF_SUPPORTED` are new in v1.4.0.

## Regular Expression Syntax ##

On POSIX systems (e.g. Linux, Cygwin, and Mac), Google Test uses the
[POSIX extended regular expression](http://www.opengroup.org/onlinepubs/009695399/basedefs/xbd_chap09.html#tag_09_04)
syntax in death tests. To learn about this syntax, you may want to read this [Wikipedia entry](http://en.wikipedia.org/wiki/Regular_expression#POSIX_Extended_Regular_Expressions).

On Windows, Google Test uses its own simple regular expression
implementation. It lacks many features you can find in POSIX extended
regular expressions.  For example, we don't support union (`"x|y"`),
grouping (`"(xy)"`), brackets (`"[xy]"`), and repetition count
(`"x{5,7}"`), among others. Below is what we do support (Letter `A` denotes a
literal character, period (`.`), or a single `\\` escape sequence; `x`
and `y` denote regular expressions.):

| `c` | matches any literal character `c` |
|:----|:----------------------------------|
| `\\d` | matches any decimal digit         |
| `\\D` | matches any character that's not a decimal digit |
| `\\f` | matches `\f`                      |
| `\\n` | matches `\n`                      |
| `\\r` | matches `\r`                      |
| `\\s` | matches any ASCII whitespace, including `\n` |
| `\\S` | matches any character that's not a whitespace |
| `\\t` | matches `\t`                      |
| `\\v` | matches `\v`                      |
| `\\w` | matches any letter, `_`, or decimal digit |
| `\\W` | matches any character that `\\w` doesn't match |
| `\\c` | matches any literal character `c`, which must be a punctuation |
| `\\.` | matches the `.` character         |
| `.` | matches any single character except `\n` |
| `A?` | matches 0 or 1 occurrences of `A` |
| `A*` | matches 0 or many occurrences of `A` |
| `A+` | matches 1 or many occurrences of `A` |
| `^` | matches the beginning of a string (not that of each line) |
| `$` | matches the end of a string (not that of each line) |
| `xy` | matches `x` followed by `y`       |

To help you determine which capability is available on your system,
Google Test defines macro `GTEST_USES_POSIX_RE=1` when it uses POSIX
extended regular expressions, or `GTEST_USES_SIMPLE_RE=1` when it uses
the simple version.  If you want your death tests to work in both
cases, you can either `#if` on these macros or use the more limited
syntax only.

## How It Works ##

Under the hood, `ASSERT_EXIT()` spawns a new process and executes the
death test statement in that process. The details of how precisely
that happens depend on the platform and the variable
`::testing::GTEST_FLAG(death_test_style)` (which is initialized from the
command-line flag `--gtest_death_test_style`).

  * On POSIX systems, `fork()` (or `clone()` on Linux) is used to spawn the child, after which:
    * If the variable's value is `"fast"`, the death test statement is immediately executed.
    * If the variable's value is `"threadsafe"`, the child process re-executes the unit test binary just as it was originally invoked, but with some extra flags to cause just the single death test under consideration to be run.
  * On Windows, the child is spawned using the `CreateProcess()` API, and re-executes the binary to cause just the single death test under consideration to be run - much like the `threadsafe` mode on POSIX.

Other values for the variable are illegal and will cause the death test to
fail. Currently, the flag's default value is `"fast"`. However, we reserve the
right to change it in the future. Therefore, your tests should not depend on
this.

In either case, the parent process waits for the child process to complete, and checks that

  1. the child's exit status satisfies the predicate, and
  1. the child's stderr matches the regular expression.

If the death test statement runs to completion without dying, the child
process will nonetheless terminate, and the assertion fails.

## Death Tests And Threads ##

The reason for the two death test styles has to do with thread safety. Due to
well-known problems with forking in the presence of threads, death tests should
be run in a single-threaded context. Sometimes, however, it isn't feasible to
arrange that kind of environment. For example, statically-initialized modules
may start threads before main is ever reached. Once threads have been created,
it may be difficult or impossible to clean them up.

Google Test has three features intended to raise awareness of threading issues.

  1. A warning is emitted if multiple threads are running when a death test is encountered.
  1. Test cases with a name ending in "DeathTest" are run before all other tests.
  1. It uses `clone()` instead of `fork()` to spawn the child process on Linux (`clone()` is not available on Cygwin and Mac), as `fork()` is more likely to cause the child to hang when the parent process has multiple threads.

It's perfectly fine to create threads inside a death test statement; they are
executed in a separate process and cannot affect the parent.

## Death Test Styles ##

The "threadsafe" death test style was introduced in order to help mitigate the
risks of testing in a possibly multithreaded environment. It trades increased
test execution time (potentially dramatically so) for improved thread safety.
We suggest using the faster, default "fast" style unless your test has specific
problems with it.

You can choose a particular style of death tests by setting the flag
programmatically:

```
::testing::FLAGS_gtest_death_test_style = "threadsafe";
```

You can do this in `main()` to set the style for all death tests in the
binary, or in individual tests. Recall that flags are saved before running each
test and restored afterwards, so you need not do that yourself. For example:

```
TEST(MyDeathTest, TestOne) {
  ::testing::FLAGS_gtest_death_test_style = "threadsafe";
  // This test is run in the "threadsafe" style:
  ASSERT_DEATH(ThisShouldDie(), "");
}

TEST(MyDeathTest, TestTwo) {
  // This test is run in the "fast" style:
  ASSERT_DEATH(ThisShouldDie(), "");
}

int main(int argc, char** argv) {
  ::testing::InitGoogleTest(&argc, argv);
  ::testing::FLAGS_gtest_death_test_style = "fast";
  return RUN_ALL_TESTS();
}
```

## Caveats ##

The _statement_ argument of `ASSERT_EXIT()` can be any valid C++ statement.
If it leaves the current function via a `return` statement or by throwing an exception,
the death test is considered to have failed.  Some Google Test macros may return
from the current function (e.g. `ASSERT_TRUE()`), so be sure to avoid them in _statement_.

Since _statement_ runs in the child process, any in-memory side effect (e.g.
modifying a variable, releasing memory, etc) it causes will _not_ be observable
in the parent process. In particular, if you release memory in a death test,
your program will fail the heap check as the parent process will never see the
memory reclaimed. To solve this problem, you can

  1. try not to free memory in a death test;
  1. free the memory again in the parent process; or
  1. do not use the heap checker in your program.

Due to an implementation detail, you cannot place multiple death test
assertions on the same line; otherwise, compilation will fail with an unobvious
error message.

Despite the improved thread safety afforded by the "threadsafe" style of death
test, thread problems such as deadlock are still possible in the presence of
handlers registered with `pthread_atfork(3)`.

# Using Assertions in Sub-routines #

## Adding Traces to Assertions ##

If a test sub-routine is called from several places, when an assertion
inside it fails, it can be hard to tell which invocation of the
sub-routine the failure is from.  You can alleviate this problem using
extra logging or custom failure messages, but that usually clutters up
your tests. A better solution is to use the `SCOPED_TRACE` macro:

| `SCOPED_TRACE(`_message_`);` |
|:-----------------------------|

where _message_ can be anything streamable to `std::ostream`. This
macro will cause the current file name, line number, and the given
message to be added in every failure message. The effect will be
undone when the control leaves the current lexical scope.

For example,

```
10: void Sub1(int n) {
11:   EXPECT_EQ(1, Bar(n));
12:   EXPECT_EQ(2, Bar(n + 1));
13: }
14:
15: TEST(FooTest, Bar) {
16:   {
17:     SCOPED_TRACE("A");  // This trace point will be included in
18:                         // every failure in this scope.
19:     Sub1(1);
20:   }
21:   // Now it won't.
22:   Sub1(9);
23: }
```

could result in messages like these:

```
path/to/foo_test.cc:11: Failure
Value of: Bar(n)
Expected: 1
  Actual: 2
   Trace:
path/to/foo_test.cc:17: A

path/to/foo_test.cc:12: Failure
Value of: Bar(n + 1)
Expected: 2
  Actual: 3
```

Without the trace, it would've been difficult to know which invocation
of `Sub1()` the two failures come from respectively. (You could add an
extra message to each assertion in `Sub1()` to indicate the value of
`n`, but that's tedious.)

Some tips on using `SCOPED_TRACE`:

  1. With a suitable message, it's often enough to use `SCOPED_TRACE` at the beginning of a sub-routine, instead of at each call site.
  1. When calling sub-routines inside a loop, make the loop iterator part of the message in `SCOPED_TRACE` such that you can know which iteration the failure is from.
  1. Sometimes the line number of the trace point is enough for identifying the particular invocation of a sub-routine. In this case, you don't have to choose a unique message for `SCOPED_TRACE`. You can simply use `""`.
  1. You can use `SCOPED_TRACE` in an inner scope when there is one in the outer scope. In this case, all active trace points will be included in the failure messages, in reverse order they are encountered.
  1. The trace dump is clickable in Emacs' compilation buffer - hit return on a line number and you'll be taken to that line in the source file!

_Availability:_ Linux, Windows, Mac.

## Propagating Fatal Failures ##

A common pitfall when using `ASSERT_*` and `FAIL*` is not understanding that
when they fail they only abort the _current function_, not the entire test. For
example, the following test will segfault:
```
void Subroutine() {
  // Generates a fatal failure and aborts the current function.
  ASSERT_EQ(1, 2);
  // The following won't be executed.
  ...
}

TEST(FooTest, Bar) {
  Subroutine();
  // The intended behavior is for the fatal failure
  // in Subroutine() to abort the entire test.
  // The actual behavior: the function goes on after Subroutine() returns.
  int* p = NULL;
  *p = 3; // Segfault!
}
```

Since we don't use exceptions, it is technically impossible to
implement the intended behavior here.  To alleviate this, Google Test
provides two solutions.  You could use either the
`(ASSERT|EXPECT)_NO_FATAL_FAILURE` assertions or the
`HasFatalFailure()` function.  They are described in the following two
subsections.

### Asserting on Subroutines ###

As shown above, if your test calls a subroutine that has an `ASSERT_*`
failure in it, the test will continue after the subroutine
returns. This may not be what you want.

Often people want fatal failures to propagate like exceptions.  For
that Google Test offers the following macros:

| **Fatal assertion** | **Nonfatal assertion** | **Verifies** |
|:--------------------|:-----------------------|:-------------|
| `ASSERT_NO_FATAL_FAILURE(`_statement_`);` | `EXPECT_NO_FATAL_FAILURE(`_statement_`);` | _statement_ doesn't generate any new fatal failures in the current thread. |

Only failures in the thread that executes the assertion are checked to
determine the result of this type of assertions.  If _statement_
creates new threads, failures in these threads are ignored.

Examples:

```
ASSERT_NO_FATAL_FAILURE(Foo());

int i;
EXPECT_NO_FATAL_FAILURE({
  i = Bar();
});
```

_Availability:_ Linux, Windows, Mac. Assertions from multiple threads
are currently not supported.

### Checking for Failures in the Current Test ###

`HasFatalFailure()` in the `::testing::Test` class returns `true` if an
assertion in the current test has suffered a fatal failure. This
allows functions to catch fatal failures in a sub-routine and return
early.

```
class Test {
 public:
  ...
  static bool HasFatalFailure();
};
```

The typical usage, which basically simulates the behavior of a thrown
exception, is:

```
TEST(FooTest, Bar) {
  Subroutine();
  // Aborts if Subroutine() had a fatal failure.
  if (HasFatalFailure())
    return;
  // The following won't be executed.
  ...
}
```

If `HasFatalFailure()` is used outside of `TEST()` , `TEST_F()` , or a test
fixture, you must add the `::testing::Test::` prefix, as in:

```
if (::testing::Test::HasFatalFailure())
  return;
```

Similarly, `HasNonfatalFailure()` returns `true` if the current test
has at least one non-fatal failure, and `HasFailure()` returns `true`
if the current test has at least one failure of either kind.

_Availability:_ Linux, Windows, Mac.  `HasNonfatalFailure()` and
`HasFailure()` are available since version 1.4.0.

# Logging Additional Information #

In your test code, you can call `RecordProperty("key", value)` to log
additional information, where `value` can be either a string or an `int`. The _last_ value recorded for a key will be emitted to the XML output
if you specify one. For example, the test

```
TEST_F(WidgetUsageTest, MinAndMaxWidgets) {
  RecordProperty("MaximumWidgets", ComputeMaxUsage());
  RecordProperty("MinimumWidgets", ComputeMinUsage());
}
```

will output XML like this:

```
...
  <testcase name="MinAndMaxWidgets" status="run" time="6" classname="WidgetUsageTest"
            MaximumWidgets="12"
            MinimumWidgets="9" />
...
```

_Note_:
  * `RecordProperty()` is a static member of the `Test` class. Therefore it needs to be prefixed with `::testing::Test::` if used outside of the `TEST` body and the test fixture class.
  * `key` must be a valid XML attribute name, and cannot conflict with the ones already used by Google Test (`name`, `status`, `time`, `classname`, `type_param`, and `value_param`).
  * Calling `RecordProperty()` outside of the lifespan of a test is allowed. If it's called outside of a test but between a test case's `SetUpTestCase()` and `TearDownTestCase()` methods, it will be attributed to the XML element for the test case. If it's called outside of all test cases (e.g. in a test environment), it will be attributed to the top-level XML element.

_Availability_: Linux, Windows, Mac.

# Sharing Resources Between Tests in the Same Test Case #



Google Test creates a new test fixture object for each test in order to make
tests independent and easier to debug. However, sometimes tests use resources
that are expensive to set up, making the one-copy-per-test model prohibitively
expensive.

If the tests don't change the resource, there's no harm in them sharing a
single resource copy. So, in addition to per-test set-up/tear-down, Google Test
also supports per-test-case set-up/tear-down. To use it:

  1. In your test fixture class (say `FooTest` ), define as `static` some member variables to hold the shared resources.
  1. In the same test fixture class, define a `static void SetUpTestCase()` function (remember not to spell it as **`SetupTestCase`** with a small `u`!) to set up the shared resources and a `static void TearDownTestCase()` function to tear them down.

That's it! Google Test automatically calls `SetUpTestCase()` before running the
_first test_ in the `FooTest` test case (i.e. before creating the first
`FooTest` object), and calls `TearDownTestCase()` after running the _last test_
in it (i.e. after deleting the last `FooTest` object). In between, the tests
can use the shared resources.

Remember that the test order is undefined, so your code can't depend on a test
preceding or following another. Also, the tests must either not modify the
state of any shared resource, or, if they do modify the state, they must
restore the state to its original value before passing control to the next
test.

Here's an example of per-test-case set-up and tear-down:
```
class FooTest : public ::testing::Test {
 protected:
  // Per-test-case set-up.
  // Called before the first test in this test case.
  // Can be omitted if not needed.
  static void SetUpTestCase() {
    shared_resource_ = new ...;
  }

  // Per-test-case tear-down.
  // Called after the last test in this test case.
  // Can be omitted if not needed.
  static void TearDownTestCase() {
    delete shared_resource_;
    shared_resource_ = NULL;
  }

  // You can define per-test set-up and tear-down logic as usual.
  virtual void SetUp() { ... }
  virtual void TearDown() { ... }

  // Some expensive resource shared by all tests.
  static T* shared_resource_;
};

T* FooTest::shared_resource_ = NULL;

TEST_F(FooTest, Test1) {
  ... you can refer to shared_resource here ...
}
TEST_F(FooTest, Test2) {
  ... you can refer to shared_resource here ...
}
```

_Availability:_ Linux, Windows, Mac.

# Global Set-Up and Tear-Down #

Just as you can do set-up and tear-down at the test level and the test case
level, you can also do it at the test program level. Here's how.

First, you subclass the `::testing::Environment` class to define a test
environment, which knows how to set-up and tear-down:

```
class Environment {
 public:
  virtual ~Environment() {}
  // Override this to define how to set up the environment.
  virtual void SetUp() {}
  // Override this to define how to tear down the environment.
  virtual void TearDown() {}
};
```

Then, you register an instance of your environment class with Google Test by
calling the `::testing::AddGlobalTestEnvironment()` function:

```
Environment* AddGlobalTestEnvironment(Environment* env);
```

Now, when `RUN_ALL_TESTS()` is called, it first calls the `SetUp()` method of
the environment object, then runs the tests if there was no fatal failures, and
finally calls `TearDown()` of the environment object.

It's OK to register multiple environment objects. In this case, their `SetUp()`
will be called in the order they are registered, and their `TearDown()` will be
called in the reverse order.

Note that Google Test takes ownership of the registered environment objects.
Therefore **do not delete them** by yourself.

You should call `AddGlobalTestEnvironment()` before `RUN_ALL_TESTS()` is
called, probably in `main()`. If you use `gtest_main`, you need to      call
this before `main()` starts for it to take effect. One way to do this is to
define a global variable like this:

```
::testing::Environment* const foo_env = ::testing::AddGlobalTestEnvironment(new FooEnvironment);
```

However, we strongly recommend you to write your own `main()` and call
`AddGlobalTestEnvironment()` there, as relying on initialization of global
variables makes the code harder to read and may cause problems when you
register multiple environments from different translation units and the
environments have dependencies among them (remember that the compiler doesn't
guarantee the order in which global variables from different translation units
are initialized).

_Availability:_ Linux, Windows, Mac.


# Value Parameterized Tests #

_Value-parameterized tests_ allow you to test your code with different
parameters without writing multiple copies of the same test.

Suppose you write a test for your code and then realize that your code is affected by a presence of a Boolean command line flag.

```
TEST(MyCodeTest, TestFoo) {
  // A code to test foo().
}
```

Usually people factor their test code into a function with a Boolean parameter in such situations. The function sets the flag, then executes the testing code.

```
void TestFooHelper(bool flag_value) {
  flag = flag_value;
  // A code to test foo().
}

TEST(MyCodeTest, TestFoo) {
  TestFooHelper(false);
  TestFooHelper(true);
}
```

But this setup has serious drawbacks. First, when a test assertion fails in your tests, it becomes unclear what value of the parameter caused it to fail. You can stream a clarifying message into your `EXPECT`/`ASSERT` statements, but it you'll have to do it with all of them. Second, you have to add one such helper function per test. What if you have ten tests? Twenty? A hundred?

Value-parameterized tests will let you write your test only once and then easily instantiate and run it with an arbitrary number of parameter values.

Here are some other situations when value-parameterized tests come handy:

  * You want to test different implementations of an OO interface.
  * You want to test your code over various inputs (a.k.a. data-driven testing). This feature is easy to abuse, so please exercise your good sense when doing it!

## How to Write Value-Parameterized Tests ##

To write value-parameterized tests, first you should define a fixture
class.  It must be derived from both `::testing::Test` and
`::testing::WithParamInterface<T>` (the latter is a pure interface),
where `T` is the type of your parameter values.  For convenience, you
can just derive the fixture class from `::testing::TestWithParam<T>`,
which itself is derived from both `::testing::Test` and
`::testing::WithParamInterface<T>`. `T` can be any copyable type. If
it's a raw pointer, you are responsible for managing the lifespan of
the pointed values.

```
class FooTest : public ::testing::TestWithParam<const char*> {
  // You can implement all the usual fixture class members here.
  // To access the test parameter, call GetParam() from class
  // TestWithParam<T>.
};

// Or, when you want to add parameters to a pre-existing fixture class:
class BaseTest : public ::testing::Test {
  ...
};
class BarTest : public BaseTest,
                public ::testing::WithParamInterface<const char*> {
  ...
};
```

Then, use the `TEST_P` macro to define as many test patterns using
this fixture as you want.  The `_P` suffix is for "parameterized" or
"pattern", whichever you prefer to think.

```
TEST_P(FooTest, DoesBlah) {
  // Inside a test, access the test parameter with the GetParam() method
  // of the TestWithParam<T> class:
  EXPECT_TRUE(foo.Blah(GetParam()));
  ...
}

TEST_P(FooTest, HasBlahBlah) {
  ...
}
```

Finally, you can use `INSTANTIATE_TEST_CASE_P` to instantiate the test
case with any set of parameters you want. Google Test defines a number of
functions for generating test parameters. They return what we call
(surprise!) _parameter generators_. Here is a summary of them,
which are all in the `testing` namespace:

| `Range(begin, end[, step])` | Yields values `{begin, begin+step, begin+step+step, ...}`. The values do not include `end`. `step` defaults to 1. |
|:----------------------------|:------------------------------------------------------------------------------------------------------------------|
| `Values(v1, v2, ..., vN)`   | Yields values `{v1, v2, ..., vN}`.                                                                                |
| `ValuesIn(container)` and `ValuesIn(begin, end)` | Yields values from a C-style array, an STL-style container, or an iterator range `[begin, end)`. `container`, `begin`, and `end` can be expressions whose values are determined at run time.  |
| `Bool()`                    | Yields sequence `{false, true}`.                                                                                  |
| `Combine(g1, g2, ..., gN)`  | Yields all combinations (the Cartesian product for the math savvy) of the values generated by the `N` generators. This is only available if your system provides the `<tr1/tuple>` header. If you are sure your system does, and Google Test disagrees, you can override it by defining `GTEST_HAS_TR1_TUPLE=1`. See comments in [include/gtest/internal/gtest-port.h](../include/gtest/internal/gtest-port.h) for more information. |

For more details, see the comments at the definitions of these functions in the [source code](../include/gtest/gtest-param-test.h).

The following statement will instantiate tests from the `FooTest` test case
each with parameter values `"meeny"`, `"miny"`, and `"moe"`.

```
INSTANTIATE_TEST_CASE_P(InstantiationName,
                        FooTest,
                        ::testing::Values("meeny", "miny", "moe"));
```

To distinguish different instances of the pattern (yes, you can
instantiate it more than once), the first argument to
`INSTANTIATE_TEST_CASE_P` is a prefix that will be added to the actual
test case name. Remember to pick unique prefixes for different
instantiations. The tests from the instantiation above will have these
names:

  * `InstantiationName/FooTest.DoesBlah/0` for `"meeny"`
  * `InstantiationName/FooTest.DoesBlah/1` for `"miny"`
  * `InstantiationName/FooTest.DoesBlah/2` for `"moe"`
  * `InstantiationName/FooTest.HasBlahBlah/0` for `"meeny"`
  * `InstantiationName/FooTest.HasBlahBlah/1` for `"miny"`
  * `InstantiationName/FooTest.HasBlahBlah/2` for `"moe"`

You can use these names in [--gtest\_filter](#running-a-subset-of-the-tests).

This statement will instantiate all tests from `FooTest` again, each
with parameter values `"cat"` and `"dog"`:

```
const char* pets[] = {"cat", "dog"};
INSTANTIATE_TEST_CASE_P(AnotherInstantiationName, FooTest,
                        ::testing::ValuesIn(pets));
```

The tests from the instantiation above will have these names:

  * `AnotherInstantiationName/FooTest.DoesBlah/0` for `"cat"`
  * `AnotherInstantiationName/FooTest.DoesBlah/1` for `"dog"`
  * `AnotherInstantiationName/FooTest.HasBlahBlah/0` for `"cat"`
  * `AnotherInstantiationName/FooTest.HasBlahBlah/1` for `"dog"`

Please note that `INSTANTIATE_TEST_CASE_P` will instantiate _all_
tests in the given test case, whether their definitions come before or
_after_ the `INSTANTIATE_TEST_CASE_P` statement.

You can see
[these](../samples/sample7_unittest.cc)
[files](../samples/sample8_unittest.cc) for more examples.

_Availability_: Linux, Windows (requires MSVC 8.0 or above), Mac; since version 1.2.0.

## Creating Value-Parameterized Abstract Tests ##

In the above, we define and instantiate `FooTest` in the same source
file. Sometimes you may want to define value-parameterized tests in a
library and let other people instantiate them later. This pattern is
known as <i>abstract tests</i>. As an example of its application, when you
are designing an interface you can write a standard suite of abstract
tests (perhaps using a factory function as the test parameter) that
all implementations of the interface are expected to pass. When
someone implements the interface, they can instantiate your suite to get
all the interface-conformance tests for free.

To define abstract tests, you should organize your code like this:

  1. Put the definition of the parameterized test fixture class (e.g. `FooTest`) in a header file, say `foo_param_test.h`. Think of this as _declaring_ your abstract tests.
  1. Put the `TEST_P` definitions in `foo_param_test.cc`, which includes `foo_param_test.h`. Think of this as _implementing_ your abstract tests.

Once they are defined, you can instantiate them by including
`foo_param_test.h`, invoking `INSTANTIATE_TEST_CASE_P()`, and linking
with `foo_param_test.cc`. You can instantiate the same abstract test
case multiple times, possibly in different source files.

# Typed Tests #

Suppose you have multiple implementations of the same interface and
want to make sure that all of them satisfy some common requirements.
Or, you may have defined several types that are supposed to conform to
the same "concept" and you want to verify it.  In both cases, you want
the same test logic repeated for different types.

While you can write one `TEST` or `TEST_F` for each type you want to
test (and you may even factor the test logic into a function template
that you invoke from the `TEST`), it's tedious and doesn't scale:
if you want _m_ tests over _n_ types, you'll end up writing _m\*n_
`TEST`s.

_Typed tests_ allow you to repeat the same test logic over a list of
types.  You only need to write the test logic once, although you must
know the type list when writing typed tests.  Here's how you do it:

First, define a fixture class template.  It should be parameterized
by a type.  Remember to derive it from `::testing::Test`:

```
template <typename T>
class FooTest : public ::testing::Test {
 public:
  ...
  typedef std::list<T> List;
  static T shared_;
  T value_;
};
```

Next, associate a list of types with the test case, which will be
repeated for each type in the list:

```
typedef ::testing::Types<char, int, unsigned int> MyTypes;
TYPED_TEST_CASE(FooTest, MyTypes);
```

The `typedef` is necessary for the `TYPED_TEST_CASE` macro to parse
correctly.  Otherwise the compiler will think that each comma in the
type list introduces a new macro argument.

Then, use `TYPED_TEST()` instead of `TEST_F()` to define a typed test
for this test case.  You can repeat this as many times as you want:

```
TYPED_TEST(FooTest, DoesBlah) {
  // Inside a test, refer to the special name TypeParam to get the type
  // parameter.  Since we are inside a derived class template, C++ requires
  // us to visit the members of FooTest via 'this'.
  TypeParam n = this->value_;

  // To visit static members of the fixture, add the 'TestFixture::'
  // prefix.
  n += TestFixture::shared_;

  // To refer to typedefs in the fixture, add the 'typename TestFixture::'
  // prefix.  The 'typename' is required to satisfy the compiler.
  typename TestFixture::List values;
  values.push_back(n);
  ...
}

TYPED_TEST(FooTest, HasPropertyA) { ... }
```

You can see [`samples/sample6_unittest.cc`](../samples/sample6_unittest.cc) for a complete example.

_Availability:_ Linux, Windows (requires MSVC 8.0 or above), Mac;
since version 1.1.0.

# Type-Parameterized Tests #

_Type-parameterized tests_ are like typed tests, except that they
don't require you to know the list of types ahead of time.  Instead,
you can define the test logic first and instantiate it with different
type lists later.  You can even instantiate it more than once in the
same program.

If you are designing an interface or concept, you can define a suite
of type-parameterized tests to verify properties that any valid
implementation of the interface/concept should have.  Then, the author
of each implementation can just instantiate the test suite with his
type to verify that it conforms to the requirements, without having to
write similar tests repeatedly.  Here's an example:

First, define a fixture class template, as we did with typed tests:

```
template <typename T>
class FooTest : public ::testing::Test {
  ...
};
```

Next, declare that you will define a type-parameterized test case:

```
TYPED_TEST_CASE_P(FooTest);
```

The `_P` suffix is for "parameterized" or "pattern", whichever you
prefer to think.

Then, use `TYPED_TEST_P()` to define a type-parameterized test.  You
can repeat this as many times as you want:

```
TYPED_TEST_P(FooTest, DoesBlah) {
  // Inside a test, refer to TypeParam to get the type parameter.
  TypeParam n = 0;
  ...
}

TYPED_TEST_P(FooTest, HasPropertyA) { ... }
```

Now the tricky part: you need to register all test patterns using the
`REGISTER_TYPED_TEST_CASE_P` macro before you can instantiate them.
The first argument of the macro is the test case name; the rest are
the names of the tests in this test case:

```
REGISTER_TYPED_TEST_CASE_P(FooTest,
                           DoesBlah, HasPropertyA);
```

Finally, you are free to instantiate the pattern with the types you
want.  If you put the above code in a header file, you can `#include`
it in multiple C++ source files and instantiate it multiple times.

```
typedef ::testing::Types<char, int, unsigned int> MyTypes;
INSTANTIATE_TYPED_TEST_CASE_P(My, FooTest, MyTypes);
```

To distinguish different instances of the pattern, the first argument
to the `INSTANTIATE_TYPED_TEST_CASE_P` macro is a prefix that will be
added to the actual test case name.  Remember to pick unique prefixes
for different instances.

In the special case where the type list contains only one type, you
can write that type directly without `::testing::Types<...>`, like this:

```
INSTANTIATE_TYPED_TEST_CASE_P(My, FooTest, int);
```

You can see `samples/sample6_unittest.cc` for a complete example.

_Availability:_ Linux, Windows (requires MSVC 8.0 or above), Mac;
since version 1.1.0.

# Testing Private Code #

If you change your software's internal implementation, your tests should not
break as long as the change is not observable by users. Therefore, per the
_black-box testing principle_, most of the time you should test your code
through its public interfaces.

If you still find yourself needing to test internal implementation code,
consider if there's a better design that wouldn't require you to do so. If you
absolutely have to test non-public interface code though, you can. There are
two cases to consider:

  * Static functions (_not_ the same as static member functions!) or unnamed namespaces, and
  * Private or protected class members.

## Static Functions ##

Both static functions and definitions/declarations in an unnamed namespace are
only visible within the same translation unit. To test them, you can `#include`
the entire `.cc` file being tested in your `*_test.cc` file. (`#include`ing `.cc`
files is not a good way to reuse code - you should not do this in production
code!)

However, a better approach is to move the private code into the
`foo::internal` namespace, where `foo` is the namespace your project normally
uses, and put the private declarations in a `*-internal.h` file. Your
production `.cc` files and your tests are allowed to include this internal
header, but your clients are not. This way, you can fully test your internal
implementation without leaking it to your clients.

## Private Class Members ##

Private class members are only accessible from within the class or by friends.
To access a class' private members, you can declare your test fixture as a
friend to the class and define accessors in your fixture. Tests using the
fixture can then access the private members of your production class via the
accessors in the fixture. Note that even though your fixture is a friend to
your production class, your tests are not automatically friends to it, as they
are technically defined in sub-classes of the fixture.

Another way to test private members is to refactor them into an implementation
class, which is then declared in a `*-internal.h` file. Your clients aren't
allowed to include this header but your tests can. Such is called the Pimpl
(Private Implementation) idiom.

Or, you can declare an individual test as a friend of your class by adding this
line in the class body:

```
FRIEND_TEST(TestCaseName, TestName);
```

For example,
```
// foo.h
#include "gtest/gtest_prod.h"

// Defines FRIEND_TEST.
class Foo {
  ...
 private:
  FRIEND_TEST(FooTest, BarReturnsZeroOnNull);
  int Bar(void* x);
};

// foo_test.cc
...
TEST(FooTest, BarReturnsZeroOnNull) {
  Foo foo;
  EXPECT_EQ(0, foo.Bar(NULL));
  // Uses Foo's private member Bar().
}
```

Pay special attention when your class is defined in a namespace, as you should
define your test fixtures and tests in the same namespace if you want them to
be friends of your class. For example, if the code to be tested looks like:

```
namespace my_namespace {

class Foo {
  friend class FooTest;
  FRIEND_TEST(FooTest, Bar);
  FRIEND_TEST(FooTest, Baz);
  ...
  definition of the class Foo
  ...
};

}  // namespace my_namespace
```

Your test code should be something like:

```
namespace my_namespace {
class FooTest : public ::testing::Test {
 protected:
  ...
};

TEST_F(FooTest, Bar) { ... }
TEST_F(FooTest, Baz) { ... }

}  // namespace my_namespace
```

# Catching Failures #

If you are building a testing utility on top of Google Test, you'll
want to test your utility.  What framework would you use to test it?
Google Test, of course.

The challenge is to verify that your testing utility reports failures
correctly.  In frameworks that report a failure by throwing an
exception, you could catch the exception and assert on it.  But Google
Test doesn't use exceptions, so how do we test that a piece of code
generates an expected failure?

`"gtest/gtest-spi.h"` contains some constructs to do this.  After
`#include`ing this header, you can use

| `EXPECT_FATAL_FAILURE(`_statement, substring_`);` |
|:--------------------------------------------------|

to assert that _statement_ generates a fatal (e.g. `ASSERT_*`) failure
whose message contains the given _substring_, or use

| `EXPECT_NONFATAL_FAILURE(`_statement, substring_`);` |
|:-----------------------------------------------------|

if you are expecting a non-fatal (e.g. `EXPECT_*`) failure.

For technical reasons, there are some caveats:

  1. You cannot stream a failure message to either macro.
  1. _statement_ in `EXPECT_FATAL_FAILURE()` cannot reference local non-static variables or non-static members of `this` object.
  1. _statement_ in `EXPECT_FATAL_FAILURE()` cannot return a value.

_Note:_ Google Test is designed with threads in mind. Once the
synchronization primitives in `"gtest/internal/gtest-port.h"` have
been implemented, Google Test will become thread-safe, meaning that
you can then use assertions in multiple threads concurrently. Before
that, however, Google Test only supports single-threaded usage. Once
thread-safe, `EXPECT_FATAL_FAILURE()` and `EXPECT_NONFATAL_FAILURE()`
will capture failures in the current thread only. If _statement_
creates new threads, failures in these threads will be ignored. If
you want to capture failures from all threads instead, you should use
the following macros:

| `EXPECT_FATAL_FAILURE_ON_ALL_THREADS(`_statement, substring_`);` |
|:-----------------------------------------------------------------|
| `EXPECT_NONFATAL_FAILURE_ON_ALL_THREADS(`_statement, substring_`);` |

# Getting the Current Test's Name #

Sometimes a function may need to know the name of the currently running test.
For example, you may be using the `SetUp()` method of your test fixture to set
the golden file name based on which test is running. The `::testing::TestInfo`
class has this information:

```
namespace testing {

class TestInfo {
 public:
  // Returns the test case name and the test name, respectively.
  //
  // Do NOT delete or free the return value - it's managed by the
  // TestInfo class.
  const char* test_case_name() const;
  const char* name() const;
};

}  // namespace testing
```


> To obtain a `TestInfo` object for the currently running test, call
`current_test_info()` on the `UnitTest` singleton object:

```
// Gets information about the currently running test.
// Do NOT delete the returned object - it's managed by the UnitTest class.
const ::testing::TestInfo* const test_info =
  ::testing::UnitTest::GetInstance()->current_test_info();
printf("We are in test %s of test case %s.\n",
       test_info->name(), test_info->test_case_name());
```

`current_test_info()` returns a null pointer if no test is running. In
particular, you cannot find the test case name in `SetUpTestCase()`,
`TearDownTestCase()` (where you know the test case name implicitly), or
functions called from them.

_Availability:_ Linux, Windows, Mac.

# Extending Google Test by Handling Test Events #

Google Test provides an <b>event listener API</b> to let you receive
notifications about the progress of a test program and test
failures. The events you can listen to include the start and end of
the test program, a test case, or a test method, among others. You may
use this API to augment or replace the standard console output,
replace the XML output, or provide a completely different form of
output, such as a GUI or a database. You can also use test events as
checkpoints to implement a resource leak checker, for example.

_Availability:_ Linux, Windows, Mac; since v1.4.0.

## Defining Event Listeners ##

To define a event listener, you subclass either
[testing::TestEventListener](../include/gtest/gtest.h#L991)
or [testing::EmptyTestEventListener](../include/gtest/gtest.h#L1044).
The former is an (abstract) interface, where <i>each pure virtual method<br>
can be overridden to handle a test event</i> (For example, when a test
starts, the `OnTestStart()` method will be called.). The latter provides
an empty implementation of all methods in the interface, such that a
subclass only needs to override the methods it cares about.

When an event is fired, its context is passed to the handler function
as an argument. The following argument types are used:
  * [UnitTest](../include/gtest/gtest.h#L1151) reflects the state of the entire test program,
  * [TestCase](../include/gtest/gtest.h#L778) has information about a test case, which can contain one or more tests,
  * [TestInfo](../include/gtest/gtest.h#L644) contains the state of a test, and
  * [TestPartResult](../include/gtest/gtest-test-part.h#L47) represents the result of a test assertion.

An event handler function can examine the argument it receives to find
out interesting information about the event and the test program's
state.  Here's an example:

```
  class MinimalistPrinter : public ::testing::EmptyTestEventListener {
    // Called before a test starts.
    virtual void OnTestStart(const ::testing::TestInfo& test_info) {
      printf("*** Test %s.%s starting.\n",
             test_info.test_case_name(), test_info.name());
    }

    // Called after a failed assertion or a SUCCEED() invocation.
    virtual void OnTestPartResult(
        const ::testing::TestPartResult& test_part_result) {
      printf("%s in %s:%d\n%s\n",
             test_part_result.failed() ? "*** Failure" : "Success",
             test_part_result.file_name(),
             test_part_result.line_number(),
             test_part_result.summary());
    }

    // Called after a test ends.
    virtual void OnTestEnd(const ::testing::TestInfo& test_info) {
      printf("*** Test %s.%s ending.\n",
             test_info.test_case_name(), test_info.name());
    }
  };
```

## Using Event Listeners ##

To use the event listener you have defined, add an instance of it to
the Google Test event listener list (represented by class
[TestEventListeners](../include/gtest/gtest.h#L1064)
- note the "s" at the end of the name) in your
`main()` function, before calling `RUN_ALL_TESTS()`:
```
int main(int argc, char** argv) {
  ::testing::InitGoogleTest(&argc, argv);
  // Gets hold of the event listener list.
  ::testing::TestEventListeners& listeners =
      ::testing::UnitTest::GetInstance()->listeners();
  // Adds a listener to the end.  Google Test takes the ownership.
  listeners.Append(new MinimalistPrinter);
  return RUN_ALL_TESTS();
}
```

There's only one problem: the default test result printer is still in
effect, so its output will mingle with the output from your minimalist
printer. To suppress the default printer, just release it from the
event listener list and delete it. You can do so by adding one line:
```
  ...
  delete listeners.Release(listeners.default_result_printer());
  listeners.Append(new MinimalistPrinter);
  return RUN_ALL_TESTS();
```

Now, sit back and enjoy a completely different output from your
tests. For more details, you can read this
[sample](../samples/sample9_unittest.cc).

You may append more than one listener to the list. When an `On*Start()`
or `OnTestPartResult()` event is fired, the listeners will receive it in
the order they appear in the list (since new listeners are added to
the end of the list, the default text printer and the default XML
generator will receive the event first). An `On*End()` event will be
received by the listeners in the _reverse_ order. This allows output by
listeners added later to be framed by output from listeners added
earlier.

## Generating Failures in Listeners ##

You may use failure-raising macros (`EXPECT_*()`, `ASSERT_*()`,
`FAIL()`, etc) when processing an event. There are some restrictions:

  1. You cannot generate any failure in `OnTestPartResult()` (otherwise it will cause `OnTestPartResult()` to be called recursively).
  1. A listener that handles `OnTestPartResult()` is not allowed to generate any failure.

When you add listeners to the listener list, you should put listeners
that handle `OnTestPartResult()` _before_ listeners that can generate
failures. This ensures that failures generated by the latter are
attributed to the right test by the former.

We have a sample of failure-raising listener
[here](../samples/sample10_unittest.cc).

# Running Test Programs: Advanced Options #

Google Test test programs are ordinary executables. Once built, you can run
them directly and affect their behavior via the following environment variables
and/or command line flags. For the flags to work, your programs must call
`::testing::InitGoogleTest()` before calling `RUN_ALL_TESTS()`.

To see a list of supported flags and their usage, please run your test
program with the `--help` flag.  You can also use `-h`, `-?`, or `/?`
for short.  This feature is added in version 1.3.0.

If an option is specified both by an environment variable and by a
flag, the latter takes precedence.  Most of the options can also be
set/read in code: to access the value of command line flag
`--gtest_foo`, write `::testing::GTEST_FLAG(foo)`.  A common pattern is
to set the value of a flag before calling `::testing::InitGoogleTest()`
to change the default value of the flag:
```
int main(int argc, char** argv) {
  // Disables elapsed time by default.
  ::testing::GTEST_FLAG(print_time) = false;

  // This allows the user to override the flag on the command line.
  ::testing::InitGoogleTest(&argc, argv);

  return RUN_ALL_TESTS();
}
```

## Selecting Tests ##

This section shows various options for choosing which tests to run.

### Listing Test Names ###

Sometimes it is necessary to list the available tests in a program before
running them so that a filter may be applied if needed. Including the flag
`--gtest_list_tests` overrides all other flags and lists tests in the following
format:
```
TestCase1.
  TestName1
  TestName2
TestCase2.
  TestName
```

None of the tests listed are actually run if the flag is provided. There is no
corresponding environment variable for this flag.

_Availability:_ Linux, Windows, Mac.

### Running a Subset of the Tests ###

By default, a Google Test program runs all tests the user has defined.
Sometimes, you want to run only a subset of the tests (e.g. for debugging or
quickly verifying a change). If you set the `GTEST_FILTER` environment variable
or the `--gtest_filter` flag to a filter string, Google Test will only run the
tests whose full names (in the form of `TestCaseName.TestName`) match the
filter.

The format of a filter is a '`:`'-separated list of wildcard patterns (called
the positive patterns) optionally followed by a '`-`' and another
'`:`'-separated pattern list (called the negative patterns). A test matches the
filter if and only if it matches any of the positive patterns but does not
match any of the negative patterns.

A pattern may contain `'*'` (matches any string) or `'?'` (matches any single
character). For convenience, the filter `'*-NegativePatterns'` can be also
written as `'-NegativePatterns'`.

For example:

  * `./foo_test` Has no flag, and thus runs all its tests.
  * `./foo_test --gtest_filter=*` Also runs everything, due to the single match-everything `*` value.
  * `./foo_test --gtest_filter=FooTest.*` Runs everything in test case `FooTest`.
  * `./foo_test --gtest_filter=*Null*:*Constructor*` Runs any test whose full name contains either `"Null"` or `"Constructor"`.
  * `./foo_test --gtest_filter=-*DeathTest.*` Runs all non-death tests.
  * `./foo_test --gtest_filter=FooTest.*-FooTest.Bar` Runs everything in test case `FooTest` except `FooTest.Bar`.

_Availability:_ Linux, Windows, Mac.

### Temporarily Disabling Tests ###

If you have a broken test that you cannot fix right away, you can add the
`DISABLED_` prefix to its name. This will exclude it from execution. This is
better than commenting out the code or using `#if 0`, as disabled tests are
still compiled (and thus won't rot).

If you need to disable all tests in a test case, you can either add `DISABLED_`
to the front of the name of each test, or alternatively add it to the front of
the test case name.

For example, the following tests won't be run by Google Test, even though they
will still be compiled:

```
// Tests that Foo does Abc.
TEST(FooTest, DISABLED_DoesAbc) { ... }

class DISABLED_BarTest : public ::testing::Test { ... };

// Tests that Bar does Xyz.
TEST_F(DISABLED_BarTest, DoesXyz) { ... }
```

_Note:_ This feature should only be used for temporary pain-relief. You still
have to fix the disabled tests at a later date. As a reminder, Google Test will
print a banner warning you if a test program contains any disabled tests.

_Tip:_ You can easily count the number of disabled tests you have
using `grep`. This number can be used as a metric for improving your
test quality.

_Availability:_ Linux, Windows, Mac.

### Temporarily Enabling Disabled Tests ###

To include [disabled tests](#temporarily-disabling-tests) in test
execution, just invoke the test program with the
`--gtest_also_run_disabled_tests` flag or set the
`GTEST_ALSO_RUN_DISABLED_TESTS` environment variable to a value other
than `0`.  You can combine this with the
[--gtest\_filter](#running-a-subset-of-the-tests) flag to further select
which disabled tests to run.

_Availability:_ Linux, Windows, Mac; since version 1.3.0.

## Repeating the Tests ##

Once in a while you'll run into a test whose result is hit-or-miss. Perhaps it
will fail only 1% of the time, making it rather hard to reproduce the bug under
a debugger. This can be a major source of frustration.

The `--gtest_repeat` flag allows you to repeat all (or selected) test methods
in a program many times. Hopefully, a flaky test will eventually fail and give
you a chance to debug. Here's how to use it:

| `$ foo_test --gtest_repeat=1000` | Repeat foo\_test 1000 times and don't stop at failures. |
|:---------------------------------|:--------------------------------------------------------|
| `$ foo_test --gtest_repeat=-1`   | A negative count means repeating forever.               |
| `$ foo_test --gtest_repeat=1000 --gtest_break_on_failure` | Repeat foo\_test 1000 times, stopping at the first failure. This is especially useful when running under a debugger: when the testfails, it will drop into the debugger and you can then inspect variables and stacks. |
| `$ foo_test --gtest_repeat=1000 --gtest_filter=FooBar` | Repeat the tests whose name matches the filter 1000 times. |

If your test program contains global set-up/tear-down code registered
using `AddGlobalTestEnvironment()`, it will be repeated in each
iteration as well, as the flakiness may be in it. You can also specify
the repeat count by setting the `GTEST_REPEAT` environment variable.

_Availability:_ Linux, Windows, Mac.

## Shuffling the Tests ##

You can specify the `--gtest_shuffle` flag (or set the `GTEST_SHUFFLE`
environment variable to `1`) to run the tests in a program in a random
order. This helps to reveal bad dependencies between tests.

By default, Google Test uses a random seed calculated from the current
time. Therefore you'll get a different order every time. The console
output includes the random seed value, such that you can reproduce an
order-related test failure later. To specify the random seed
explicitly, use the `--gtest_random_seed=SEED` flag (or set the
`GTEST_RANDOM_SEED` environment variable), where `SEED` is an integer
between 0 and 99999. The seed value 0 is special: it tells Google Test
to do the default behavior of calculating the seed from the current
time.

If you combine this with `--gtest_repeat=N`, Google Test will pick a
different random seed and re-shuffle the tests in each iteration.

_Availability:_ Linux, Windows, Mac; since v1.4.0.

## Controlling Test Output ##

This section teaches how to tweak the way test results are reported.

### Colored Terminal Output ###

Google Test can use colors in its terminal output to make it easier to spot
the separation between tests, and whether tests passed.

You can set the GTEST\_COLOR environment variable or set the `--gtest_color`
command line flag to `yes`, `no`, or `auto` (the default) to enable colors,
disable colors, or let Google Test decide. When the value is `auto`, Google
Test will use colors if and only if the output goes to a terminal and (on
non-Windows platforms) the `TERM` environment variable is set to `xterm` or
`xterm-color`.

_Availability:_ Linux, Windows, Mac.

### Suppressing the Elapsed Time ###

By default, Google Test prints the time it takes to run each test.  To
suppress that, run the test program with the `--gtest_print_time=0`
command line flag.  Setting the `GTEST_PRINT_TIME` environment
variable to `0` has the same effect.

_Availability:_ Linux, Windows, Mac.  (In Google Test 1.3.0 and lower,
the default behavior is that the elapsed time is **not** printed.)

### Generating an XML Report ###

Google Test can emit a detailed XML report to a file in addition to its normal
textual output. The report contains the duration of each test, and thus can
help you identify slow tests.

To generate the XML report, set the `GTEST_OUTPUT` environment variable or the
`--gtest_output` flag to the string `"xml:_path_to_output_file_"`, which will
create the file at the given location. You can also just use the string
`"xml"`, in which case the output can be found in the `test_detail.xml` file in
the current directory.

If you specify a directory (for example, `"xml:output/directory/"` on Linux or
`"xml:output\directory\"` on Windows), Google Test will create the XML file in
that directory, named after the test executable (e.g. `foo_test.xml` for test
program `foo_test` or `foo_test.exe`). If the file already exists (perhaps left
over from a previous run), Google Test will pick a different name (e.g.
`foo_test_1.xml`) to avoid overwriting it.

The report uses the format described here.  It is based on the
`junitreport` Ant task and can be parsed by popular continuous build
systems like [Hudson](https://hudson.dev.java.net/). Since that format
was originally intended for Java, a little interpretation is required
to make it apply to Google Test tests, as shown here:

```
<testsuites name="AllTests" ...>
  <testsuite name="test_case_name" ...>
    <testcase name="test_name" ...>
      <failure message="..."/>
      <failure message="..."/>
      <failure message="..."/>
    </testcase>
  </testsuite>
</testsuites>
```

  * The root `<testsuites>` element corresponds to the entire test program.
  * `<testsuite>` elements correspond to Google Test test cases.
  * `<testcase>` elements correspond to Google Test test functions.

For instance, the following program

```
TEST(MathTest, Addition) { ... }
TEST(MathTest, Subtraction) { ... }
TEST(LogicTest, NonContradiction) { ... }
```

could generate this report:

```
<?xml version="1.0" encoding="UTF-8"?>
<testsuites tests="3" failures="1" errors="0" time="35" name="AllTests">
  <testsuite name="MathTest" tests="2" failures="1" errors="0" time="15">
    <testcase name="Addition" status="run" time="7" classname="">
      <failure message="Value of: add(1, 1)&#x0A; Actual: 3&#x0A;Expected: 2" type=""/>
      <failure message="Value of: add(1, -1)&#x0A; Actual: 1&#x0A;Expected: 0" type=""/>
    </testcase>
    <testcase name="Subtraction" status="run" time="5" classname="">
    </testcase>
  </testsuite>
  <testsuite name="LogicTest" tests="1" failures="0" errors="0" time="5">
    <testcase name="NonContradiction" status="run" time="5" classname="">
    </testcase>
  </testsuite>
</testsuites>
```

Things to note:

  * The `tests` attribute of a `<testsuites>` or `<testsuite>` element tells how many test functions the Google Test program or test case contains, while the `failures` attribute tells how many of them failed.
  * The `time` attribute expresses the duration of the test, test case, or entire test program in milliseconds.
  * Each `<failure>` element corresponds to a single failed Google Test assertion.
  * Some JUnit concepts don't apply to Google Test, yet we have to conform to the DTD. Therefore you'll see some dummy elements and attributes in the report. You can safely ignore these parts.

_Availability:_ Linux, Windows, Mac.

## Controlling How Failures Are Reported ##

### Turning Assertion Failures into Break-Points ###

When running test programs under a debugger, it's very convenient if the
debugger can catch an assertion failure and automatically drop into interactive
mode. Google Test's _break-on-failure_ mode supports this behavior.

To enable it, set the `GTEST_BREAK_ON_FAILURE` environment variable to a value
other than `0` . Alternatively, you can use the `--gtest_break_on_failure`
command line flag.

_Availability:_ Linux, Windows, Mac.

### Disabling Catching Test-Thrown Exceptions ###

Google Test can be used either with or without exceptions enabled.  If
a test throws a C++ exception or (on Windows) a structured exception
(SEH), by default Google Test catches it, reports it as a test
failure, and continues with the next test method.  This maximizes the
coverage of a test run.  Also, on Windows an uncaught exception will
cause a pop-up window, so catching the exceptions allows you to run
the tests automatically.

When debugging the test failures, however, you may instead want the
exceptions to be handled by the debugger, such that you can examine
the call stack when an exception is thrown.  To achieve that, set the
`GTEST_CATCH_EXCEPTIONS` environment variable to `0`, or use the
`--gtest_catch_exceptions=0` flag when running the tests.

**Availability**: Linux, Windows, Mac.

### Letting Another Testing Framework Drive ###

If you work on a project that has already been using another testing
framework and is not ready to completely switch to Google Test yet,
you can get much of Google Test's benefit by using its assertions in
your existing tests.  Just change your `main()` function to look
like:

```
#include "gtest/gtest.h"

int main(int argc, char** argv) {
  ::testing::GTEST_FLAG(throw_on_failure) = true;
  // Important: Google Test must be initialized.
  ::testing::InitGoogleTest(&argc, argv);

  ... whatever your existing testing framework requires ...
}
```

With that, you can use Google Test assertions in addition to the
native assertions your testing framework provides, for example:

```
void TestFooDoesBar() {
  Foo foo;
  EXPECT_LE(foo.Bar(1), 100);     // A Google Test assertion.
  CPPUNIT_ASSERT(foo.IsEmpty());  // A native assertion.
}
```

If a Google Test assertion fails, it will print an error message and
throw an exception, which will be treated as a failure by your host
testing framework.  If you compile your code with exceptions disabled,
a failed Google Test assertion will instead exit your program with a
non-zero code, which will also signal a test failure to your test
runner.

If you don't write `::testing::GTEST_FLAG(throw_on_failure) = true;` in
your `main()`, you can alternatively enable this feature by specifying
the `--gtest_throw_on_failure` flag on the command-line or setting the
`GTEST_THROW_ON_FAILURE` environment variable to a non-zero value.

Death tests are _not_ supported when other test framework is used to organize tests.

_Availability:_ Linux, Windows, Mac; since v1.3.0.

## Distributing Test Functions to Multiple Machines ##

If you have more than one machine you can use to run a test program,
you might want to run the test functions in parallel and get the
result faster.  We call this technique _sharding_, where each machine
is called a _shard_.

Google Test is compatible with test sharding.  To take advantage of
this feature, your test runner (not part of Google Test) needs to do
the following:

  1. Allocate a number of machines (shards) to run the tests.
  1. On each shard, set the `GTEST_TOTAL_SHARDS` environment variable to the total number of shards.  It must be the same for all shards.
  1. On each shard, set the `GTEST_SHARD_INDEX` environment variable to the index of the shard.  Different shards must be assigned different indices, which must be in the range `[0, GTEST_TOTAL_SHARDS - 1]`.
  1. Run the same test program on all shards.  When Google Test sees the above two environment variables, it will select a subset of the test functions to run.  Across all shards, each test function in the program will be run exactly once.
  1. Wait for all shards to finish, then collect and report the results.

Your project may have tests that were written without Google Test and
thus don't understand this protocol.  In order for your test runner to
figure out which test supports sharding, it can set the environment
variable `GTEST_SHARD_STATUS_FILE` to a non-existent file path.  If a
test program supports sharding, it will create this file to
acknowledge the fact (the actual contents of the file are not
important at this time; although we may stick some useful information
in it in the future.); otherwise it will not create it.

Here's an example to make it clear.  Suppose you have a test program
`foo_test` that contains the following 5 test functions:
```
TEST(A, V)
TEST(A, W)
TEST(B, X)
TEST(B, Y)
TEST(B, Z)
```
and you have 3 machines at your disposal.  To run the test functions in
parallel, you would set `GTEST_TOTAL_SHARDS` to 3 on all machines, and
set `GTEST_SHARD_INDEX` to 0, 1, and 2 on the machines respectively.
Then you would run the same `foo_test` on each machine.

Google Test reserves the right to change how the work is distributed
across the shards, but here's one possible scenario:

  * Machine #0 runs `A.V` and `B.X`.
  * Machine #1 runs `A.W` and `B.Y`.
  * Machine #2 runs `B.Z`.

_Availability:_ Linux, Windows, Mac; since version 1.3.0.

# Fusing Google Test Source Files #

Google Test's implementation consists of ~30 files (excluding its own
tests).  Sometimes you may want them to be packaged up in two files (a
`.h` and a `.cc`) instead, such that you can easily copy them to a new
machine and start hacking there.  For this we provide an experimental
Python script `fuse_gtest_files.py` in the `scripts/` directory (since release 1.3.0).
Assuming you have Python 2.4 or above installed on your machine, just
go to that directory and run
```
python fuse_gtest_files.py OUTPUT_DIR
```

and you should see an `OUTPUT_DIR` directory being created with files
`gtest/gtest.h` and `gtest/gtest-all.cc` in it.  These files contain
everything you need to use Google Test.  Just copy them to anywhere
you want and you are ready to write tests.  You can use the
[scripts/test/Makefile](../scripts/test/Makefile)
file as an example on how to compile your tests against them.

# Where to Go from Here #

Congratulations! You've now learned more advanced Google Test tools and are
ready to tackle more complex testing tasks. If you want to dive even deeper, you
can read the [Frequently-Asked Questions](FAQ.md).


If you are interested in understanding the internals of Google Test,
building from source, or contributing ideas or modifications to the
project, then this document is for you.

# Introduction #

First, let's give you some background of the project.

## Licensing ##

All Google Test source and pre-built packages are provided under the [New BSD License](http://www.opensource.org/licenses/bsd-license.php).

## The Google Test Community ##

The Google Test community exists primarily through the [discussion group](http://groups.google.com/group/googletestframework) and the GitHub repository.
You are definitely encouraged to contribute to the
discussion and you can also help us to keep the effectiveness of the
group high by following and promoting the guidelines listed here.

### Please Be Friendly ###

Showing courtesy and respect to others is a vital part of the Google
culture, and we strongly encourage everyone participating in Google
Test development to join us in accepting nothing less. Of course,
being courteous is not the same as failing to constructively disagree
with each other, but it does mean that we should be respectful of each
other when enumerating the 42 technical reasons that a particular
proposal may not be the best choice. There's never a reason to be
antagonistic or dismissive toward anyone who is sincerely trying to
contribute to a discussion.

Sure, C++ testing is serious business and all that, but it's also
a lot of fun. Let's keep it that way. Let's strive to be one of the
friendliest communities in all of open source.

As always, discuss Google Test in the official GoogleTest discussion group.
You don't have to actually submit code in order to sign up. Your participation
itself is a valuable contribution.

# Working with the Code #

If you want to get your hands dirty with the code inside Google Test,
this is the section for you.

## Compiling from Source ##

Once you check out the code, you can find instructions on how to
compile it in the [README](../README.md) file.

## Testing ##

A testing framework is of no good if itself is not thoroughly tested.
Tests should be written for any new code, and changes should be
verified to not break existing tests before they are submitted for
review. To perform the tests, follow the instructions in
[README](../README.md) and verify that there are no failures.

# Contributing Code #

We are excited that Google Test is now open source, and hope to get
great patches from the community. Before you fire up your favorite IDE
and begin hammering away at that new feature, though, please take the
time to read this section and understand the process. While it seems
rigorous, we want to keep a high standard of quality in the code
base.

## Contributor License Agreements ##

You must sign a Contributor License Agreement (CLA) before we can
accept any code.  The CLA protects you and us.

  * If you are an individual writing original source code and you're sure you own the intellectual property, then you'll need to sign an [individual CLA](http://code.google.com/legal/individual-cla-v1.0.html).
  * If you work for a company that wants to allow you to contribute your work to Google Test, then you'll need to sign a [corporate CLA](http://code.google.com/legal/corporate-cla-v1.0.html).

Follow either of the two links above to access the appropriate CLA and
instructions for how to sign and return it.

## Coding Style ##

To keep the source consistent, readable, diffable and easy to merge,
we use a fairly rigid coding style, as defined by the [google-styleguide](https://github.com/google/styleguide) project.  All patches will be expected
to conform to the style outlined [here](https://google.github.io/styleguide/cppguide.html).

## Updating Generated Code ##

Some of Google Test's source files are generated by the Pump tool (a
Python script).  If you need to update such files, please modify the
source (`foo.h.pump`) and re-generate the C++ file using Pump.  You
can read the PumpManual for details.

## Submitting Patches ##

Please do submit code. Here's what you need to do:

  1. A submission should be a set of changes that addresses one issue in the [issue tracker](https://github.com/google/googletest/issues). Please don't mix more than one logical change per submittal, because it makes the history hard to follow. If you want to make a change that doesn't have a corresponding issue in the issue tracker, please create one.
  1. Also, coordinate with team members that are listed on the issue in question. This ensures that work isn't being duplicated and communicating your plan early also generally leads to better patches.
  1. Ensure that your code adheres to the [Google Test source code style](#Coding_Style.md).
  1. Ensure that there are unit tests for your code.
  1. Sign a Contributor License Agreement.
  1. Create a Pull Request in the usual way.

If you are a Googler, it is preferable to first create an internal change and
have it reviewed and submitted, and then create an upstreaming pull
request here. 

## Google Test Committers ##

The current members of the Google Test engineering team are the only
committers at present. In the great tradition of eating one's own
dogfood, we will be requiring each new Google Test engineering team
member to earn the right to become a committer by following the
procedures in this document, writing consistently great code, and
demonstrating repeatedly that he or she truly gets the zen of Google
Test.

# Release Process #

We follow a typical release process:

  1. A release branch named `release-X.Y` is created.
  1. Bugs are fixed and features are added in trunk; those individual patches are merged into the release branch until it's stable.
  1. An individual point release (the `Z` in `X.Y.Z`) is made by creating a tag from the branch.
  1. Repeat steps 2 and 3 throughout one release cycle (as determined by features or time).
  1. Go back to step 1 to create another release branch and so on.

---

This page is based on the [Making GWT Better](http://code.google.com/webtoolkit/makinggwtbetter.html) guide from the [Google Web Toolkit](http://code.google.com/webtoolkit/) project.  Except as otherwise [noted](http://code.google.com/policies.html#restrictions), the content of this page is licensed under the [Creative Commons Attribution 2.5 License](http://creativecommons.org/licenses/by/2.5/).
This page lists all documentation markdown files for Google Test **(the
current git version)**
-- **if you use a former version of Google Test, please read the
documentation for that specific version instead (e.g. by checking out
the respective git branch/tag).**

  * [Primer](Primer.md) -- start here if you are new to Google Test.
  * [Samples](Samples.md) -- learn from examples.
  * [AdvancedGuide](AdvancedGuide.md) -- learn more about Google Test.
  * [XcodeGuide](XcodeGuide.md) -- how to use Google Test in Xcode on Mac.
  * [Frequently-Asked Questions](FAQ.md) -- check here before asking a question on the mailing list.

To contribute code to Google Test, read:

  * [DevGuide](DevGuide.md) -- read this _before_ writing your first patch.
  * [PumpManual](PumpManual.md) -- how we generate some of Google Test's source files.


If you cannot find the answer to your question here, and you have read
[Primer](Primer.md) and [AdvancedGuide](AdvancedGuide.md), send it to
googletestframework@googlegroups.com.

## Why should I use Google Test instead of my favorite C++ testing framework? ##

First, let us say clearly that we don't want to get into the debate of
which C++ testing framework is **the best**.  There exist many fine
frameworks for writing C++ tests, and we have tremendous respect for
the developers and users of them.  We don't think there is (or will
be) a single best framework - you have to pick the right tool for the
particular task you are tackling.

We created Google Test because we couldn't find the right combination
of features and conveniences in an existing framework to satisfy _our_
needs.  The following is a list of things that _we_ like about Google
Test.  We don't claim them to be unique to Google Test - rather, the
combination of them makes Google Test the choice for us.  We hope this
list can help you decide whether it is for you too.

  * Google Test is designed to be portable: it doesn't require exceptions or RTTI; it works around various bugs in various compilers and environments; etc.  As a result, it works on Linux, Mac OS X, Windows and several embedded operating systems.
  * Nonfatal assertions (`EXPECT_*`) have proven to be great time savers, as they allow a test to report multiple failures in a single edit-compile-test cycle.
  * It's easy to write assertions that generate informative messages: you just use the stream syntax to append any additional information, e.g. `ASSERT_EQ(5, Foo(i)) << " where i = " << i;`.  It doesn't require a new set of macros or special functions.
  * Google Test automatically detects your tests and doesn't require you to enumerate them in order to run them.
  * Death tests are pretty handy for ensuring that your asserts in production code are triggered by the right conditions.
  * `SCOPED_TRACE` helps you understand the context of an assertion failure when it comes from inside a sub-routine or loop.
  * You can decide which tests to run using name patterns.  This saves time when you want to quickly reproduce a test failure.
  * Google Test can generate XML test result reports that can be parsed by popular continuous build system like Hudson.
  * Simple things are easy in Google Test, while hard things are possible: in addition to advanced features like [global test environments](AdvancedGuide.md#global-set-up-and-tear-down) and tests parameterized by [values](AdvancedGuide.md#value-parameterized-tests) or [types](docs/AdvancedGuide.md#typed-tests), Google Test supports various ways for the user to extend the framework -- if Google Test doesn't do something out of the box, chances are that a user can implement the feature using Google Test's public API, without changing Google Test itself.  In particular, you can:
    * expand your testing vocabulary by defining [custom predicates](AdvancedGuide.md#predicate-assertions-for-better-error-messages),
    * teach Google Test how to [print your types](AdvancedGuide.md#teaching-google-test-how-to-print-your-values),
    * define your own testing macros or utilities and verify them using Google Test's [Service Provider Interface](AdvancedGuide.md#catching-failures), and
    * reflect on the test cases or change the test output format by intercepting the [test events](AdvancedGuide.md#extending-google-test-by-handling-test-events).

## I'm getting warnings when compiling Google Test.  Would you fix them? ##

We strive to minimize compiler warnings Google Test generates.  Before releasing a new version, we test to make sure that it doesn't generate warnings when compiled using its CMake script on Windows, Linux, and Mac OS.

Unfortunately, this doesn't mean you are guaranteed to see no warnings when compiling Google Test in your environment:

  * You may be using a different compiler as we use, or a different version of the same compiler.  We cannot possibly test for all compilers.
  * You may be compiling on a different platform as we do.
  * Your project may be using different compiler flags as we do.

It is not always possible to make Google Test warning-free for everyone.  Or, it may not be desirable if the warning is rarely enabled and fixing the violations makes the code more complex.

If you see warnings when compiling Google Test, we suggest that you use the `-isystem` flag (assuming your are using GCC) to mark Google Test headers as system headers.  That'll suppress warnings from Google Test headers.

## Why should not test case names and test names contain underscore? ##

Underscore (`_`) is special, as C++ reserves the following to be used by
the compiler and the standard library:

  1. any identifier that starts with an `_` followed by an upper-case letter, and
  1. any identifier that contains two consecutive underscores (i.e. `__`) _anywhere_ in its name.

User code is _prohibited_ from using such identifiers.

Now let's look at what this means for `TEST` and `TEST_F`.

Currently `TEST(TestCaseName, TestName)` generates a class named
`TestCaseName_TestName_Test`.  What happens if `TestCaseName` or `TestName`
contains `_`?

  1. If `TestCaseName` starts with an `_` followed by an upper-case letter (say, `_Foo`), we end up with `_Foo_TestName_Test`, which is reserved and thus invalid.
  1. If `TestCaseName` ends with an `_` (say, `Foo_`), we get `Foo__TestName_Test`, which is invalid.
  1. If `TestName` starts with an `_` (say, `_Bar`), we get `TestCaseName__Bar_Test`, which is invalid.
  1. If `TestName` ends with an `_` (say, `Bar_`), we get `TestCaseName_Bar__Test`, which is invalid.

So clearly `TestCaseName` and `TestName` cannot start or end with `_`
(Actually, `TestCaseName` can start with `_` -- as long as the `_` isn't
followed by an upper-case letter.  But that's getting complicated.  So
for simplicity we just say that it cannot start with `_`.).

It may seem fine for `TestCaseName` and `TestName` to contain `_` in the
middle.  However, consider this:
``` cpp
TEST(Time, Flies_Like_An_Arrow) { ... }
TEST(Time_Flies, Like_An_Arrow) { ... }
```

Now, the two `TEST`s will both generate the same class
(`Time_Files_Like_An_Arrow_Test`).  That's not good.

So for simplicity, we just ask the users to avoid `_` in `TestCaseName`
and `TestName`.  The rule is more constraining than necessary, but it's
simple and easy to remember.  It also gives Google Test some wiggle
room in case its implementation needs to change in the future.

If you violate the rule, there may not be immediately consequences,
but your test may (just may) break with a new compiler (or a new
version of the compiler you are using) or with a new version of Google
Test.  Therefore it's best to follow the rule.

## Why is it not recommended to install a pre-compiled copy of Google Test (for example, into /usr/local)? ##

In the early days, we said that you could install
compiled Google Test libraries on `*`nix systems using `make install`.
Then every user of your machine can write tests without
recompiling Google Test.

This seemed like a good idea, but it has a
got-cha: every user needs to compile their tests using the _same_ compiler
flags used to compile the installed Google Test libraries; otherwise
they may run into undefined behaviors (i.e. the tests can behave
strangely and may even crash for no obvious reasons).

Why?  Because C++ has this thing called the One-Definition Rule: if
two C++ source files contain different definitions of the same
class/function/variable, and you link them together, you violate the
rule.  The linker may or may not catch the error (in many cases it's
not required by the C++ standard to catch the violation).  If it
doesn't, you get strange run-time behaviors that are unexpected and
hard to debug.

If you compile Google Test and your test code using different compiler
flags, they may see different definitions of the same
class/function/variable (e.g. due to the use of `#if` in Google Test).
Therefore, for your sanity, we recommend to avoid installing pre-compiled
Google Test libraries.  Instead, each project should compile
Google Test itself such that it can be sure that the same flags are
used for both Google Test and the tests.

## How do I generate 64-bit binaries on Windows (using Visual Studio 2008)? ##

(Answered by Trevor Robinson)

Load the supplied Visual Studio solution file, either `msvc\gtest-md.sln` or
`msvc\gtest.sln`. Go through the migration wizard to migrate the
solution and project files to Visual Studio 2008. Select
`Configuration Manager...` from the `Build` menu. Select `<New...>` from
the `Active solution platform` dropdown.  Select `x64` from the new
platform dropdown, leave `Copy settings from` set to `Win32` and
`Create new project platforms` checked, then click `OK`. You now have
`Win32` and `x64` platform configurations, selectable from the
`Standard` toolbar, which allow you to toggle between building 32-bit or
64-bit binaries (or both at once using Batch Build).

In order to prevent build output files from overwriting one another,
you'll need to change the `Intermediate Directory` settings for the
newly created platform configuration across all the projects. To do
this, multi-select (e.g. using shift-click) all projects (but not the
solution) in the `Solution Explorer`. Right-click one of them and
select `Properties`. In the left pane, select `Configuration Properties`,
and from the `Configuration` dropdown, select `All Configurations`.
Make sure the selected platform is `x64`. For the
`Intermediate Directory` setting, change the value from
`$(PlatformName)\$(ConfigurationName)` to
`$(OutDir)\$(ProjectName)`. Click `OK` and then build the
solution. When the build is complete, the 64-bit binaries will be in
the `msvc\x64\Debug` directory.

## Can I use Google Test on MinGW? ##

We haven't tested this ourselves, but Per Abrahamsen reported that he
was able to compile and install Google Test successfully when using
MinGW from Cygwin.  You'll need to configure it with:

`PATH/TO/configure CC="gcc -mno-cygwin" CXX="g++ -mno-cygwin"`

You should be able to replace the `-mno-cygwin` option with direct links
to the real MinGW binaries, but we haven't tried that.

Caveats:

  * There are many warnings when compiling.
  * `make check` will produce some errors as not all tests for Google Test itself are compatible with MinGW.

We also have reports on successful cross compilation of Google Test
MinGW binaries on Linux using
[these instructions](http://wiki.wxwidgets.org/Cross-Compiling_Under_Linux#Cross-compiling_under_Linux_for_MS_Windows)
on the WxWidgets site.

Please contact `googletestframework@googlegroups.com` if you are
interested in improving the support for MinGW.

## Why does Google Test support EXPECT\_EQ(NULL, ptr) and ASSERT\_EQ(NULL, ptr) but not EXPECT\_NE(NULL, ptr) and ASSERT\_NE(NULL, ptr)? ##

Due to some peculiarity of C++, it requires some non-trivial template
meta programming tricks to support using `NULL` as an argument of the
`EXPECT_XX()` and `ASSERT_XX()` macros. Therefore we only do it where
it's most needed (otherwise we make the implementation of Google Test
harder to maintain and more error-prone than necessary).

The `EXPECT_EQ()` macro takes the _expected_ value as its first
argument and the _actual_ value as the second. It's reasonable that
someone wants to write `EXPECT_EQ(NULL, some_expression)`, and this
indeed was requested several times. Therefore we implemented it.

The need for `EXPECT_NE(NULL, ptr)` isn't nearly as strong. When the
assertion fails, you already know that `ptr` must be `NULL`, so it
doesn't add any information to print ptr in this case. That means
`EXPECT_TRUE(ptr != NULL)` works just as well.

If we were to support `EXPECT_NE(NULL, ptr)`, for consistency we'll
have to support `EXPECT_NE(ptr, NULL)` as well, as unlike `EXPECT_EQ`,
we don't have a convention on the order of the two arguments for
`EXPECT_NE`. This means using the template meta programming tricks
twice in the implementation, making it even harder to understand and
maintain. We believe the benefit doesn't justify the cost.

Finally, with the growth of Google Mock's [matcher](../../googlemock/docs/CookBook.md#using-matchers-in-google-test-assertions) library, we are
encouraging people to use the unified `EXPECT_THAT(value, matcher)`
syntax more often in tests. One significant advantage of the matcher
approach is that matchers can be easily combined to form new matchers,
while the `EXPECT_NE`, etc, macros cannot be easily
combined. Therefore we want to invest more in the matchers than in the
`EXPECT_XX()` macros.

## Does Google Test support running tests in parallel? ##

Test runners tend to be tightly coupled with the build/test
environment, and Google Test doesn't try to solve the problem of
running tests in parallel.  Instead, we tried to make Google Test work
nicely with test runners.  For example, Google Test's XML report
contains the time spent on each test, and its `gtest_list_tests` and
`gtest_filter` flags can be used for splitting the execution of test
methods into multiple processes.  These functionalities can help the
test runner run the tests in parallel.

## Why don't Google Test run the tests in different threads to speed things up? ##

It's difficult to write thread-safe code.  Most tests are not written
with thread-safety in mind, and thus may not work correctly in a
multi-threaded setting.

If you think about it, it's already hard to make your code work when
you know what other threads are doing.  It's much harder, and
sometimes even impossible, to make your code work when you don't know
what other threads are doing (remember that test methods can be added,
deleted, or modified after your test was written).  If you want to run
the tests in parallel, you'd better run them in different processes.

## Why aren't Google Test assertions implemented using exceptions? ##

Our original motivation was to be able to use Google Test in projects
that disable exceptions.  Later we realized some additional benefits
of this approach:

  1. Throwing in a destructor is undefined behavior in C++.  Not using exceptions means Google Test's assertions are safe to use in destructors.
  1. The `EXPECT_*` family of macros will continue even after a failure, allowing multiple failures in a `TEST` to be reported in a single run. This is a popular feature, as in C++ the edit-compile-test cycle is usually quite long and being able to fixing more than one thing at a time is a blessing.
  1. If assertions are implemented using exceptions, a test may falsely ignore a failure if it's caught by user code:
``` cpp
try { ... ASSERT_TRUE(...) ... }
catch (...) { ... }
```
The above code will pass even if the `ASSERT_TRUE` throws.  While it's unlikely for someone to write this in a test, it's possible to run into this pattern when you write assertions in callbacks that are called by the code under test.

The downside of not using exceptions is that `ASSERT_*` (implemented
using `return`) will only abort the current function, not the current
`TEST`.

## Why do we use two different macros for tests with and without fixtures? ##

Unfortunately, C++'s macro system doesn't allow us to use the same
macro for both cases.  One possibility is to provide only one macro
for tests with fixtures, and require the user to define an empty
fixture sometimes:

``` cpp
class FooTest : public ::testing::Test {};

TEST_F(FooTest, DoesThis) { ... }
```
or
``` cpp
typedef ::testing::Test FooTest;

TEST_F(FooTest, DoesThat) { ... }
```

Yet, many people think this is one line too many. :-) Our goal was to
make it really easy to write tests, so we tried to make simple tests
trivial to create.  That means using a separate macro for such tests.

We think neither approach is ideal, yet either of them is reasonable.
In the end, it probably doesn't matter much either way.

## Why don't we use structs as test fixtures? ##

We like to use structs only when representing passive data.  This
distinction between structs and classes is good for documenting the
intent of the code's author.  Since test fixtures have logic like
`SetUp()` and `TearDown()`, they are better defined as classes.

## Why are death tests implemented as assertions instead of using a test runner? ##

Our goal was to make death tests as convenient for a user as C++
possibly allows.  In particular:

  * The runner-style requires to split the information into two pieces: the definition of the death test itself, and the specification for the runner on how to run the death test and what to expect.  The death test would be written in C++, while the runner spec may or may not be.  A user needs to carefully keep the two in sync. `ASSERT_DEATH(statement, expected_message)` specifies all necessary information in one place, in one language, without boilerplate code. It is very declarative.
  * `ASSERT_DEATH` has a similar syntax and error-reporting semantics as other Google Test assertions, and thus is easy to learn.
  * `ASSERT_DEATH` can be mixed with other assertions and other logic at your will.  You are not limited to one death test per test method. For example, you can write something like:
``` cpp
    if (FooCondition()) {
      ASSERT_DEATH(Bar(), "blah");
    } else {
      ASSERT_EQ(5, Bar());
    }
```
If you prefer one death test per test method, you can write your tests in that style too, but we don't want to impose that on the users.  The fewer artificial limitations the better.
  * `ASSERT_DEATH` can reference local variables in the current function, and you can decide how many death tests you want based on run-time information.  For example,
``` cpp
    const int count = GetCount();  // Only known at run time.
    for (int i = 1; i <= count; i++) {
      ASSERT_DEATH({
        double* buffer = new double[i];
        ... initializes buffer ...
        Foo(buffer, i)
      }, "blah blah");
    }
```
The runner-based approach tends to be more static and less flexible, or requires more user effort to get this kind of flexibility.

Another interesting thing about `ASSERT_DEATH` is that it calls `fork()`
to create a child process to run the death test.  This is lightening
fast, as `fork()` uses copy-on-write pages and incurs almost zero
overhead, and the child process starts from the user-supplied
statement directly, skipping all global and local initialization and
any code leading to the given statement.  If you launch the child
process from scratch, it can take seconds just to load everything and
start running if the test links to many libraries dynamically.

## My death test modifies some state, but the change seems lost after the death test finishes. Why? ##

Death tests (`EXPECT_DEATH`, etc) are executed in a sub-process s.t. the
expected crash won't kill the test program (i.e. the parent process). As a
result, any in-memory side effects they incur are observable in their
respective sub-processes, but not in the parent process. You can think of them
as running in a parallel universe, more or less.

## The compiler complains about "undefined references" to some static const member variables, but I did define them in the class body. What's wrong? ##

If your class has a static data member:

``` cpp
// foo.h
class Foo {
  ...
  static const int kBar = 100;
};
```

You also need to define it _outside_ of the class body in `foo.cc`:

``` cpp
const int Foo::kBar;  // No initializer here.
```

Otherwise your code is **invalid C++**, and may break in unexpected ways. In
particular, using it in Google Test comparison assertions (`EXPECT_EQ`, etc)
will generate an "undefined reference" linker error.

## I have an interface that has several implementations. Can I write a set of tests once and repeat them over all the implementations? ##

Google Test doesn't yet have good support for this kind of tests, or
data-driven tests in general. We hope to be able to make improvements in this
area soon.

## Can I derive a test fixture from another? ##

Yes.

Each test fixture has a corresponding and same named test case. This means only
one test case can use a particular fixture. Sometimes, however, multiple test
cases may want to use the same or slightly different fixtures. For example, you
may want to make sure that all of a GUI library's test cases don't leak
important system resources like fonts and brushes.

In Google Test, you share a fixture among test cases by putting the shared
logic in a base test fixture, then deriving from that base a separate fixture
for each test case that wants to use this common logic. You then use `TEST_F()`
to write tests using each derived fixture.

Typically, your code looks like this:

``` cpp
// Defines a base test fixture.
class BaseTest : public ::testing::Test {
  protected:
   ...
};

// Derives a fixture FooTest from BaseTest.
class FooTest : public BaseTest {
  protected:
    virtual void SetUp() {
      BaseTest::SetUp();  // Sets up the base fixture first.
      ... additional set-up work ...
    }
    virtual void TearDown() {
      ... clean-up work for FooTest ...
      BaseTest::TearDown();  // Remember to tear down the base fixture
                             // after cleaning up FooTest!
    }
    ... functions and variables for FooTest ...
};

// Tests that use the fixture FooTest.
TEST_F(FooTest, Bar) { ... }
TEST_F(FooTest, Baz) { ... }

... additional fixtures derived from BaseTest ...
```

If necessary, you can continue to derive test fixtures from a derived fixture.
Google Test has no limit on how deep the hierarchy can be.

For a complete example using derived test fixtures, see
[sample5](../samples/sample5_unittest.cc).

## My compiler complains "void value not ignored as it ought to be." What does this mean? ##

You're probably using an `ASSERT_*()` in a function that doesn't return `void`.
`ASSERT_*()` can only be used in `void` functions.

## My death test hangs (or seg-faults). How do I fix it? ##

In Google Test, death tests are run in a child process and the way they work is
delicate. To write death tests you really need to understand how they work.
Please make sure you have read this.

In particular, death tests don't like having multiple threads in the parent
process. So the first thing you can try is to eliminate creating threads
outside of `EXPECT_DEATH()`.

Sometimes this is impossible as some library you must use may be creating
threads before `main()` is even reached. In this case, you can try to minimize
the chance of conflicts by either moving as many activities as possible inside
`EXPECT_DEATH()` (in the extreme case, you want to move everything inside), or
leaving as few things as possible in it. Also, you can try to set the death
test style to `"threadsafe"`, which is safer but slower, and see if it helps.

If you go with thread-safe death tests, remember that they rerun the test
program from the beginning in the child process. Therefore make sure your
program can run side-by-side with itself and is deterministic.

In the end, this boils down to good concurrent programming. You have to make
sure that there is no race conditions or dead locks in your program. No silver
bullet - sorry!

## Should I use the constructor/destructor of the test fixture or the set-up/tear-down function? ##

The first thing to remember is that Google Test does not reuse the
same test fixture object across multiple tests. For each `TEST_F`,
Google Test will create a fresh test fixture object, _immediately_
call `SetUp()`, run the test body, call `TearDown()`, and then
_immediately_ delete the test fixture object.

When you need to write per-test set-up and tear-down logic, you have
the choice between using the test fixture constructor/destructor or
`SetUp()/TearDown()`. The former is usually preferred, as it has the
following benefits:

  * By initializing a member variable in the constructor, we have the option to make it `const`, which helps prevent accidental changes to its value and makes the tests more obviously correct.
  * In case we need to subclass the test fixture class, the subclass' constructor is guaranteed to call the base class' constructor first, and the subclass' destructor is guaranteed to call the base class' destructor afterward. With `SetUp()/TearDown()`, a subclass may make the mistake of forgetting to call the base class' `SetUp()/TearDown()` or call them at the wrong moment.

You may still want to use `SetUp()/TearDown()` in the following rare cases:
  * If the tear-down operation could throw an exception, you must use `TearDown()` as opposed to the destructor, as throwing in a destructor leads to undefined behavior and usually will kill your program right away. Note that many standard libraries (like STL) may throw when exceptions are enabled in the compiler. Therefore you should prefer `TearDown()` if you want to write portable tests that work with or without exceptions.
  * The assertion macros throw an exception when flag `--gtest_throw_on_failure` is specified. Therefore, you shouldn't use Google Test assertions in a destructor if you plan to run your tests with this flag.
  * In a constructor or destructor, you cannot make a virtual function call on this object. (You can call a method declared as virtual, but it will be statically bound.) Therefore, if you need to call a method that will be overriden in a derived class, you have to use `SetUp()/TearDown()`.

## The compiler complains "no matching function to call" when I use ASSERT\_PREDn. How do I fix it? ##

If the predicate function you use in `ASSERT_PRED*` or `EXPECT_PRED*` is
overloaded or a template, the compiler will have trouble figuring out which
overloaded version it should use. `ASSERT_PRED_FORMAT*` and
`EXPECT_PRED_FORMAT*` don't have this problem.

If you see this error, you might want to switch to
`(ASSERT|EXPECT)_PRED_FORMAT*`, which will also give you a better failure
message. If, however, that is not an option, you can resolve the problem by
explicitly telling the compiler which version to pick.

For example, suppose you have

``` cpp
bool IsPositive(int n) {
  return n > 0;
}
bool IsPositive(double x) {
  return x > 0;
}
```

you will get a compiler error if you write

``` cpp
EXPECT_PRED1(IsPositive, 5);
```

However, this will work:

``` cpp
EXPECT_PRED1(static_cast<bool (*)(int)>(IsPositive), 5);
```

(The stuff inside the angled brackets for the `static_cast` operator is the
type of the function pointer for the `int`-version of `IsPositive()`.)

As another example, when you have a template function

``` cpp
template <typename T>
bool IsNegative(T x) {
  return x < 0;
}
```

you can use it in a predicate assertion like this:

``` cpp
ASSERT_PRED1(IsNegative<int>, -5);
```

Things are more interesting if your template has more than one parameters. The
following won't compile:

``` cpp
ASSERT_PRED2(GreaterThan<int, int>, 5, 0);
```


as the C++ pre-processor thinks you are giving `ASSERT_PRED2` 4 arguments,
which is one more than expected. The workaround is to wrap the predicate
function in parentheses:

``` cpp
ASSERT_PRED2((GreaterThan<int, int>), 5, 0);
```


## My compiler complains about "ignoring return value" when I call RUN\_ALL\_TESTS(). Why? ##

Some people had been ignoring the return value of `RUN_ALL_TESTS()`. That is,
instead of

``` cpp
return RUN_ALL_TESTS();
```

they write

``` cpp
RUN_ALL_TESTS();
```

This is wrong and dangerous. A test runner needs to see the return value of
`RUN_ALL_TESTS()` in order to determine if a test has passed. If your `main()`
function ignores it, your test will be considered successful even if it has a
Google Test assertion failure. Very bad.

To help the users avoid this dangerous bug, the implementation of
`RUN_ALL_TESTS()` causes gcc to raise this warning, when the return value is
ignored. If you see this warning, the fix is simple: just make sure its value
is used as the return value of `main()`.

## My compiler complains that a constructor (or destructor) cannot return a value. What's going on? ##

Due to a peculiarity of C++, in order to support the syntax for streaming
messages to an `ASSERT_*`, e.g.

``` cpp
ASSERT_EQ(1, Foo()) << "blah blah" << foo;
```

we had to give up using `ASSERT*` and `FAIL*` (but not `EXPECT*` and
`ADD_FAILURE*`) in constructors and destructors. The workaround is to move the
content of your constructor/destructor to a private void member function, or
switch to `EXPECT_*()` if that works. This section in the user's guide explains
it.

## My set-up function is not called. Why? ##

C++ is case-sensitive. It should be spelled as `SetUp()`.  Did you
spell it as `Setup()`?

Similarly, sometimes people spell `SetUpTestCase()` as `SetupTestCase()` and
wonder why it's never called.

## How do I jump to the line of a failure in Emacs directly? ##

Google Test's failure message format is understood by Emacs and many other
IDEs, like acme and XCode. If a Google Test message is in a compilation buffer
in Emacs, then it's clickable. You can now hit `enter` on a message to jump to
the corresponding source code, or use `C-x `` to jump to the next failure.

## I have several test cases which share the same test fixture logic, do I have to define a new test fixture class for each of them? This seems pretty tedious. ##

You don't have to. Instead of

``` cpp
class FooTest : public BaseTest {};

TEST_F(FooTest, Abc) { ... }
TEST_F(FooTest, Def) { ... }

class BarTest : public BaseTest {};

TEST_F(BarTest, Abc) { ... }
TEST_F(BarTest, Def) { ... }
```

you can simply `typedef` the test fixtures:
``` cpp
typedef BaseTest FooTest;

TEST_F(FooTest, Abc) { ... }
TEST_F(FooTest, Def) { ... }

typedef BaseTest BarTest;

TEST_F(BarTest, Abc) { ... }
TEST_F(BarTest, Def) { ... }
```

## The Google Test output is buried in a whole bunch of log messages. What do I do? ##

The Google Test output is meant to be a concise and human-friendly report. If
your test generates textual output itself, it will mix with the Google Test
output, making it hard to read. However, there is an easy solution to this
problem.

Since most log messages go to stderr, we decided to let Google Test output go
to stdout. This way, you can easily separate the two using redirection. For
example:
```
./my_test > googletest_output.txt
```

## Why should I prefer test fixtures over global variables? ##

There are several good reasons:
  1. It's likely your test needs to change the states of its global variables. This makes it difficult to keep side effects from escaping one test and contaminating others, making debugging difficult. By using fixtures, each test has a fresh set of variables that's different (but with the same names). Thus, tests are kept independent of each other.
  1. Global variables pollute the global namespace.
  1. Test fixtures can be reused via subclassing, which cannot be done easily with global variables. This is useful if many test cases have something in common.

## How do I test private class members without writing FRIEND\_TEST()s? ##

You should try to write testable code, which means classes should be easily
tested from their public interface. One way to achieve this is the Pimpl idiom:
you move all private members of a class into a helper class, and make all
members of the helper class public.

You have several other options that don't require using `FRIEND_TEST`:
  * Write the tests as members of the fixture class:
``` cpp
class Foo {
  friend class FooTest;
  ...
};

class FooTest : public ::testing::Test {
 protected:
  ...
  void Test1() {...} // This accesses private members of class Foo.
  void Test2() {...} // So does this one.
};

TEST_F(FooTest, Test1) {
  Test1();
}

TEST_F(FooTest, Test2) {
  Test2();
}
```
  * In the fixture class, write accessors for the tested class' private members, then use the accessors in your tests:
``` cpp
class Foo {
  friend class FooTest;
  ...
};

class FooTest : public ::testing::Test {
 protected:
  ...
  T1 get_private_member1(Foo* obj) {
    return obj->private_member1_;
  }
};

TEST_F(FooTest, Test1) {
  ...
  get_private_member1(x)
  ...
}
```
  * If the methods are declared **protected**, you can change their access level in a test-only subclass:
``` cpp
class YourClass {
  ...
 protected: // protected access for testability.
  int DoSomethingReturningInt();
  ...
};

// in the your_class_test.cc file:
class TestableYourClass : public YourClass {
  ...
 public: using YourClass::DoSomethingReturningInt; // changes access rights
  ...
};

TEST_F(YourClassTest, DoSomethingTest) {
  TestableYourClass obj;
  assertEquals(expected_value, obj.DoSomethingReturningInt());
}
```

## How do I test private class static members without writing FRIEND\_TEST()s? ##

We find private static methods clutter the header file.  They are
implementation details and ideally should be kept out of a .h. So often I make
them free functions instead.

Instead of:
``` cpp
// foo.h
class Foo {
  ...
 private:
  static bool Func(int n);
};

// foo.cc
bool Foo::Func(int n) { ... }

// foo_test.cc
EXPECT_TRUE(Foo::Func(12345));
```

You probably should better write:
``` cpp
// foo.h
class Foo {
  ...
};

// foo.cc
namespace internal {
  bool Func(int n) { ... }
}

// foo_test.cc
namespace internal {
  bool Func(int n);
}

EXPECT_TRUE(internal::Func(12345));
```

## I would like to run a test several times with different parameters. Do I need to write several similar copies of it? ##

No. You can use a feature called [value-parameterized tests](AdvancedGuide.md#Value_Parameterized_Tests) which
lets you repeat your tests with different parameters, without defining it more than once.

## How do I test a file that defines main()? ##

To test a `foo.cc` file, you need to compile and link it into your unit test
program. However, when the file contains a definition for the `main()`
function, it will clash with the `main()` of your unit test, and will result in
a build error.

The right solution is to split it into three files:
  1. `foo.h` which contains the declarations,
  1. `foo.cc` which contains the definitions except `main()`, and
  1. `foo_main.cc` which contains nothing but the definition of `main()`.

Then `foo.cc` can be easily tested.

If you are adding tests to an existing file and don't want an intrusive change
like this, there is a hack: just include the entire `foo.cc` file in your unit
test. For example:
``` cpp
// File foo_unittest.cc

// The headers section
...

// Renames main() in foo.cc to make room for the unit test main()
#define main FooMain

#include "a/b/foo.cc"

// The tests start here.
...
```


However, please remember this is a hack and should only be used as the last
resort.

## What can the statement argument in ASSERT\_DEATH() be? ##

`ASSERT_DEATH(_statement_, _regex_)` (or any death assertion macro) can be used
wherever `_statement_` is valid. So basically `_statement_` can be any C++
statement that makes sense in the current context. In particular, it can
reference global and/or local variables, and can be:
  * a simple function call (often the case),
  * a complex expression, or
  * a compound statement.

Some examples are shown here:

``` cpp
// A death test can be a simple function call.
TEST(MyDeathTest, FunctionCall) {
  ASSERT_DEATH(Xyz(5), "Xyz failed");
}

// Or a complex expression that references variables and functions.
TEST(MyDeathTest, ComplexExpression) {
  const bool c = Condition();
  ASSERT_DEATH((c ? Func1(0) : object2.Method("test")),
               "(Func1|Method) failed");
}

// Death assertions can be used any where in a function. In
// particular, they can be inside a loop.
TEST(MyDeathTest, InsideLoop) {
  // Verifies that Foo(0), Foo(1), ..., and Foo(4) all die.
  for (int i = 0; i < 5; i++) {
    EXPECT_DEATH_M(Foo(i), "Foo has \\d+ errors",
                   ::testing::Message() << "where i is " << i);
  }
}

// A death assertion can contain a compound statement.
TEST(MyDeathTest, CompoundStatement) {
  // Verifies that at lease one of Bar(0), Bar(1), ..., and
  // Bar(4) dies.
  ASSERT_DEATH({
    for (int i = 0; i < 5; i++) {
      Bar(i);
    }
  },
  "Bar has \\d+ errors");}
```

`googletest_unittest.cc` contains more examples if you are interested.

## What syntax does the regular expression in ASSERT\_DEATH use? ##

On POSIX systems, Google Test uses the POSIX Extended regular
expression syntax
(http://en.wikipedia.org/wiki/Regular_expression#POSIX_Extended_Regular_Expressions).
On Windows, it uses a limited variant of regular expression
syntax. For more details, see the
[regular expression syntax](AdvancedGuide.md#Regular_Expression_Syntax).

## I have a fixture class Foo, but TEST\_F(Foo, Bar) gives me error "no matching function for call to Foo::Foo()". Why? ##

Google Test needs to be able to create objects of your test fixture class, so
it must have a default constructor. Normally the compiler will define one for
you. However, there are cases where you have to define your own:
  * If you explicitly declare a non-default constructor for class `Foo`, then you need to define a default constructor, even if it would be empty.
  * If `Foo` has a const non-static data member, then you have to define the default constructor _and_ initialize the const member in the initializer list of the constructor. (Early versions of `gcc` doesn't force you to initialize the const member. It's a bug that has been fixed in `gcc 4`.)

## Why does ASSERT\_DEATH complain about previous threads that were already joined? ##

With the Linux pthread library, there is no turning back once you cross the
line from single thread to multiple threads. The first time you create a
thread, a manager thread is created in addition, so you get 3, not 2, threads.
Later when the thread you create joins the main thread, the thread count
decrements by 1, but the manager thread will never be killed, so you still have
2 threads, which means you cannot safely run a death test.

The new NPTL thread library doesn't suffer from this problem, as it doesn't
create a manager thread. However, if you don't control which machine your test
runs on, you shouldn't depend on this.

## Why does Google Test require the entire test case, instead of individual tests, to be named FOODeathTest when it uses ASSERT\_DEATH? ##

Google Test does not interleave tests from different test cases. That is, it
runs all tests in one test case first, and then runs all tests in the next test
case, and so on. Google Test does this because it needs to set up a test case
before the first test in it is run, and tear it down afterwords. Splitting up
the test case would require multiple set-up and tear-down processes, which is
inefficient and makes the semantics unclean.

If we were to determine the order of tests based on test name instead of test
case name, then we would have a problem with the following situation:

``` cpp
TEST_F(FooTest, AbcDeathTest) { ... }
TEST_F(FooTest, Uvw) { ... }

TEST_F(BarTest, DefDeathTest) { ... }
TEST_F(BarTest, Xyz) { ... }
```

Since `FooTest.AbcDeathTest` needs to run before `BarTest.Xyz`, and we don't
interleave tests from different test cases, we need to run all tests in the
`FooTest` case before running any test in the `BarTest` case. This contradicts
with the requirement to run `BarTest.DefDeathTest` before `FooTest.Uvw`.

## But I don't like calling my entire test case FOODeathTest when it contains both death tests and non-death tests. What do I do? ##

You don't have to, but if you like, you may split up the test case into
`FooTest` and `FooDeathTest`, where the names make it clear that they are
related:

``` cpp
class FooTest : public ::testing::Test { ... };

TEST_F(FooTest, Abc) { ... }
TEST_F(FooTest, Def) { ... }

typedef FooTest FooDeathTest;

TEST_F(FooDeathTest, Uvw) { ... EXPECT_DEATH(...) ... }
TEST_F(FooDeathTest, Xyz) { ... ASSERT_DEATH(...) ... }
```

## The compiler complains about "no match for 'operator<<'" when I use an assertion. What gives? ##

If you use a user-defined type `FooType` in an assertion, you must make sure
there is an `std::ostream& operator<<(std::ostream&, const FooType&)` function
defined such that we can print a value of `FooType`.

In addition, if `FooType` is declared in a name space, the `<<` operator also
needs to be defined in the _same_ name space.

## How do I suppress the memory leak messages on Windows? ##

Since the statically initialized Google Test singleton requires allocations on
the heap, the Visual C++ memory leak detector will report memory leaks at the
end of the program run. The easiest way to avoid this is to use the
`_CrtMemCheckpoint` and `_CrtMemDumpAllObjectsSince` calls to not report any
statically initialized heap objects. See MSDN for more details and additional
heap check/debug routines.

## I am building my project with Google Test in Visual Studio and all I'm getting is a bunch of linker errors (or warnings). Help! ##

You may get a number of the following linker error or warnings if you
attempt to link your test project with the Google Test library when
your project and the are not built using the same compiler settings.

  * LNK2005: symbol already defined in object
  * LNK4217: locally defined symbol 'symbol' imported in function 'function'
  * LNK4049: locally defined symbol 'symbol' imported

The Google Test project (gtest.vcproj) has the Runtime Library option
set to /MT (use multi-threaded static libraries, /MTd for debug). If
your project uses something else, for example /MD (use multi-threaded
DLLs, /MDd for debug), you need to change the setting in the Google
Test project to match your project's.

To update this setting open the project properties in the Visual
Studio IDE then select the branch Configuration Properties | C/C++ |
Code Generation and change the option "Runtime Library".  You may also try
using gtest-md.vcproj instead of gtest.vcproj.

## I put my tests in a library and Google Test doesn't run them. What's happening? ##
Have you read a
[warning](Primer.md#important-note-for-visual-c-users) on
the Google Test Primer page?

## I want to use Google Test with Visual Studio but don't know where to start. ##
Many people are in your position and one of them posted his solution to our mailing list.

## I am seeing compile errors mentioning std::type\_traits when I try to use Google Test on Solaris. ##
Google Test uses parts of the standard C++ library that SunStudio does not support.
Our users reported success using alternative implementations. Try running the build after running this command:

`export CC=cc CXX=CC CXXFLAGS='-library=stlport4'`

## How can my code detect if it is running in a test? ##

If you write code that sniffs whether it's running in a test and does
different things accordingly, you are leaking test-only logic into
production code and there is no easy way to ensure that the test-only
code paths aren't run by mistake in production.  Such cleverness also
leads to
[Heisenbugs](http://en.wikipedia.org/wiki/Unusual_software_bug#Heisenbug).
Therefore we strongly advise against the practice, and Google Test doesn't
provide a way to do it.

In general, the recommended way to cause the code to behave
differently under test is [dependency injection](http://jamesshore.com/Blog/Dependency-Injection-Demystified.html).
You can inject different functionality from the test and from the
production code.  Since your production code doesn't link in the
for-test logic at all, there is no danger in accidentally running it.

However, if you _really_, _really_, _really_ have no choice, and if
you follow the rule of ending your test program names with `_test`,
you can use the _horrible_ hack of sniffing your executable name
(`argv[0]` in `main()`) to know whether the code is under test.

## Google Test defines a macro that clashes with one defined by another library. How do I deal with that? ##

In C++, macros don't obey namespaces.  Therefore two libraries that
both define a macro of the same name will clash if you `#include` both
definitions.  In case a Google Test macro clashes with another
library, you can force Google Test to rename its macro to avoid the
conflict.

Specifically, if both Google Test and some other code define macro
`FOO`, you can add
```
  -DGTEST_DONT_DEFINE_FOO=1
```
to the compiler flags to tell Google Test to change the macro's name
from `FOO` to `GTEST_FOO`. For example, with `-DGTEST_DONT_DEFINE_TEST=1`, you'll need to write
``` cpp
  GTEST_TEST(SomeTest, DoesThis) { ... }
```
instead of
``` cpp
  TEST(SomeTest, DoesThis) { ... }
```
in order to define a test.

Currently, the following `TEST`, `FAIL`, `SUCCEED`, and the basic comparison assertion macros can have . You can see the full list of covered macros [here](../include/gtest/gtest.h). More information can be found in the "Avoiding Macro Name Clashes" section of the README file.


## Is it OK if I have two separate `TEST(Foo, Bar)` test methods defined in different namespaces? ##

Yes.

The rule is **all test methods in the same test case must use the same fixture class**. This means that the following is **allowed** because both tests use the same fixture class (`::testing::Test`).

``` cpp
namespace foo {
TEST(CoolTest, DoSomething) {
  SUCCEED();
}
}  // namespace foo

namespace bar {
TEST(CoolTest, DoSomething) {
  SUCCEED();
}
}  // namespace bar
```

However, the following code is **not allowed** and will produce a runtime error from Google Test because the test methods are using different test fixture classes with the same test case name.

``` cpp
namespace foo {
class CoolTest : public ::testing::Test {};  // Fixture foo::CoolTest
TEST_F(CoolTest, DoSomething) {
  SUCCEED();
}
}  // namespace foo

namespace bar {
class CoolTest : public ::testing::Test {};  // Fixture: bar::CoolTest
TEST_F(CoolTest, DoSomething) {
  SUCCEED();
}
}  // namespace bar
```

## How do I build Google Testing Framework with Xcode 4? ##

If you try to build Google Test's Xcode project with Xcode 4.0 or later, you may encounter an error message that looks like
"Missing SDK in target gtest\_framework: /Developer/SDKs/MacOSX10.4u.sdk". That means that Xcode does not support the SDK the project is targeting. See the Xcode section in the [README](../README.md) file on how to resolve this.

## How do I easily discover the flags needed for GoogleTest? ##

GoogleTest (and GoogleMock) now support discovering all necessary flags using pkg-config.
See the [pkg-config guide](Pkgconfig.md) on how you can easily discover all compiler and
linker flags using pkg-config.

## My question is not covered in your FAQ! ##

If you cannot find the answer to your question in this FAQ, there are
some other resources you can use:

  1. read other [wiki pages](../docs),
  1. search the mailing list [archive](https://groups.google.com/forum/#!forum/googletestframework),
  1. ask it on [googletestframework@googlegroups.com](mailto:googletestframework@googlegroups.com) and someone will answer it (to prevent spam, we require you to join the [discussion group](http://groups.google.com/group/googletestframework) before you can post.).

Please note that creating an issue in the
[issue tracker](https://github.com/google/googletest/issues) is _not_
a good way to get your answer, as it is monitored infrequently by a
very small number of people.

When asking a question, it's helpful to provide as much of the
following information as possible (people cannot help you if there's
not enough information in your question):

  * the version (or the commit hash if you check out from Git directly) of Google Test you use (Google Test is under active development, so it's possible that your problem has been solved in a later version),
  * your operating system,
  * the name and version of your compiler,
  * the complete command line flags you give to your compiler,
  * the complete compiler error messages (if the question is about compilation),
  * the _actual_ code (ideally, a minimal but complete program) that has the problem you encounter.
## Using GoogleTest from various build systems ##

GoogleTest comes with pkg-config files that can be used to determine all
necessary flags for compiling and linking to GoogleTest (and GoogleMock).
Pkg-config is a standardised plain-text format containing

  * the includedir (-I) path
  * necessary macro (-D) definitions
  * further required flags (-pthread)
  * the library (-L) path
  * the library (-l) to link to

All current build systems support pkg-config in one way or another. For
all examples here we assume you want to compile the sample
`samples/sample3_unittest.cc`.


### CMake ###

Using `pkg-config` in CMake is fairly easy:

```
cmake_minimum_required(VERSION 3.0)

cmake_policy(SET CMP0048 NEW)
project(my_gtest_pkgconfig VERSION 0.0.1 LANGUAGES CXX)

find_package(PkgConfig)
pkg_search_module(GTEST REQUIRED gtest_main)

add_executable(testapp samples/sample3_unittest.cc)
target_link_libraries(testapp ${GTEST_LDFLAGS})
target_compile_options(testapp PUBLIC ${GTEST_CFLAGS})

include(CTest)
add_test(first_and_only_test testapp)
```

It is generally recommended that you use `target_compile_options` + `_CFLAGS`
over `target_include_directories` + `_INCLUDE_DIRS` as the former includes not
just -I flags (GoogleTest might require a macro indicating to internal headers
that all libraries have been compiled with threading enabled. In addition,
GoogleTest might also require `-pthread` in the compiling step, and as such
splitting the pkg-config `Cflags` variable into include dirs and macros for
`target_compile_definitions()` might still miss this). The same recommendation
goes for using `_LDFLAGS` over the more commonplace `_LIBRARIES`, which
happens to discard `-L` flags and `-pthread`.


### Autotools ###

Finding GoogleTest in Autoconf and using it from Automake is also fairly easy:

In your `configure.ac`:

```
AC_PREREQ([2.69])
AC_INIT([my_gtest_pkgconfig], [0.0.1])
AC_CONFIG_SRCDIR([samples/sample3_unittest.cc])
AC_PROG_CXX

PKG_CHECK_MODULES([GTEST], [gtest_main])

AM_INIT_AUTOMAKE([foreign subdir-objects])
AC_CONFIG_FILES([Makefile])
AC_OUTPUT
```

and in your `Makefile.am`:

```
check_PROGRAMS = testapp
TESTS = $(check_PROGRAMS)

testapp_SOURCES = samples/sample3_unittest.cc
testapp_CXXFLAGS = $(GTEST_CFLAGS)
testapp_LDADD = $(GTEST_LIBS)
```


### Meson ###

Meson natively uses pkgconfig to query dependencies:

```
project('my_gtest_pkgconfig', 'cpp', version : '0.0.1')

gtest_dep = dependency('gtest_main')

testapp = executable(
  'testapp',
  files(['samples/sample3_unittest.cc']),
  dependencies : gtest_dep,
  install : false)

test('first_and_only_test', testapp)
```


### Plain Makefiles ###

Since `pkg-config` is a small Unix command-line utility, it can be used
in handwritten `Makefile`s too:

```
GTEST_CFLAGS = `pkg-config --cflags gtest_main`
GTEST_LIBS = `pkg-config --libs gtest_main`

.PHONY: tests all

tests: all
	./testapp

all: testapp

testapp: testapp.o
	$(CXX) $(CXXFLAGS) $(LDFLAGS) $< -o $@ $(GTEST_LIBS)

testapp.o: samples/sample3_unittest.cc
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) $< -c -o $@ $(GTEST_CFLAGS)
```


### Help! pkg-config can't find GoogleTest! ###

Let's say you have a `CMakeLists.txt` along the lines of the one in this
tutorial and you try to run `cmake`. It is very possible that you get a
failure along the lines of:

```
-- Checking for one of the modules 'gtest_main'
CMake Error at /usr/share/cmake/Modules/FindPkgConfig.cmake:640 (message):
  None of the required 'gtest_main' found
```

These failures are common if you installed GoogleTest yourself and have not
sourced it from a distro or other package manager. If so, you need to tell
pkg-config where it can find the `.pc` files containing the information.
Say you installed GoogleTest to `/usr/local`, then it might be that the
`.pc` files are installed under `/usr/local/lib64/pkgconfig`. If you set

```
export PKG_CONFIG_PATH=/usr/local/lib64/pkgconfig
```

pkg-config will also try to look in `PKG_CONFIG_PATH` to find `gtest_main.pc`.


# Introduction: Why Google C++ Testing Framework? #

_Google C++ Testing Framework_ helps you write better C++ tests.

No matter whether you work on Linux, Windows, or a Mac, if you write C++ code,
Google Test can help you.

So what makes a good test, and how does Google C++ Testing Framework fit in? We believe:
  1. Tests should be _independent_ and _repeatable_. It's a pain to debug a test that succeeds or fails as a result of other tests.  Google C++ Testing Framework isolates the tests by running each of them on a different object. When a test fails, Google C++ Testing Framework allows you to run it in isolation for quick debugging.
  1. Tests should be well _organized_ and reflect the structure of the tested code.  Google C++ Testing Framework groups related tests into test cases that can share data and subroutines. This common pattern is easy to recognize and makes tests easy to maintain. Such consistency is especially helpful when people switch projects and start to work on a new code base.
  1. Tests should be _portable_ and _reusable_. The open-source community has a lot of code that is platform-neutral, its tests should also be platform-neutral.  Google C++ Testing Framework works on different OSes, with different compilers (gcc, MSVC, and others), with or without exceptions, so Google C++ Testing Framework tests can easily work with a variety of configurations.  (Note that the current release only contains build scripts for Linux - we are actively working on scripts for other platforms.)
  1. When tests fail, they should provide as much _information_ about the problem as possible. Google C++ Testing Framework doesn't stop at the first test failure. Instead, it only stops the current test and continues with the next. You can also set up tests that report non-fatal failures after which the current test continues. Thus, you can detect and fix multiple bugs in a single run-edit-compile cycle.
  1. The testing framework should liberate test writers from housekeeping chores and let them focus on the test _content_.  Google C++ Testing Framework automatically keeps track of all tests defined, and doesn't require the user to enumerate them in order to run them.
  1. Tests should be _fast_. With Google C++ Testing Framework, you can reuse shared resources across tests and pay for the set-up/tear-down only once, without making tests depend on each other.

Since Google C++ Testing Framework is based on the popular xUnit
architecture, you'll feel right at home if you've used JUnit or PyUnit before.
If not, it will take you about 10 minutes to learn the basics and get started.
So let's go!

_Note:_ We sometimes refer to Google C++ Testing Framework informally
as _Google Test_.

# Beware of the nomenclature #

_Note:_ There might be some confusion of idea due to different
definitions of the terms _Test_, _Test Case_ and _Test Suite_, so beware
of misunderstanding these.

Historically, the Google C++ Testing Framework started to use the term
_Test Case_ for grouping related tests, whereas current publications
including the International Software Testing Qualifications Board
([ISTQB](http://www.istqb.org/)) and various textbooks on Software
Quality use the term _[Test
Suite](http://glossary.istqb.org/search/test%20suite)_ for this.

The related term _Test_, as it is used in the Google C++ Testing
Framework, is corresponding to the term _[Test
Case](http://glossary.istqb.org/search/test%20case)_ of ISTQB and
others.

The term _Test_ is commonly of broad enough sense, including ISTQB's
definition of _Test Case_, so it's not much of a problem here. But the
term _Test Case_ as used in Google Test is of contradictory sense and thus confusing.

Unfortunately replacing the term _Test Case_ by _Test Suite_ throughout
the Google C++ Testing Framework is not easy without breaking dependent
projects, as `TestCase` is part of the public API at various places.

So for the time being, please be aware of the different definitions of
the terms:

Meaning | Google Test Term | [ISTQB](http://www.istqb.org/) Term
------- | ---------------- | -----------------------------------
Exercise a particular program path with specific input values and verify the results | [TEST()](#simple-tests) | [Test Case](http://glossary.istqb.org/search/test%20case)
A set of several tests related to one component | [Test Case](#basic-concepts) | [Test Suite](http://glossary.istqb.org/search/test%20suite)

# Setting up a New Test Project #

To write a test program using Google Test, you need to compile Google
Test into a library and link your test with it.  We provide build
files for some popular build systems: `msvc/` for Visual Studio,
`xcode/` for Mac Xcode, `make/` for GNU make, `codegear/` for Borland
C++ Builder, and the autotools script (deprecated) and
`CMakeLists.txt` for CMake (recommended) in the Google Test root
directory.  If your build system is not on this list, you can take a
look at `make/Makefile` to learn how Google Test should be compiled
(basically you want to compile `src/gtest-all.cc` with `GTEST_ROOT`
and `GTEST_ROOT/include` in the header search path, where `GTEST_ROOT`
is the Google Test root directory).

Once you are able to compile the Google Test library, you should
create a project or build target for your test program.  Make sure you
have `GTEST_ROOT/include` in the header search path so that the
compiler can find `"gtest/gtest.h"` when compiling your test.  Set up
your test project to link with the Google Test library (for example,
in Visual Studio, this is done by adding a dependency on
`gtest.vcproj`).

If you still have questions, take a look at how Google Test's own
tests are built and use them as examples.

# Basic Concepts #

When using Google Test, you start by writing _assertions_, which are statements
that check whether a condition is true. An assertion's result can be _success_,
_nonfatal failure_, or _fatal failure_. If a fatal failure occurs, it aborts
the current function; otherwise the program continues normally.

_Tests_ use assertions to verify the tested code's behavior. If a test crashes
or has a failed assertion, then it _fails_; otherwise it _succeeds_.

A _test case_ contains one or many tests. You should group your tests into test
cases that reflect the structure of the tested code. When multiple tests in a
test case need to share common objects and subroutines, you can put them into a
_test fixture_ class.

A _test program_ can contain multiple test cases.

We'll now explain how to write a test program, starting at the individual
assertion level and building up to tests and test cases.

# Assertions #

Google Test assertions are macros that resemble function calls. You test a
class or function by making assertions about its behavior. When an assertion
fails, Google Test prints the assertion's source file and line number location,
along with a failure message. You may also supply a custom failure message
which will be appended to Google Test's message.

The assertions come in pairs that test the same thing but have different
effects on the current function. `ASSERT_*` versions generate fatal failures
when they fail, and **abort the current function**. `EXPECT_*` versions generate
nonfatal failures, which don't abort the current function. Usually `EXPECT_*`
are preferred, as they allow more than one failures to be reported in a test.
However, you should use `ASSERT_*` if it doesn't make sense to continue when
the assertion in question fails.

Since a failed `ASSERT_*` returns from the current function immediately,
possibly skipping clean-up code that comes after it, it may cause a space leak.
Depending on the nature of the leak, it may or may not be worth fixing - so
keep this in mind if you get a heap checker error in addition to assertion
errors.

To provide a custom failure message, simply stream it into the macro using the
`<<` operator, or a sequence of such operators. An example:
```
ASSERT_EQ(x.size(), y.size()) << "Vectors x and y are of unequal length";

for (int i = 0; i < x.size(); ++i) {
  EXPECT_EQ(x[i], y[i]) << "Vectors x and y differ at index " << i;
}
```

Anything that can be streamed to an `ostream` can be streamed to an assertion
macro--in particular, C strings and `string` objects. If a wide string
(`wchar_t*`, `TCHAR*` in `UNICODE` mode on Windows, or `std::wstring`) is
streamed to an assertion, it will be translated to UTF-8 when printed.

## Basic Assertions ##

These assertions do basic true/false condition testing.

| **Fatal assertion** | **Nonfatal assertion** | **Verifies** |
|:--------------------|:-----------------------|:-------------|
| `ASSERT_TRUE(`_condition_`)`;  | `EXPECT_TRUE(`_condition_`)`;   | _condition_ is true |
| `ASSERT_FALSE(`_condition_`)`; | `EXPECT_FALSE(`_condition_`)`;  | _condition_ is false |

Remember, when they fail, `ASSERT_*` yields a fatal failure and
returns from the current function, while `EXPECT_*` yields a nonfatal
failure, allowing the function to continue running. In either case, an
assertion failure means its containing test fails.

_Availability_: Linux, Windows, Mac.

## Binary Comparison ##

This section describes assertions that compare two values.

| **Fatal assertion** | **Nonfatal assertion** | **Verifies** |
|:--------------------|:-----------------------|:-------------|
|`ASSERT_EQ(`_val1_`, `_val2_`);`|`EXPECT_EQ(`_val1_`, `_val2_`);`| _val1_ `==` _val2_ |
|`ASSERT_NE(`_val1_`, `_val2_`);`|`EXPECT_NE(`_val1_`, `_val2_`);`| _val1_ `!=` _val2_ |
|`ASSERT_LT(`_val1_`, `_val2_`);`|`EXPECT_LT(`_val1_`, `_val2_`);`| _val1_ `<` _val2_ |
|`ASSERT_LE(`_val1_`, `_val2_`);`|`EXPECT_LE(`_val1_`, `_val2_`);`| _val1_ `<=` _val2_ |
|`ASSERT_GT(`_val1_`, `_val2_`);`|`EXPECT_GT(`_val1_`, `_val2_`);`| _val1_ `>` _val2_ |
|`ASSERT_GE(`_val1_`, `_val2_`);`|`EXPECT_GE(`_val1_`, `_val2_`);`| _val1_ `>=` _val2_ |

In the event of a failure, Google Test prints both _val1_ and _val2_.

Value arguments must be comparable by the assertion's comparison
operator or you'll get a compiler error.  We used to require the
arguments to support the `<<` operator for streaming to an `ostream`,
but it's no longer necessary since v1.6.0 (if `<<` is supported, it
will be called to print the arguments when the assertion fails;
otherwise Google Test will attempt to print them in the best way it
can. For more details and how to customize the printing of the
arguments, see this Google Mock [recipe](../../googlemock/docs/CookBook.md#teaching-google-mock-how-to-print-your-values).).

These assertions can work with a user-defined type, but only if you define the
corresponding comparison operator (e.g. `==`, `<`, etc).  If the corresponding
operator is defined, prefer using the `ASSERT_*()` macros because they will
print out not only the result of the comparison, but the two operands as well.

Arguments are always evaluated exactly once. Therefore, it's OK for the
arguments to have side effects. However, as with any ordinary C/C++ function,
the arguments' evaluation order is undefined (i.e. the compiler is free to
choose any order) and your code should not depend on any particular argument
evaluation order.

`ASSERT_EQ()` does pointer equality on pointers. If used on two C strings, it
tests if they are in the same memory location, not if they have the same value.
Therefore, if you want to compare C strings (e.g. `const char*`) by value, use
`ASSERT_STREQ()` , which will be described later on. In particular, to assert
that a C string is `NULL`, use `ASSERT_STREQ(NULL, c_string)` . However, to
compare two `string` objects, you should use `ASSERT_EQ`.

Macros in this section work with both narrow and wide string objects (`string`
and `wstring`).

_Availability_: Linux, Windows, Mac.

_Historical note_: Before February 2016 `*_EQ` had a convention of calling it as
`ASSERT_EQ(expected, actual)`, so lots of existing code uses this order.
Now `*_EQ` treats both parameters in the same way.

## String Comparison ##

The assertions in this group compare two **C strings**. If you want to compare
two `string` objects, use `EXPECT_EQ`, `EXPECT_NE`, and etc instead.

| **Fatal assertion** | **Nonfatal assertion** | **Verifies** |
|:--------------------|:-----------------------|:-------------|
| `ASSERT_STREQ(`_str1_`, `_str2_`);`    | `EXPECT_STREQ(`_str1_`, `_str2_`);`     | the two C strings have the same content |
| `ASSERT_STRNE(`_str1_`, `_str2_`);`    | `EXPECT_STRNE(`_str1_`, `_str2_`);`     | the two C strings have different content |
| `ASSERT_STRCASEEQ(`_str1_`, `_str2_`);`| `EXPECT_STRCASEEQ(`_str1_`, `_str2_`);` | the two C strings have the same content, ignoring case |
| `ASSERT_STRCASENE(`_str1_`, `_str2_`);`| `EXPECT_STRCASENE(`_str1_`, `_str2_`);` | the two C strings have different content, ignoring case |

Note that "CASE" in an assertion name means that case is ignored.

`*STREQ*` and `*STRNE*` also accept wide C strings (`wchar_t*`). If a
comparison of two wide strings fails, their values will be printed as UTF-8
narrow strings.

A `NULL` pointer and an empty string are considered _different_.

_Availability_: Linux, Windows, Mac.

See also: For more string comparison tricks (substring, prefix, suffix, and
regular expression matching, for example), see the [Advanced Google Test Guide](AdvancedGuide.md).

# Simple Tests #

To create a test:
  1. Use the `TEST()` macro to define and name a test function, These are ordinary C++ functions that don't return a value.
  1. In this function, along with any valid C++ statements you want to include, use the various Google Test assertions to check values.
  1. The test's result is determined by the assertions; if any assertion in the test fails (either fatally or non-fatally), or if the test crashes, the entire test fails. Otherwise, it succeeds.

```
TEST(test_case_name, test_name) {
 ... test body ...
}
```


`TEST()` arguments go from general to specific. The _first_ argument is the
name of the test case, and the _second_ argument is the test's name within the
test case. Both names must be valid C++ identifiers, and they should not contain underscore (`_`). A test's _full name_ consists of its containing test case and its
individual name. Tests from different test cases can have the same individual
name.

For example, let's take a simple integer function:
```
int Factorial(int n); // Returns the factorial of n
```

A test case for this function might look like:
```
// Tests factorial of 0.
TEST(FactorialTest, HandlesZeroInput) {
  EXPECT_EQ(1, Factorial(0));
}

// Tests factorial of positive numbers.
TEST(FactorialTest, HandlesPositiveInput) {
  EXPECT_EQ(1, Factorial(1));
  EXPECT_EQ(2, Factorial(2));
  EXPECT_EQ(6, Factorial(3));
  EXPECT_EQ(40320, Factorial(8));
}
```

Google Test groups the test results by test cases, so logically-related tests
should be in the same test case; in other words, the first argument to their
`TEST()` should be the same. In the above example, we have two tests,
`HandlesZeroInput` and `HandlesPositiveInput`, that belong to the same test
case `FactorialTest`.

_Availability_: Linux, Windows, Mac.

# Test Fixtures: Using the Same Data Configuration for Multiple Tests #

If you find yourself writing two or more tests that operate on similar data,
you can use a _test fixture_. It allows you to reuse the same configuration of
objects for several different tests.

To create a fixture, just:
  1. Derive a class from `::testing::Test` . Start its body with `protected:` or `public:` as we'll want to access fixture members from sub-classes.
  1. Inside the class, declare any objects you plan to use.
  1. If necessary, write a default constructor or `SetUp()` function to prepare the objects for each test. A common mistake is to spell `SetUp()` as `Setup()` with a small `u` - don't let that happen to you.
  1. If necessary, write a destructor or `TearDown()` function to release any resources you allocated in `SetUp()` . To learn when you should use the constructor/destructor and when you should use `SetUp()/TearDown()`, read this [FAQ entry](FAQ.md#should-i-use-the-constructordestructor-of-the-test-fixture-or-the-set-uptear-down-function).
  1. If needed, define subroutines for your tests to share.

When using a fixture, use `TEST_F()` instead of `TEST()` as it allows you to
access objects and subroutines in the test fixture:
```
TEST_F(test_case_name, test_name) {
 ... test body ...
}
```

Like `TEST()`, the first argument is the test case name, but for `TEST_F()`
this must be the name of the test fixture class. You've probably guessed: `_F`
is for fixture.

Unfortunately, the C++ macro system does not allow us to create a single macro
that can handle both types of tests. Using the wrong macro causes a compiler
error.

Also, you must first define a test fixture class before using it in a
`TEST_F()`, or you'll get the compiler error "`virtual outside class
declaration`".

For each test defined with `TEST_F()`, Google Test will:
  1. Create a _fresh_ test fixture at runtime
  1. Immediately initialize it via `SetUp()`
  1. Run the test
  1. Clean up by calling `TearDown()`
  1. Delete the test fixture.  Note that different tests in the same test case have different test fixture objects, and Google Test always deletes a test fixture before it creates the next one. Google Test does not reuse the same test fixture for multiple tests. Any changes one test makes to the fixture do not affect other tests.

As an example, let's write tests for a FIFO queue class named `Queue`, which
has the following interface:
```
template <typename E> // E is the element type.
class Queue {
 public:
  Queue();
  void Enqueue(const E& element);
  E* Dequeue(); // Returns NULL if the queue is empty.
  size_t size() const;
  ...
};
```

First, define a fixture class. By convention, you should give it the name
`FooTest` where `Foo` is the class being tested.
```
class QueueTest : public ::testing::Test {
 protected:
  virtual void SetUp() {
    q1_.Enqueue(1);
    q2_.Enqueue(2);
    q2_.Enqueue(3);
  }

  // virtual void TearDown() {}

  Queue<int> q0_;
  Queue<int> q1_;
  Queue<int> q2_;
};
```

In this case, `TearDown()` is not needed since we don't have to clean up after
each test, other than what's already done by the destructor.

Now we'll write tests using `TEST_F()` and this fixture.
```
TEST_F(QueueTest, IsEmptyInitially) {
  EXPECT_EQ(0, q0_.size());
}

TEST_F(QueueTest, DequeueWorks) {
  int* n = q0_.Dequeue();
  EXPECT_EQ(NULL, n);

  n = q1_.Dequeue();
  ASSERT_TRUE(n != NULL);
  EXPECT_EQ(1, *n);
  EXPECT_EQ(0, q1_.size());
  delete n;

  n = q2_.Dequeue();
  ASSERT_TRUE(n != NULL);
  EXPECT_EQ(2, *n);
  EXPECT_EQ(1, q2_.size());
  delete n;
}
```

The above uses both `ASSERT_*` and `EXPECT_*` assertions. The rule of thumb is
to use `EXPECT_*` when you want the test to continue to reveal more errors
after the assertion failure, and use `ASSERT_*` when continuing after failure
doesn't make sense. For example, the second assertion in the `Dequeue` test is
`ASSERT_TRUE(n != NULL)`, as we need to dereference the pointer `n` later,
which would lead to a segfault when `n` is `NULL`.

When these tests run, the following happens:
  1. Google Test constructs a `QueueTest` object (let's call it `t1` ).
  1. `t1.SetUp()` initializes `t1` .
  1. The first test ( `IsEmptyInitially` ) runs on `t1` .
  1. `t1.TearDown()` cleans up after the test finishes.
  1. `t1` is destructed.
  1. The above steps are repeated on another `QueueTest` object, this time running the `DequeueWorks` test.

_Availability_: Linux, Windows, Mac.

_Note_: Google Test automatically saves all _Google Test_ flags when a test
object is constructed, and restores them when it is destructed.

# Invoking the Tests #

`TEST()` and `TEST_F()` implicitly register their tests with Google Test. So, unlike with many other C++ testing frameworks, you don't have to re-list all your defined tests in order to run them.

After defining your tests, you can run them with `RUN_ALL_TESTS()` , which returns `0` if all the tests are successful, or `1` otherwise. Note that `RUN_ALL_TESTS()` runs _all tests_ in your link unit -- they can be from different test cases, or even different source files.

When invoked, the `RUN_ALL_TESTS()` macro:
  1. Saves the state of all  Google Test flags.
  1. Creates a test fixture object for the first test.
  1. Initializes it via `SetUp()`.
  1. Runs the test on the fixture object.
  1. Cleans up the fixture via `TearDown()`.
  1. Deletes the fixture.
  1. Restores the state of all Google Test flags.
  1. Repeats the above steps for the next test, until all tests have run.

In addition, if the test fixture's constructor generates a fatal failure in
step 2, there is no point for step 3 - 5 and they are thus skipped. Similarly,
if step 3 generates a fatal failure, step 4 will be skipped.

_Important_: You must not ignore the return value of `RUN_ALL_TESTS()`, or `gcc`
will give you a compiler error. The rationale for this design is that the
automated testing service determines whether a test has passed based on its
exit code, not on its stdout/stderr output; thus your `main()` function must
return the value of `RUN_ALL_TESTS()`.

Also, you should call `RUN_ALL_TESTS()` only **once**. Calling it more than once
conflicts with some advanced Google Test features (e.g. thread-safe death
tests) and thus is not supported.

_Availability_: Linux, Windows, Mac.

# Writing the main() Function #

You can start from this boilerplate:
```
#include "this/package/foo.h"
#include "gtest/gtest.h"

namespace {

// The fixture for testing class Foo.
class FooTest : public ::testing::Test {
 protected:
  // You can remove any or all of the following functions if its body
  // is empty.

  FooTest() {
    // You can do set-up work for each test here.
  }

  virtual ~FooTest() {
    // You can do clean-up work that doesn't throw exceptions here.
  }

  // If the constructor and destructor are not enough for setting up
  // and cleaning up each test, you can define the following methods:

  virtual void SetUp() {
    // Code here will be called immediately after the constructor (right
    // before each test).
  }

  virtual void TearDown() {
    // Code here will be called immediately after each test (right
    // before the destructor).
  }

  // Objects declared here can be used by all tests in the test case for Foo.
};

// Tests that the Foo::Bar() method does Abc.
TEST_F(FooTest, MethodBarDoesAbc) {
  const string input_filepath = "this/package/testdata/myinputfile.dat";
  const string output_filepath = "this/package/testdata/myoutputfile.dat";
  Foo f;
  EXPECT_EQ(0, f.Bar(input_filepath, output_filepath));
}

// Tests that Foo does Xyz.
TEST_F(FooTest, DoesXyz) {
  // Exercises the Xyz feature of Foo.
}

}  // namespace

int main(int argc, char **argv) {
  ::testing::InitGoogleTest(&argc, argv);
  return RUN_ALL_TESTS();
}
```

The `::testing::InitGoogleTest()` function parses the command line for Google
Test flags, and removes all recognized flags. This allows the user to control a
test program's behavior via various flags, which we'll cover in [AdvancedGuide](AdvancedGuide.md).
You must call this function before calling `RUN_ALL_TESTS()`, or the flags
won't be properly initialized.

On Windows, `InitGoogleTest()` also works with wide strings, so it can be used
in programs compiled in `UNICODE` mode as well.

But maybe you think that writing all those main() functions is too much work? We agree with you completely and that's why Google Test provides a basic implementation of main(). If it fits your needs, then just link your test with gtest\_main library and you are good to go.

## Important note for Visual C++ users ##
If you put your tests into a library and your `main()` function is in a different library or in your .exe file, those tests will not run. The reason is a [bug](https://connect.microsoft.com/feedback/viewfeedback.aspx?FeedbackID=244410&siteid=210) in Visual C++. When you define your tests, Google Test creates certain static objects to register them. These objects are not referenced from elsewhere but their constructors are still supposed to run. When Visual C++ linker sees that nothing in the library is referenced from other places it throws the library out. You have to reference your library with tests from your main program to keep the linker from discarding it. Here is how to do it. Somewhere in your library code declare a function:
```
__declspec(dllexport) int PullInMyLibrary() { return 0; }
```
If you put your tests in a static library (not DLL) then `__declspec(dllexport)` is not required. Now, in your main program, write a code that invokes that function:
```
int PullInMyLibrary();
static int dummy = PullInMyLibrary();
```
This will keep your tests referenced and will make them register themselves at startup.

In addition, if you define your tests in a static library, add `/OPT:NOREF` to your main program linker options. If you use MSVC++ IDE, go to your .exe project properties/Configuration Properties/Linker/Optimization and set References setting to `Keep Unreferenced Data (/OPT:NOREF)`. This will keep Visual C++ linker from discarding individual symbols generated by your tests from the final executable.

There is one more pitfall, though. If you use Google Test as a static library (that's how it is defined in gtest.vcproj) your tests must also reside in a static library. If you have to have them in a DLL, you _must_ change Google Test to build into a DLL as well. Otherwise your tests will not run correctly or will not run at all. The general conclusion here is: make your life easier - do not write your tests in libraries!

# Where to Go from Here #

Congratulations! You've learned the Google Test basics. You can start writing
and running Google Test tests, read some [samples](Samples.md), or continue with
[AdvancedGuide](AdvancedGuide.md), which describes many more useful Google Test features.

# Known Limitations #

Google Test is designed to be thread-safe.  The implementation is
thread-safe on systems where the `pthreads` library is available.  It
is currently _unsafe_ to use Google Test assertions from two threads
concurrently on other systems (e.g. Windows).  In most tests this is
not an issue as usually the assertions are done in the main thread. If
you want to help, you can volunteer to implement the necessary
synchronization primitives in `gtest-port.h` for your platform.


<b>P</b>ump is <b>U</b>seful for <b>M</b>eta <b>P</b>rogramming.

# The Problem #

Template and macro libraries often need to define many classes,
functions, or macros that vary only (or almost only) in the number of
arguments they take. It's a lot of repetitive, mechanical, and
error-prone work.

Variadic templates and variadic macros can alleviate the problem.
However, while both are being considered by the C++ committee, neither
is in the standard yet or widely supported by compilers.  Thus they
are often not a good choice, especially when your code needs to be
portable. And their capabilities are still limited.

As a result, authors of such libraries often have to write scripts to
generate their implementation. However, our experience is that it's
tedious to write such scripts, which tend to reflect the structure of
the generated code poorly and are often hard to read and edit. For
example, a small change needed in the generated code may require some
non-intuitive, non-trivial changes in the script. This is especially
painful when experimenting with the code.

# Our Solution #

Pump (for Pump is Useful for Meta Programming, Pretty Useful for Meta
Programming, or Practical Utility for Meta Programming, whichever you
prefer) is a simple meta-programming tool for C++. The idea is that a
programmer writes a `foo.pump` file which contains C++ code plus meta
code that manipulates the C++ code. The meta code can handle
iterations over a range, nested iterations, local meta variable
definitions, simple arithmetic, and conditional expressions. You can
view it as a small Domain-Specific Language. The meta language is
designed to be non-intrusive (s.t. it won't confuse Emacs' C++ mode,
for example) and concise, making Pump code intuitive and easy to
maintain.

## Highlights ##

  * The implementation is in a single Python script and thus ultra portable: no build or installation is needed and it works cross platforms.
  * Pump tries to be smart with respect to [Google's style guide](https://github.com/google/styleguide): it breaks long lines (easy to have when they are generated) at acceptable places to fit within 80 columns and indent the continuation lines correctly.
  * The format is human-readable and more concise than XML.
  * The format works relatively well with Emacs' C++ mode.

## Examples ##

The following Pump code (where meta keywords start with `$`, `[[` and `]]` are meta brackets, and `$$` starts a meta comment that ends with the line):

```
$var n = 3     $$ Defines a meta variable n.
$range i 0..n  $$ Declares the range of meta iterator i (inclusive).
$for i [[
               $$ Meta loop.
// Foo$i does blah for $i-ary predicates.
$range j 1..i
template <size_t N $for j [[, typename A$j]]>
class Foo$i {
$if i == 0 [[
  blah a;
]] $elif i <= 2 [[
  blah b;
]] $else [[
  blah c;
]]
};

]]
```

will be translated by the Pump compiler to:

```
// Foo0 does blah for 0-ary predicates.
template <size_t N>
class Foo0 {
  blah a;
};

// Foo1 does blah for 1-ary predicates.
template <size_t N, typename A1>
class Foo1 {
  blah b;
};

// Foo2 does blah for 2-ary predicates.
template <size_t N, typename A1, typename A2>
class Foo2 {
  blah b;
};

// Foo3 does blah for 3-ary predicates.
template <size_t N, typename A1, typename A2, typename A3>
class Foo3 {
  blah c;
};
```

In another example,

```
$range i 1..n
Func($for i + [[a$i]]);
$$ The text between i and [[ is the separator between iterations.
```

will generate one of the following lines (without the comments), depending on the value of `n`:

```
Func();              // If n is 0.
Func(a1);            // If n is 1.
Func(a1 + a2);       // If n is 2.
Func(a1 + a2 + a3);  // If n is 3.
// And so on...
```

## Constructs ##

We support the following meta programming constructs:

| `$var id = exp` | Defines a named constant value. `$id` is valid util the end of the current meta lexical block. |
|:----------------|:-----------------------------------------------------------------------------------------------|
| `$range id exp..exp` | Sets the range of an iteration variable, which can be reused in multiple loops later.          |
| `$for id sep [[ code ]]` | Iteration. The range of `id` must have been defined earlier. `$id` is valid in `code`.         |
| `$($)`          | Generates a single `$` character.                                                              |
| `$id`           | Value of the named constant or iteration variable.                                             |
| `$(exp)`        | Value of the expression.                                                                       |
| `$if exp [[ code ]] else_branch` | Conditional.                                                                                   |
| `[[ code ]]`    | Meta lexical block.                                                                            |
| `cpp_code`      | Raw C++ code.                                                                                  |
| `$$ comment`    | Meta comment.                                                                                  |

**Note:** To give the user some freedom in formatting the Pump source
code, Pump ignores a new-line character if it's right after `$for foo`
or next to `[[` or `]]`. Without this rule you'll often be forced to write
very long lines to get the desired output. Therefore sometimes you may
need to insert an extra new-line in such places for a new-line to show
up in your output.

## Grammar ##

```
code ::= atomic_code*
atomic_code ::= $var id = exp
    | $var id = [[ code ]]
    | $range id exp..exp
    | $for id sep [[ code ]]
    | $($)
    | $id
    | $(exp)
    | $if exp [[ code ]] else_branch
    | [[ code ]]
    | cpp_code
sep ::= cpp_code | empty_string
else_branch ::= $else [[ code ]]
    | $elif exp [[ code ]] else_branch
    | empty_string
exp ::= simple_expression_in_Python_syntax
```

## Code ##

You can find the source code of Pump in [scripts/pump.py](../scripts/pump.py). It is still
very unpolished and lacks automated tests, although it has been
successfully used many times. If you find a chance to use it in your
project, please let us know what you think!  We also welcome help on
improving Pump.

## Real Examples ##

You can find real-world applications of Pump in [Google Test](https://github.com/google/googletest/tree/master/googletest) and [Google Mock](https://github.com/google/googletest/tree/master/googlemock). The source file `foo.h.pump` generates `foo.h`.

## Tips ##

  * If a meta variable is followed by a letter or digit, you can separate them using `[[]]`, which inserts an empty string. For example `Foo$j[[]]Helper` generate `Foo1Helper` when `j` is 1.
  * To avoid extra-long Pump source lines, you can break a line anywhere you want by inserting `[[]]` followed by a new line. Since any new-line character next to `[[` or `]]` is ignored, the generated code won't contain this new line.
If you're like us, you'd like to look at some Google Test sample code.  The
[samples folder](../samples) has a number of well-commented samples showing how to use a
variety of Google Test features.

  * [Sample #1](../samples/sample1_unittest.cc) shows the basic steps of using Google Test to test C++ functions.
  * [Sample #2](../samples/sample2_unittest.cc) shows a more complex unit test for a class with multiple member functions.
  * [Sample #3](../samples/sample3_unittest.cc) uses a test fixture.
  * [Sample #4](../samples/sample4_unittest.cc) is another basic example of using Google Test.
  * [Sample #5](../samples/sample5_unittest.cc) teaches how to reuse a test fixture in multiple test cases by deriving sub-fixtures from it.
  * [Sample #6](../samples/sample6_unittest.cc) demonstrates type-parameterized tests.
  * [Sample #7](../samples/sample7_unittest.cc) teaches the basics of value-parameterized tests.
  * [Sample #8](../samples/sample8_unittest.cc) shows using `Combine()` in value-parameterized tests.
  * [Sample #9](../samples/sample9_unittest.cc) shows use of the listener API to modify Google Test's console output and the use of its reflection API to inspect test results.
  * [Sample #10](../samples/sample10_unittest.cc) shows use of the listener API to implement a primitive memory leak checker.


This guide will explain how to use the Google Testing Framework in your Xcode projects on Mac OS X. This tutorial begins by quickly explaining what to do for experienced users. After the quick start, the guide goes provides additional explanation about each step.

# Quick Start #

Here is the quick guide for using Google Test in your Xcode project.

  1. Download the source from the [website](http://code.google.com/p/googletest) using this command: `svn checkout http://googletest.googlecode.com/svn/trunk/ googletest-read-only`.
  1. Open up the `gtest.xcodeproj` in the `googletest-read-only/xcode/` directory and build the gtest.framework.
  1. Create a new "Shell Tool" target in your Xcode project called something like "UnitTests".
  1. Add the gtest.framework to your project and add it to the "Link Binary with Libraries" build phase of "UnitTests".
  1. Add your unit test source code to the "Compile Sources" build phase of "UnitTests".
  1. Edit the "UnitTests" executable and add an environment variable named "DYLD\_FRAMEWORK\_PATH" with a value equal to the path to the framework containing the gtest.framework relative to the compiled executable.
  1. Build and Go.

The following sections further explain each of the steps listed above in depth, describing in more detail how to complete it including some variations.

# Get the Source #

Currently, the gtest.framework discussed here isn't available in a tagged release of Google Test, it is only available in the trunk. As explained at the Google Test [site](http://code.google.com/p/googletest/source/checkout">svn), you can get the code from anonymous SVN with this command:

```
svn checkout http://googletest.googlecode.com/svn/trunk/ googletest-read-only
```

Alternatively, if you are working with Subversion in your own code base, you can add Google Test as an external dependency to your own Subversion repository. By following this approach, everyone that checks out your svn repository will also receive a copy of Google Test (a specific version, if you wish) without having to check it out explicitly. This makes the set up of your project simpler and reduces the copied code in the repository.

To use `svn:externals`, decide where you would like to have the external source reside. You might choose to put the external source inside the trunk, because you want it to be part of the branch when you make a release. However, keeping it outside the trunk in a version-tagged directory called something like `third-party/googletest/1.0.1`, is another option. Once the location is established, use `svn propedit svn:externals _directory_` to set the svn:externals property on a directory in your repository. This directory won't contain the code, but be its versioned parent directory.

The command `svn propedit` will bring up your Subversion editor, making editing the long, (potentially multi-line) property simpler. This same method can be used to check out a tagged branch, by using the appropriate URL (e.g. `http://googletest.googlecode.com/svn/tags/release-1.0.1`). Additionally, the svn:externals property allows the specification of a particular revision of the trunk with the `-r_##_` option (e.g. `externals/src/googletest -r60 http://googletest.googlecode.com/svn/trunk`).

Here is an example of using the svn:externals properties on a trunk (read via `svn propget`) of a project. This value checks out a copy of Google Test into the `trunk/externals/src/googletest/` directory.

```
[Computer:svn] user$ svn propget svn:externals trunk
externals/src/googletest http://googletest.googlecode.com/svn/trunk
```

# Add the Framework to Your Project #

The next step is to build and add the gtest.framework to your own project. This guide describes two common ways below.

  * **Option 1** --- The simplest way to add Google Test to your own project, is to open gtest.xcodeproj (found in the xcode/ directory of the Google Test trunk) and build the framework manually. Then, add the built framework into your project using the "Add->Existing Framework..." from the context menu or "Project->Add..." from the main menu. The gtest.framework is relocatable and contains the headers and object code that you'll need to make tests. This method requires rebuilding every time you upgrade Google Test in your project.
  * **Option 2** --- If you are going to be living off the trunk of Google Test, incorporating its latest features into your unit tests (or are a Google Test developer yourself). You'll want to rebuild the framework every time the source updates. to do this, you'll need to add the gtest.xcodeproj file, not the framework itself, to your own Xcode project. Then, from the build products that are revealed by the project's disclosure triangle, you can find the gtest.framework, which can be added to your targets (discussed below).

# Make a Test Target #

To start writing tests, make a new "Shell Tool" target. This target template is available under BSD, Cocoa, or Carbon. Add your unit test source code to the "Compile Sources" build phase of the target.

Next, you'll want to add gtest.framework in two different ways, depending upon which option you chose above.

  * **Option 1** --- During compilation, Xcode will need to know that you are linking against the gtest.framework. Add the gtest.framework to the "Link Binary with Libraries" build phase of your test target. This will include the Google Test headers in your header search path, and will tell the linker where to find the library.
  * **Option 2** --- If your working out of the trunk, you'll also want to add gtest.framework to your "Link Binary with Libraries" build phase of your test target. In addition, you'll  want to add the gtest.framework as a dependency to your unit test target. This way, Xcode will make sure that gtest.framework is up to date, every time your build your target. Finally, if you don't share build directories with Google Test, you'll have to copy the gtest.framework into your own build products directory using a "Run Script" build phase.

# Set Up the Executable Run Environment #

Since the unit test executable is a shell tool, it doesn't have a bundle with a `Contents/Frameworks` directory, in which to place gtest.framework. Instead, the dynamic linker must be told at runtime to search for the framework in another location. This can be accomplished by setting the "DYLD\_FRAMEWORK\_PATH" environment variable in the "Edit Active Executable ..." Arguments tab, under "Variables to be set in the environment:". The path for this value is the path (relative or absolute) of the directory containing the gtest.framework.

If you haven't set up the DYLD\_FRAMEWORK\_PATH, correctly, you might get a message like this:

```
[Session started at 2008-08-15 06:23:57 -0600.]
  dyld: Library not loaded: @loader_path/../Frameworks/gtest.framework/Versions/A/gtest
    Referenced from: /Users/username/Documents/Sandbox/gtestSample/build/Debug/WidgetFrameworkTest
    Reason: image not found
```

To correct this problem, go to to the directory containing the executable named in "Referenced from:" value in the error message above. Then, with the terminal in this location, find the relative path to the directory containing the gtest.framework. That is the value you'll need to set as the DYLD\_FRAMEWORK\_PATH.

# Build and Go #

Now, when you click "Build and Go", the test will be executed. Dumping out something like this:

```
[Session started at 2008-08-06 06:36:13 -0600.]
[==========] Running 2 tests from 1 test case.
[----------] Global test environment set-up.
[----------] 2 tests from WidgetInitializerTest
[ RUN      ] WidgetInitializerTest.TestConstructor
[       OK ] WidgetInitializerTest.TestConstructor
[ RUN      ] WidgetInitializerTest.TestConversion
[       OK ] WidgetInitializerTest.TestConversion
[----------] Global test environment tear-down
[==========] 2 tests from 1 test case ran.
[  PASSED  ] 2 tests.

The Debugger has exited with status 0.  
```

# Summary #

Unit testing is a valuable way to ensure your data model stays valid even during rapid development or refactoring. The Google Testing Framework is a great unit testing framework for C and C++ which integrates well with an Xcode development environment.The non-test part of the code is expected to have 2 failures.

gtest_output_test_.cc:#: Failure
Value of: false
  Actual: false
Expected: true
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  2
  3
[0;32m[==========] [mRunning 66 tests from 29 test cases.
[0;32m[----------] [mGlobal test environment set-up.
FooEnvironment::SetUp() called.
BarEnvironment::SetUp() called.
[0;32m[----------] [m1 test from ADeathTest
[0;32m[ RUN      ] [mADeathTest.ShouldRunFirst
[0;32m[       OK ] [mADeathTest.ShouldRunFirst
[0;32m[----------] [m1 test from ATypedDeathTest/0, where TypeParam = int
[0;32m[ RUN      ] [mATypedDeathTest/0.ShouldRunFirst
[0;32m[       OK ] [mATypedDeathTest/0.ShouldRunFirst
[0;32m[----------] [m1 test from ATypedDeathTest/1, where TypeParam = double
[0;32m[ RUN      ] [mATypedDeathTest/1.ShouldRunFirst
[0;32m[       OK ] [mATypedDeathTest/1.ShouldRunFirst
[0;32m[----------] [m1 test from My/ATypeParamDeathTest/0, where TypeParam = int
[0;32m[ RUN      ] [mMy/ATypeParamDeathTest/0.ShouldRunFirst
[0;32m[       OK ] [mMy/ATypeParamDeathTest/0.ShouldRunFirst
[0;32m[----------] [m1 test from My/ATypeParamDeathTest/1, where TypeParam = double
[0;32m[ RUN      ] [mMy/ATypeParamDeathTest/1.ShouldRunFirst
[0;32m[       OK ] [mMy/ATypeParamDeathTest/1.ShouldRunFirst
[0;32m[----------] [m2 tests from PassingTest
[0;32m[ RUN      ] [mPassingTest.PassingTest1
[0;32m[       OK ] [mPassingTest.PassingTest1
[0;32m[ RUN      ] [mPassingTest.PassingTest2
[0;32m[       OK ] [mPassingTest.PassingTest2
[0;32m[----------] [m2 tests from NonfatalFailureTest
[0;32m[ RUN      ] [mNonfatalFailureTest.EscapesStringOperands
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  kGoldenString
    Which is: "\"Line"
  actual
    Which is: "actual \"string\""
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  golden
    Which is: "\"Line"
  actual
    Which is: "actual \"string\""
[0;31m[  FAILED  ] [mNonfatalFailureTest.EscapesStringOperands
[0;32m[ RUN      ] [mNonfatalFailureTest.DiffForLongStrings
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  golden_str
    Which is: "\"Line\0 1\"\nLine 2"
  "Line 2"
With diff:
@@ -1,2 @@
-\"Line\0 1\"
 Line 2

[0;31m[  FAILED  ] [mNonfatalFailureTest.DiffForLongStrings
[0;32m[----------] [m3 tests from FatalFailureTest
[0;32m[ RUN      ] [mFatalFailureTest.FatalFailureInSubroutine
(expecting a failure that x should be 1)
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  1
  x
    Which is: 2
[0;31m[  FAILED  ] [mFatalFailureTest.FatalFailureInSubroutine
[0;32m[ RUN      ] [mFatalFailureTest.FatalFailureInNestedSubroutine
(expecting a failure that x should be 1)
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  1
  x
    Which is: 2
[0;31m[  FAILED  ] [mFatalFailureTest.FatalFailureInNestedSubroutine
[0;32m[ RUN      ] [mFatalFailureTest.NonfatalFailureInSubroutine
(expecting a failure on false)
gtest_output_test_.cc:#: Failure
Value of: false
  Actual: false
Expected: true
[0;31m[  FAILED  ] [mFatalFailureTest.NonfatalFailureInSubroutine
[0;32m[----------] [m1 test from LoggingTest
[0;32m[ RUN      ] [mLoggingTest.InterleavingLoggingAndAssertions
(expecting 2 failures on (3) >= (a[i]))
i == 0
i == 1
gtest_output_test_.cc:#: Failure
Expected: (3) >= (a[i]), actual: 3 vs 9
i == 2
i == 3
gtest_output_test_.cc:#: Failure
Expected: (3) >= (a[i]), actual: 3 vs 6
[0;31m[  FAILED  ] [mLoggingTest.InterleavingLoggingAndAssertions
[0;32m[----------] [m6 tests from SCOPED_TRACETest
[0;32m[ RUN      ] [mSCOPED_TRACETest.ObeysScopes
(expected to fail)
gtest_output_test_.cc:#: Failure
Failed
This failure is expected, and shouldn't have a trace.
gtest_output_test_.cc:#: Failure
Failed
This failure is expected, and should have a trace.
Google Test trace:
gtest_output_test_.cc:#: Expected trace
gtest_output_test_.cc:#: Failure
Failed
This failure is expected, and shouldn't have a trace.
[0;31m[  FAILED  ] [mSCOPED_TRACETest.ObeysScopes
[0;32m[ RUN      ] [mSCOPED_TRACETest.WorksInLoop
(expected to fail)
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  2
  n
    Which is: 1
Google Test trace:
gtest_output_test_.cc:#: i = 1
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  1
  n
    Which is: 2
Google Test trace:
gtest_output_test_.cc:#: i = 2
[0;31m[  FAILED  ] [mSCOPED_TRACETest.WorksInLoop
[0;32m[ RUN      ] [mSCOPED_TRACETest.WorksInSubroutine
(expected to fail)
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  2
  n
    Which is: 1
Google Test trace:
gtest_output_test_.cc:#: n = 1
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  1
  n
    Which is: 2
Google Test trace:
gtest_output_test_.cc:#: n = 2
[0;31m[  FAILED  ] [mSCOPED_TRACETest.WorksInSubroutine
[0;32m[ RUN      ] [mSCOPED_TRACETest.CanBeNested
(expected to fail)
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  1
  n
    Which is: 2
Google Test trace:
gtest_output_test_.cc:#: n = 2
gtest_output_test_.cc:#: 
[0;31m[  FAILED  ] [mSCOPED_TRACETest.CanBeNested
[0;32m[ RUN      ] [mSCOPED_TRACETest.CanBeRepeated
(expected to fail)
gtest_output_test_.cc:#: Failure
Failed
This failure is expected, and should contain trace point A.
Google Test trace:
gtest_output_test_.cc:#: A
gtest_output_test_.cc:#: Failure
Failed
This failure is expected, and should contain trace point A and B.
Google Test trace:
gtest_output_test_.cc:#: B
gtest_output_test_.cc:#: A
gtest_output_test_.cc:#: Failure
Failed
This failure is expected, and should contain trace point A, B, and C.
Google Test trace:
gtest_output_test_.cc:#: C
gtest_output_test_.cc:#: B
gtest_output_test_.cc:#: A
gtest_output_test_.cc:#: Failure
Failed
This failure is expected, and should contain trace point A, B, and D.
Google Test trace:
gtest_output_test_.cc:#: D
gtest_output_test_.cc:#: B
gtest_output_test_.cc:#: A
[0;31m[  FAILED  ] [mSCOPED_TRACETest.CanBeRepeated
[0;32m[ RUN      ] [mSCOPED_TRACETest.WorksConcurrently
(expecting 6 failures)
gtest_output_test_.cc:#: Failure
Failed
Expected failure #1 (in thread B, only trace B alive).
Google Test trace:
gtest_output_test_.cc:#: Trace B
gtest_output_test_.cc:#: Failure
Failed
Expected failure #2 (in thread A, trace A & B both alive).
Google Test trace:
gtest_output_test_.cc:#: Trace A
gtest_output_test_.cc:#: Failure
Failed
Expected failure #3 (in thread B, trace A & B both alive).
Google Test trace:
gtest_output_test_.cc:#: Trace B
gtest_output_test_.cc:#: Failure
Failed
Expected failure #4 (in thread B, only trace A alive).
gtest_output_test_.cc:#: Failure
Failed
Expected failure #5 (in thread A, only trace A alive).
Google Test trace:
gtest_output_test_.cc:#: Trace A
gtest_output_test_.cc:#: Failure
Failed
Expected failure #6 (in thread A, no trace alive).
[0;31m[  FAILED  ] [mSCOPED_TRACETest.WorksConcurrently
[0;32m[----------] [m1 test from NonFatalFailureInFixtureConstructorTest
[0;32m[ RUN      ] [mNonFatalFailureInFixtureConstructorTest.FailureInConstructor
(expecting 5 failures)
gtest_output_test_.cc:#: Failure
Failed
Expected failure #1, in the test fixture c'tor.
gtest_output_test_.cc:#: Failure
Failed
Expected failure #2, in SetUp().
gtest_output_test_.cc:#: Failure
Failed
Expected failure #3, in the test body.
gtest_output_test_.cc:#: Failure
Failed
Expected failure #4, in TearDown.
gtest_output_test_.cc:#: Failure
Failed
Expected failure #5, in the test fixture d'tor.
[0;31m[  FAILED  ] [mNonFatalFailureInFixtureConstructorTest.FailureInConstructor
[0;32m[----------] [m1 test from FatalFailureInFixtureConstructorTest
[0;32m[ RUN      ] [mFatalFailureInFixtureConstructorTest.FailureInConstructor
(expecting 2 failures)
gtest_output_test_.cc:#: Failure
Failed
Expected failure #1, in the test fixture c'tor.
gtest_output_test_.cc:#: Failure
Failed
Expected failure #2, in the test fixture d'tor.
[0;31m[  FAILED  ] [mFatalFailureInFixtureConstructorTest.FailureInConstructor
[0;32m[----------] [m1 test from NonFatalFailureInSetUpTest
[0;32m[ RUN      ] [mNonFatalFailureInSetUpTest.FailureInSetUp
(expecting 4 failures)
gtest_output_test_.cc:#: Failure
Failed
Expected failure #1, in SetUp().
gtest_output_test_.cc:#: Failure
Failed
Expected failure #2, in the test function.
gtest_output_test_.cc:#: Failure
Failed
Expected failure #3, in TearDown().
gtest_output_test_.cc:#: Failure
Failed
Expected failure #4, in the test fixture d'tor.
[0;31m[  FAILED  ] [mNonFatalFailureInSetUpTest.FailureInSetUp
[0;32m[----------] [m1 test from FatalFailureInSetUpTest
[0;32m[ RUN      ] [mFatalFailureInSetUpTest.FailureInSetUp
(expecting 3 failures)
gtest_output_test_.cc:#: Failure
Failed
Expected failure #1, in SetUp().
gtest_output_test_.cc:#: Failure
Failed
Expected failure #2, in TearDown().
gtest_output_test_.cc:#: Failure
Failed
Expected failure #3, in the test fixture d'tor.
[0;31m[  FAILED  ] [mFatalFailureInSetUpTest.FailureInSetUp
[0;32m[----------] [m1 test from AddFailureAtTest
[0;32m[ RUN      ] [mAddFailureAtTest.MessageContainsSpecifiedFileAndLineNumber
foo.cc:42: Failure
Failed
Expected failure in foo.cc
[0;31m[  FAILED  ] [mAddFailureAtTest.MessageContainsSpecifiedFileAndLineNumber
[0;32m[----------] [m4 tests from MixedUpTestCaseTest
[0;32m[ RUN      ] [mMixedUpTestCaseTest.FirstTestFromNamespaceFoo
[0;32m[       OK ] [mMixedUpTestCaseTest.FirstTestFromNamespaceFoo
[0;32m[ RUN      ] [mMixedUpTestCaseTest.SecondTestFromNamespaceFoo
[0;32m[       OK ] [mMixedUpTestCaseTest.SecondTestFromNamespaceFoo
[0;32m[ RUN      ] [mMixedUpTestCaseTest.ThisShouldFail
gtest.cc:#: Failure
Failed
All tests in the same test case must use the same test fixture
class.  However, in test case MixedUpTestCaseTest,
you defined test FirstTestFromNamespaceFoo and test ThisShouldFail
using two different test fixture classes.  This can happen if
the two classes are from different namespaces or translation
units and have the same name.  You should probably rename one
of the classes to put the tests into different test cases.
[0;31m[  FAILED  ] [mMixedUpTestCaseTest.ThisShouldFail
[0;32m[ RUN      ] [mMixedUpTestCaseTest.ThisShouldFailToo
gtest.cc:#: Failure
Failed
All tests in the same test case must use the same test fixture
class.  However, in test case MixedUpTestCaseTest,
you defined test FirstTestFromNamespaceFoo and test ThisShouldFailToo
using two different test fixture classes.  This can happen if
the two classes are from different namespaces or translation
units and have the same name.  You should probably rename one
of the classes to put the tests into different test cases.
[0;31m[  FAILED  ] [mMixedUpTestCaseTest.ThisShouldFailToo
[0;32m[----------] [m2 tests from MixedUpTestCaseWithSameTestNameTest
[0;32m[ RUN      ] [mMixedUpTestCaseWithSameTestNameTest.TheSecondTestWithThisNameShouldFail
[0;32m[       OK ] [mMixedUpTestCaseWithSameTestNameTest.TheSecondTestWithThisNameShouldFail
[0;32m[ RUN      ] [mMixedUpTestCaseWithSameTestNameTest.TheSecondTestWithThisNameShouldFail
gtest.cc:#: Failure
Failed
All tests in the same test case must use the same test fixture
class.  However, in test case MixedUpTestCaseWithSameTestNameTest,
you defined test TheSecondTestWithThisNameShouldFail and test TheSecondTestWithThisNameShouldFail
using two different test fixture classes.  This can happen if
the two classes are from different namespaces or translation
units and have the same name.  You should probably rename one
of the classes to put the tests into different test cases.
[0;31m[  FAILED  ] [mMixedUpTestCaseWithSameTestNameTest.TheSecondTestWithThisNameShouldFail
[0;32m[----------] [m2 tests from TEST_F_before_TEST_in_same_test_case
[0;32m[ RUN      ] [mTEST_F_before_TEST_in_same_test_case.DefinedUsingTEST_F
[0;32m[       OK ] [mTEST_F_before_TEST_in_same_test_case.DefinedUsingTEST_F
[0;32m[ RUN      ] [mTEST_F_before_TEST_in_same_test_case.DefinedUsingTESTAndShouldFail
gtest.cc:#: Failure
Failed
All tests in the same test case must use the same test fixture
class, so mixing TEST_F and TEST in the same test case is
illegal.  In test case TEST_F_before_TEST_in_same_test_case,
test DefinedUsingTEST_F is defined using TEST_F but
test DefinedUsingTESTAndShouldFail is defined using TEST.  You probably
want to change the TEST to TEST_F or move it to another test
case.
[0;31m[  FAILED  ] [mTEST_F_before_TEST_in_same_test_case.DefinedUsingTESTAndShouldFail
[0;32m[----------] [m2 tests from TEST_before_TEST_F_in_same_test_case
[0;32m[ RUN      ] [mTEST_before_TEST_F_in_same_test_case.DefinedUsingTEST
[0;32m[       OK ] [mTEST_before_TEST_F_in_same_test_case.DefinedUsingTEST
[0;32m[ RUN      ] [mTEST_before_TEST_F_in_same_test_case.DefinedUsingTEST_FAndShouldFail
gtest.cc:#: Failure
Failed
All tests in the same test case must use the same test fixture
class, so mixing TEST_F and TEST in the same test case is
illegal.  In test case TEST_before_TEST_F_in_same_test_case,
test DefinedUsingTEST_FAndShouldFail is defined using TEST_F but
test DefinedUsingTEST is defined using TEST.  You probably
want to change the TEST to TEST_F or move it to another test
case.
[0;31m[  FAILED  ] [mTEST_before_TEST_F_in_same_test_case.DefinedUsingTEST_FAndShouldFail
[0;32m[----------] [m8 tests from ExpectNonfatalFailureTest
[0;32m[ RUN      ] [mExpectNonfatalFailureTest.CanReferenceGlobalVariables
[0;32m[       OK ] [mExpectNonfatalFailureTest.CanReferenceGlobalVariables
[0;32m[ RUN      ] [mExpectNonfatalFailureTest.CanReferenceLocalVariables
[0;32m[       OK ] [mExpectNonfatalFailureTest.CanReferenceLocalVariables
[0;32m[ RUN      ] [mExpectNonfatalFailureTest.SucceedsWhenThereIsOneNonfatalFailure
[0;32m[       OK ] [mExpectNonfatalFailureTest.SucceedsWhenThereIsOneNonfatalFailure
[0;32m[ RUN      ] [mExpectNonfatalFailureTest.FailsWhenThereIsNoNonfatalFailure
(expecting a failure)
gtest.cc:#: Failure
Expected: 1 non-fatal failure
  Actual: 0 failures
[0;31m[  FAILED  ] [mExpectNonfatalFailureTest.FailsWhenThereIsNoNonfatalFailure
[0;32m[ RUN      ] [mExpectNonfatalFailureTest.FailsWhenThereAreTwoNonfatalFailures
(expecting a failure)
gtest.cc:#: Failure
Expected: 1 non-fatal failure
  Actual: 2 failures
gtest_output_test_.cc:#: Non-fatal failure:
Failed
Expected non-fatal failure 1.

gtest_output_test_.cc:#: Non-fatal failure:
Failed
Expected non-fatal failure 2.

[0;31m[  FAILED  ] [mExpectNonfatalFailureTest.FailsWhenThereAreTwoNonfatalFailures
[0;32m[ RUN      ] [mExpectNonfatalFailureTest.FailsWhenThereIsOneFatalFailure
(expecting a failure)
gtest.cc:#: Failure
Expected: 1 non-fatal failure
  Actual:
gtest_output_test_.cc:#: Fatal failure:
Failed
Expected fatal failure.

[0;31m[  FAILED  ] [mExpectNonfatalFailureTest.FailsWhenThereIsOneFatalFailure
[0;32m[ RUN      ] [mExpectNonfatalFailureTest.FailsWhenStatementReturns
(expecting a failure)
gtest.cc:#: Failure
Expected: 1 non-fatal failure
  Actual: 0 failures
[0;31m[  FAILED  ] [mExpectNonfatalFailureTest.FailsWhenStatementReturns
[0;32m[ RUN      ] [mExpectNonfatalFailureTest.FailsWhenStatementThrows
(expecting a failure)
gtest.cc:#: Failure
Expected: 1 non-fatal failure
  Actual: 0 failures
[0;31m[  FAILED  ] [mExpectNonfatalFailureTest.FailsWhenStatementThrows
[0;32m[----------] [m8 tests from ExpectFatalFailureTest
[0;32m[ RUN      ] [mExpectFatalFailureTest.CanReferenceGlobalVariables
[0;32m[       OK ] [mExpectFatalFailureTest.CanReferenceGlobalVariables
[0;32m[ RUN      ] [mExpectFatalFailureTest.CanReferenceLocalStaticVariables
[0;32m[       OK ] [mExpectFatalFailureTest.CanReferenceLocalStaticVariables
[0;32m[ RUN      ] [mExpectFatalFailureTest.SucceedsWhenThereIsOneFatalFailure
[0;32m[       OK ] [mExpectFatalFailureTest.SucceedsWhenThereIsOneFatalFailure
[0;32m[ RUN      ] [mExpectFatalFailureTest.FailsWhenThereIsNoFatalFailure
(expecting a failure)
gtest.cc:#: Failure
Expected: 1 fatal failure
  Actual: 0 failures
[0;31m[  FAILED  ] [mExpectFatalFailureTest.FailsWhenThereIsNoFatalFailure
[0;32m[ RUN      ] [mExpectFatalFailureTest.FailsWhenThereAreTwoFatalFailures
(expecting a failure)
gtest.cc:#: Failure
Expected: 1 fatal failure
  Actual: 2 failures
gtest_output_test_.cc:#: Fatal failure:
Failed
Expected fatal failure.

gtest_output_test_.cc:#: Fatal failure:
Failed
Expected fatal failure.

[0;31m[  FAILED  ] [mExpectFatalFailureTest.FailsWhenThereAreTwoFatalFailures
[0;32m[ RUN      ] [mExpectFatalFailureTest.FailsWhenThereIsOneNonfatalFailure
(expecting a failure)
gtest.cc:#: Failure
Expected: 1 fatal failure
  Actual:
gtest_output_test_.cc:#: Non-fatal failure:
Failed
Expected non-fatal failure.

[0;31m[  FAILED  ] [mExpectFatalFailureTest.FailsWhenThereIsOneNonfatalFailure
[0;32m[ RUN      ] [mExpectFatalFailureTest.FailsWhenStatementReturns
(expecting a failure)
gtest.cc:#: Failure
Expected: 1 fatal failure
  Actual: 0 failures
[0;31m[  FAILED  ] [mExpectFatalFailureTest.FailsWhenStatementReturns
[0;32m[ RUN      ] [mExpectFatalFailureTest.FailsWhenStatementThrows
(expecting a failure)
gtest.cc:#: Failure
Expected: 1 fatal failure
  Actual: 0 failures
[0;31m[  FAILED  ] [mExpectFatalFailureTest.FailsWhenStatementThrows
[0;32m[----------] [m2 tests from TypedTest/0, where TypeParam = int
[0;32m[ RUN      ] [mTypedTest/0.Success
[0;32m[       OK ] [mTypedTest/0.Success
[0;32m[ RUN      ] [mTypedTest/0.Failure
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  1
  TypeParam()
    Which is: 0
Expected failure
[0;31m[  FAILED  ] [mTypedTest/0.Failure, where TypeParam = int
[0;32m[----------] [m2 tests from Unsigned/TypedTestP/0, where TypeParam = unsigned char
[0;32m[ RUN      ] [mUnsigned/TypedTestP/0.Success
[0;32m[       OK ] [mUnsigned/TypedTestP/0.Success
[0;32m[ RUN      ] [mUnsigned/TypedTestP/0.Failure
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  1U
    Which is: 1
  TypeParam()
    Which is: '\0'
Expected failure
[0;31m[  FAILED  ] [mUnsigned/TypedTestP/0.Failure, where TypeParam = unsigned char
[0;32m[----------] [m2 tests from Unsigned/TypedTestP/1, where TypeParam = unsigned int
[0;32m[ RUN      ] [mUnsigned/TypedTestP/1.Success
[0;32m[       OK ] [mUnsigned/TypedTestP/1.Success
[0;32m[ RUN      ] [mUnsigned/TypedTestP/1.Failure
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  1U
    Which is: 1
  TypeParam()
    Which is: 0
Expected failure
[0;31m[  FAILED  ] [mUnsigned/TypedTestP/1.Failure, where TypeParam = unsigned int
[0;32m[----------] [m4 tests from ExpectFailureTest
[0;32m[ RUN      ] [mExpectFailureTest.ExpectFatalFailure
(expecting 1 failure)
gtest.cc:#: Failure
Expected: 1 fatal failure
  Actual:
gtest_output_test_.cc:#: Success:
Succeeded

(expecting 1 failure)
gtest.cc:#: Failure
Expected: 1 fatal failure
  Actual:
gtest_output_test_.cc:#: Non-fatal failure:
Failed
Expected non-fatal failure.

(expecting 1 failure)
gtest.cc:#: Failure
Expected: 1 fatal failure containing "Some other fatal failure expected."
  Actual:
gtest_output_test_.cc:#: Fatal failure:
Failed
Expected fatal failure.

[0;31m[  FAILED  ] [mExpectFailureTest.ExpectFatalFailure
[0;32m[ RUN      ] [mExpectFailureTest.ExpectNonFatalFailure
(expecting 1 failure)
gtest.cc:#: Failure
Expected: 1 non-fatal failure
  Actual:
gtest_output_test_.cc:#: Success:
Succeeded

(expecting 1 failure)
gtest.cc:#: Failure
Expected: 1 non-fatal failure
  Actual:
gtest_output_test_.cc:#: Fatal failure:
Failed
Expected fatal failure.

(expecting 1 failure)
gtest.cc:#: Failure
Expected: 1 non-fatal failure containing "Some other non-fatal failure."
  Actual:
gtest_output_test_.cc:#: Non-fatal failure:
Failed
Expected non-fatal failure.

[0;31m[  FAILED  ] [mExpectFailureTest.ExpectNonFatalFailure
[0;32m[ RUN      ] [mExpectFailureTest.ExpectFatalFailureOnAllThreads
(expecting 1 failure)
gtest.cc:#: Failure
Expected: 1 fatal failure
  Actual:
gtest_output_test_.cc:#: Success:
Succeeded

(expecting 1 failure)
gtest.cc:#: Failure
Expected: 1 fatal failure
  Actual:
gtest_output_test_.cc:#: Non-fatal failure:
Failed
Expected non-fatal failure.

(expecting 1 failure)
gtest.cc:#: Failure
Expected: 1 fatal failure containing "Some other fatal failure expected."
  Actual:
gtest_output_test_.cc:#: Fatal failure:
Failed
Expected fatal failure.

[0;31m[  FAILED  ] [mExpectFailureTest.ExpectFatalFailureOnAllThreads
[0;32m[ RUN      ] [mExpectFailureTest.ExpectNonFatalFailureOnAllThreads
(expecting 1 failure)
gtest.cc:#: Failure
Expected: 1 non-fatal failure
  Actual:
gtest_output_test_.cc:#: Success:
Succeeded

(expecting 1 failure)
gtest.cc:#: Failure
Expected: 1 non-fatal failure
  Actual:
gtest_output_test_.cc:#: Fatal failure:
Failed
Expected fatal failure.

(expecting 1 failure)
gtest.cc:#: Failure
Expected: 1 non-fatal failure containing "Some other non-fatal failure."
  Actual:
gtest_output_test_.cc:#: Non-fatal failure:
Failed
Expected non-fatal failure.

[0;31m[  FAILED  ] [mExpectFailureTest.ExpectNonFatalFailureOnAllThreads
[0;32m[----------] [m2 tests from ExpectFailureWithThreadsTest
[0;32m[ RUN      ] [mExpectFailureWithThreadsTest.ExpectFatalFailure
(expecting 2 failures)
gtest_output_test_.cc:#: Failure
Failed
Expected fatal failure.
gtest.cc:#: Failure
Expected: 1 fatal failure
  Actual: 0 failures
[0;31m[  FAILED  ] [mExpectFailureWithThreadsTest.ExpectFatalFailure
[0;32m[ RUN      ] [mExpectFailureWithThreadsTest.ExpectNonFatalFailure
(expecting 2 failures)
gtest_output_test_.cc:#: Failure
Failed
Expected non-fatal failure.
gtest.cc:#: Failure
Expected: 1 non-fatal failure
  Actual: 0 failures
[0;31m[  FAILED  ] [mExpectFailureWithThreadsTest.ExpectNonFatalFailure
[0;32m[----------] [m1 test from ScopedFakeTestPartResultReporterTest
[0;32m[ RUN      ] [mScopedFakeTestPartResultReporterTest.InterceptOnlyCurrentThread
(expecting 2 failures)
gtest_output_test_.cc:#: Failure
Failed
Expected fatal failure.
gtest_output_test_.cc:#: Failure
Failed
Expected non-fatal failure.
[0;31m[  FAILED  ] [mScopedFakeTestPartResultReporterTest.InterceptOnlyCurrentThread
[0;32m[----------] [m1 test from PrintingFailingParams/FailingParamTest
[0;32m[ RUN      ] [mPrintingFailingParams/FailingParamTest.Fails/0
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  1
  GetParam()
    Which is: 2
[0;31m[  FAILED  ] [mPrintingFailingParams/FailingParamTest.Fails/0, where GetParam() = 2
[0;32m[----------] [m2 tests from PrintingStrings/ParamTest
[0;32m[ RUN      ] [mPrintingStrings/ParamTest.Success/a
[0;32m[       OK ] [mPrintingStrings/ParamTest.Success/a
[0;32m[ RUN      ] [mPrintingStrings/ParamTest.Failure/a
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  "b"
  GetParam()
    Which is: "a"
Expected failure
[0;31m[  FAILED  ] [mPrintingStrings/ParamTest.Failure/a, where GetParam() = "a"
[0;32m[----------] [mGlobal test environment tear-down
BarEnvironment::TearDown() called.
gtest_output_test_.cc:#: Failure
Failed
Expected non-fatal failure.
FooEnvironment::TearDown() called.
gtest_output_test_.cc:#: Failure
Failed
Expected fatal failure.
[0;32m[==========] [m66 tests from 29 test cases ran.
[0;32m[  PASSED  ] [m22 tests.
[0;31m[  FAILED  ] [m44 tests, listed below:
[0;31m[  FAILED  ] [mNonfatalFailureTest.EscapesStringOperands
[0;31m[  FAILED  ] [mNonfatalFailureTest.DiffForLongStrings
[0;31m[  FAILED  ] [mFatalFailureTest.FatalFailureInSubroutine
[0;31m[  FAILED  ] [mFatalFailureTest.FatalFailureInNestedSubroutine
[0;31m[  FAILED  ] [mFatalFailureTest.NonfatalFailureInSubroutine
[0;31m[  FAILED  ] [mLoggingTest.InterleavingLoggingAndAssertions
[0;31m[  FAILED  ] [mSCOPED_TRACETest.ObeysScopes
[0;31m[  FAILED  ] [mSCOPED_TRACETest.WorksInLoop
[0;31m[  FAILED  ] [mSCOPED_TRACETest.WorksInSubroutine
[0;31m[  FAILED  ] [mSCOPED_TRACETest.CanBeNested
[0;31m[  FAILED  ] [mSCOPED_TRACETest.CanBeRepeated
[0;31m[  FAILED  ] [mSCOPED_TRACETest.WorksConcurrently
[0;31m[  FAILED  ] [mNonFatalFailureInFixtureConstructorTest.FailureInConstructor
[0;31m[  FAILED  ] [mFatalFailureInFixtureConstructorTest.FailureInConstructor
[0;31m[  FAILED  ] [mNonFatalFailureInSetUpTest.FailureInSetUp
[0;31m[  FAILED  ] [mFatalFailureInSetUpTest.FailureInSetUp
[0;31m[  FAILED  ] [mAddFailureAtTest.MessageContainsSpecifiedFileAndLineNumber
[0;31m[  FAILED  ] [mMixedUpTestCaseTest.ThisShouldFail
[0;31m[  FAILED  ] [mMixedUpTestCaseTest.ThisShouldFailToo
[0;31m[  FAILED  ] [mMixedUpTestCaseWithSameTestNameTest.TheSecondTestWithThisNameShouldFail
[0;31m[  FAILED  ] [mTEST_F_before_TEST_in_same_test_case.DefinedUsingTESTAndShouldFail
[0;31m[  FAILED  ] [mTEST_before_TEST_F_in_same_test_case.DefinedUsingTEST_FAndShouldFail
[0;31m[  FAILED  ] [mExpectNonfatalFailureTest.FailsWhenThereIsNoNonfatalFailure
[0;31m[  FAILED  ] [mExpectNonfatalFailureTest.FailsWhenThereAreTwoNonfatalFailures
[0;31m[  FAILED  ] [mExpectNonfatalFailureTest.FailsWhenThereIsOneFatalFailure
[0;31m[  FAILED  ] [mExpectNonfatalFailureTest.FailsWhenStatementReturns
[0;31m[  FAILED  ] [mExpectNonfatalFailureTest.FailsWhenStatementThrows
[0;31m[  FAILED  ] [mExpectFatalFailureTest.FailsWhenThereIsNoFatalFailure
[0;31m[  FAILED  ] [mExpectFatalFailureTest.FailsWhenThereAreTwoFatalFailures
[0;31m[  FAILED  ] [mExpectFatalFailureTest.FailsWhenThereIsOneNonfatalFailure
[0;31m[  FAILED  ] [mExpectFatalFailureTest.FailsWhenStatementReturns
[0;31m[  FAILED  ] [mExpectFatalFailureTest.FailsWhenStatementThrows
[0;31m[  FAILED  ] [mTypedTest/0.Failure, where TypeParam = int
[0;31m[  FAILED  ] [mUnsigned/TypedTestP/0.Failure, where TypeParam = unsigned char
[0;31m[  FAILED  ] [mUnsigned/TypedTestP/1.Failure, where TypeParam = unsigned int
[0;31m[  FAILED  ] [mExpectFailureTest.ExpectFatalFailure
[0;31m[  FAILED  ] [mExpectFailureTest.ExpectNonFatalFailure
[0;31m[  FAILED  ] [mExpectFailureTest.ExpectFatalFailureOnAllThreads
[0;31m[  FAILED  ] [mExpectFailureTest.ExpectNonFatalFailureOnAllThreads
[0;31m[  FAILED  ] [mExpectFailureWithThreadsTest.ExpectFatalFailure
[0;31m[  FAILED  ] [mExpectFailureWithThreadsTest.ExpectNonFatalFailure
[0;31m[  FAILED  ] [mScopedFakeTestPartResultReporterTest.InterceptOnlyCurrentThread
[0;31m[  FAILED  ] [mPrintingFailingParams/FailingParamTest.Fails/0, where GetParam() = 2
[0;31m[  FAILED  ] [mPrintingStrings/ParamTest.Failure/a, where GetParam() = "a"

44 FAILED TESTS
[0;33m  YOU HAVE 1 DISABLED TEST

[mNote: Google Test filter = FatalFailureTest.*:LoggingTest.*
[==========] Running 4 tests from 2 test cases.
[----------] Global test environment set-up.
[----------] 3 tests from FatalFailureTest
[ RUN      ] FatalFailureTest.FatalFailureInSubroutine
(expecting a failure that x should be 1)
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  1
  x
    Which is: 2
[  FAILED  ] FatalFailureTest.FatalFailureInSubroutine (? ms)
[ RUN      ] FatalFailureTest.FatalFailureInNestedSubroutine
(expecting a failure that x should be 1)
gtest_output_test_.cc:#: Failure
Expected equality of these values:
  1
  x
    Which is: 2
[  FAILED  ] FatalFailureTest.FatalFailureInNestedSubroutine (? ms)
[ RUN      ] FatalFailureTest.NonfatalFailureInSubroutine
(expecting a failure on false)
gtest_output_test_.cc:#: Failure
Value of: false
  Actual: false
Expected: true
[  FAILED  ] FatalFailureTest.NonfatalFailureInSubroutine (? ms)
[----------] 3 tests from FatalFailureTest (? ms total)

[----------] 1 test from LoggingTest
[ RUN      ] LoggingTest.InterleavingLoggingAndAssertions
(expecting 2 failures on (3) >= (a[i]))
i == 0
i == 1
gtest_output_test_.cc:#: Failure
Expected: (3) >= (a[i]), actual: 3 vs 9
i == 2
i == 3
gtest_output_test_.cc:#: Failure
Expected: (3) >= (a[i]), actual: 3 vs 6
[  FAILED  ] LoggingTest.InterleavingLoggingAndAssertions (? ms)
[----------] 1 test from LoggingTest (? ms total)

[----------] Global test environment tear-down
[==========] 4 tests from 2 test cases ran. (? ms total)
[  PASSED  ] 0 tests.
[  FAILED  ] 4 tests, listed below:
[  FAILED  ] FatalFailureTest.FatalFailureInSubroutine
[  FAILED  ] FatalFailureTest.FatalFailureInNestedSubroutine
[  FAILED  ] FatalFailureTest.NonfatalFailureInSubroutine
[  FAILED  ] LoggingTest.InterleavingLoggingAndAssertions

 4 FAILED TESTS
Note: Google Test filter = *DISABLED_*
[==========] Running 1 test from 1 test case.
[----------] Global test environment set-up.
[----------] 1 test from DisabledTestsWarningTest
[ RUN      ] DisabledTestsWarningTest.DISABLED_AlsoRunDisabledTestsFlagSuppressesWarning
[       OK ] DisabledTestsWarningTest.DISABLED_AlsoRunDisabledTestsFlagSuppressesWarning
[----------] Global test environment tear-down
[==========] 1 test from 1 test case ran.
[  PASSED  ] 1 test.
Note: Google Test filter = PassingTest.*
Note: This is test shard 2 of 2.
[==========] Running 1 test from 1 test case.
[----------] Global test environment set-up.
[----------] 1 test from PassingTest
[ RUN      ] PassingTest.PassingTest2
[       OK ] PassingTest.PassingTest2
[----------] Global test environment tear-down
[==========] 1 test from 1 test case ran.
[  PASSED  ] 1 test.
