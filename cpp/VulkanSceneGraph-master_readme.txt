cmake_minimum_required(VERSION 3.7)

project(VSG
    VERSION 0.0.0
    DESCRIPTION "Vulkan/VkSceneGraph Prototype library"
    LANGUAGES CXX
)
set(VSG_SOVERSION 0)

# create the version header
set(VSG_VERSION_HEADER "${PROJECT_BINARY_DIR}/include/vsg/core/Version.h")
configure_file("${CMAKE_CURRENT_SOURCE_DIR}/src/vsg/core/Version.h.in" "${VSG_VERSION_HEADER}")

set(OUTPUT_BINDIR ${PROJECT_BINARY_DIR}/bin)
set(OUTPUT_LIBDIR ${PROJECT_BINARY_DIR}/lib)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${OUTPUT_LIBDIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${OUTPUT_LIBDIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${OUTPUT_BINDIR})

SET(CMAKE_DEBUG_POSTFIX "d" CACHE STRING "add a postfix, usually d on windows")
SET(CMAKE_RELEASE_POSTFIX "" CACHE STRING "add a postfix, usually empty on windows")
SET(CMAKE_RELWITHDEBINFO_POSTFIX "rd" CACHE STRING "add a postfix, usually empty on windows")
SET(CMAKE_MINSIZEREL_POSTFIX "s" CACHE STRING "add a postfix, usually empty on windows")

if(WIN32)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${OUTPUT_BINDIR})
    # set up local bin directory to place all binaries
    make_directory(${OUTPUT_BINDIR})
    make_directory(${OUTPUT_LIBDIR})
else(WIN32)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${OUTPUT_LIBDIR})
    # set up local bin directory to place all binaries
    make_directory(${OUTPUT_LIBDIR})
endif(WIN32)


set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${OUTPUT_BINDIR})

# Change the default build type to Release
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release CACHE STRING "Choose the type of build, options are: None Debug Release RelWithDebInfo MinSizeRel." FORCE)
endif(NOT CMAKE_BUILD_TYPE)

if(CMAKE_COMPILER_IS_GNUCXX)
    set(VSG_WARNING_FLAGS -Wall -Wparentheses -Wno-long-long -Wno-import -Wreturn-type -Wmissing-braces -Wunknown-pragmas -Wmaybe-uninitialized -Wshadow -Wunused -Wno-misleading-indentation -Wextra)
elseif(CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
    set(VSG_WARNING_FLAGS -Wall -Wparentheses -Wno-long-long -Wno-import -Wreturn-type -Wmissing-braces -Wunknown-pragmas -Wshadow -Wunused -Wextra)
endif()

set(VSG_WARNING_FLAGS ${VSG_WARNING_FLAGS} CACHE STRING "Compiler flags to use." FORCE)
add_compile_options(${VSG_WARNING_FLAGS})


find_package(Vulkan)
find_package(Threads)

if (ANDROID)
    find_library(AndroidLib android)
    if(CMAKE_SYSTEM_VERSION GREATER 24)
        find_library(AndroidNativeWindowLib nativewindow)
    endif()
elseif (WIN32)
    # just use native windowing
elseif (APPLE)
    find_library(COCOA_LIBRARY Cocoa)
    find_library(QUARTZCORE_LIBRARY QuartzCore)
else()
    # just use Xcb for native windowing
    find_package(PkgConfig)
    pkg_check_modules(xcb REQUIRED IMPORTED_TARGET xcb)
endif()



# create doxygen build target
find_package(Doxygen QUIET)
if (DOXYGEN_FOUND)
    set(DOXYGEN_GENERATE_HTML YES)
    set(DOXYGEN_GENERATE_MAN NO)

    doxygen_add_docs(
        docs
        ${PROJECT_SOURCE_DIR}/include/vsg
        COMMENT "Use doxygen to Generate html documentaion"
    )
endif()

# add clobber build target to clear all the non git registered files/directories
add_custom_target(clobber
    COMMAND git clean -d -f -x
)

# automatically buil_all_h build target to generate the include/vsg/all.h from the headers in the include/vsg/* directories
add_custom_target(build_all_h
    COMMAND ${CMAKE_COMMAND} -P ${CMAKE_CURRENT_SOURCE_DIR}/build/build_all_h.cmake
)

# automatically buil_all_h build target to generate the include/vsg/all.h from the headers in the include/vsg/* directories
add_custom_target(uninstall
    COMMAND ${CMAKE_COMMAND} -P ${CMAKE_CURRENT_SOURCE_DIR}/build/uninstall.cmake
)

# add cppcheck build target to provide static analysis of codebase
find_program(CPPCHECK cppcheck)
if (CPPCHECK)
    file(RELATIVE_PATH PATH_TO_SOURCE ${PROJECT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR} )
    if (PATH_TO_SOURCE)
        set(PATH_TO_SOURCE "${PATH_TO_SOURCE}/")
    endif()

    include(ProcessorCount)
    ProcessorCount(CPU_CORES)

    set(CPPCHECK_SUPPRESION_LIST_FILE "${CMAKE_SOURCE_DIR}/build/cppcheck-suppression-list.txt")
    set(CPPCHECK_SUPPRESION_LIST "--suppressions-list=${CPPCHECK_SUPPRESION_LIST_FILE}")
    set(CPPCHECK_EXTRA_OPTIONS "" CACHE STRING "additional commndline options to use when invoking cppcheck")
    add_custom_target(cppcheck
        COMMAND ${CPPCHECK} -j ${CPU_CORES} --quiet --enable=style --language=c++ ${CPPCHECK_EXTRA_OPTIONS} ${CPPCHECK_SUPPRESION_LIST} ${PATH_TO_SOURCE}include/vsg/*/*.h ${PATH_TO_SOURCE}src/vsg/*/*.cpp -I ${PATH_TO_SOURCE}include/
        WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
        COMMENT "Static code analsysi using cppcheck"
    )
endif()

# add clang-foramt build target to enforce a standard code style guide.
find_program(CLANGFORMAT clang-format)
if (CLANGFORMAT)
    add_custom_target(clang-format
        COMMAND ${CLANGFORMAT} -i ${PATH_TO_SOURCE}include/vsg/*/*.h ${PATH_TO_SOURCE}src/vsg/*/*.cpp
        WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
        COMMENT "Automated code format using clang-format"
    )
endif()

#
# src directory contains all the source of the vsg library
#
add_subdirectory(src/vsg)
## Build and Install instructions index
* [Prerequisites](#prerequisites) - list of project external dependencies
* Unix
	* [Quick Unix instructions](#quick-build-instructions-for-unix-from-the-command-line)
* Windows
	* [Quick Windows instructions](#quick-build-instructions-for-windows-using-visual-studio-2017)
	* [Detailed Windows instructions](#detailed-instructions-for-setting-up-your-environment-and-building-for-microsoft-windows)
* Android
	* [Quick Android instructions](#quick-build-instructions-for-android)
	* [Detailed Android instructions](#detailed-instructions-for-setting-up-your-environment-and-building-for-android)
* macOS
	* [Quick macOS instructions](#quick-build-instructions-for-macOS-using-xcode-9)
	* [Detailed macOS instructions](#detailed-instructions-for-setting-up-your-environment-and-building-for-macos)
* [Build targets](#available-build-targets)
* [Using the VSG within your own projects](#using-the-vsg-within-your-own-projects)

---

## Prerequisites
* C++17 compliant compiler i.e. g++ 7.3 or later, Clang 6.0 or later, Visual Studio S2017 or later.
* [Vulkan](https://vulkan.lunarg.com/) 1.1 or later.
* [CMake](https://www.cmake.org) 3.7 or later.

The above dependency versions are known to work so they've been set as the current minimum, it may be possible to build against older versions. If you find success with older versions let us know and we can update the version info.

---

## Quick build instructions for Unix from the command line

Command line instructions for default build of static library (.a/.lib) in source:

    git clone https://github.com/vsg-dev/VulkanSceneGraphPrototype.git
    cd VulkanSceneGraphPrototype
    cmake .
    make -j 8
    make install

Command line instructions for building shared library (.so/.lib + .dll) out of source:

    git clone https://github.com/vsg-dev/VulkanSceneGraphPrototype.git
    mkdir vsg-shared-build
    cd vsg-shared-build
    cmake ../VulkanSceneGraphPrototype -DBUILD_SHARED_LIBS=ON
    make -j 8
    make install

---

## Quick build instructions for Windows using Visual Studio 2017

Command line instructions for default build of static library (.lib) in source:

    git clone https://github.com/vsg-dev/VulkanSceneGraphPrototype.git
    cd VulkanSceneGraphPrototype
    cmake . -G "Visual Studio 15 2017 Win64"

After running cmake open the generated VSG.sln file and build the All target. Once built you can run the install target. If you are using the default cmake install path (in Program Files folder), ensure you have started Visual Studio as administrator otherwise the install will fail.

More detailed Windows platform instructions can be found [below](#detailed-instructions-for-setting-up-your-environment-and-building-for-microsoft-windows).

---

## Quick build instructions for Android

Requires Android NDK 18 and CMake 3.13 (lower CMake versions may work but have not been tested).

	cmake ./ \
	-DCMAKE_BUILD_TYPE="Debug" \
	-DCMAKE_SYSTEM_NAME="Android" \
	-DCMAKE_SYSTEM_VERSION=24 \
	-DCMAKE_ANDROID_STL_TYPE="c++_static" \
	-DCMAKE_ANDROID_ARCH_ABI=armeabi-v7a \
	-DCMAKE_ANDROID_NDK=/location/of/Android/sdk/ndk-bundle \
	-DCMAKE_INSTALL_PREFIX=/usr/local/android

	make -j 8
	make install

More detailed Android platform instructions can be found [below](#detailed-instructions-for-setting-up-your-environment-and-building-for-android).

---

## Quick build instructions for macOS using Xcode 9

Command line instructions for default build of static library (.lib) in source:

    git clone https://github.com/vsg-dev/VulkanSceneGraphPrototype.git
    cd VulkanSceneGraphPrototype
    cmake . -G "Xcode"

After running cmake open the generated VSG.xcodeproj file and build the All target. Once built you can run the install target. Please note that for release builds you currently need to use the Archive option in xcode. This will rebuild every time so you can just select the install target and run Archive which will also build the All target.

---

## Available build targets

Once you have generated the build system using *cmake* as above, you can list the available make options using:

    make help

This lists the options:

    ... all (the default if no target is provided)
	... clean
	... depend
	... install/strip
	... install/local
	... rebuild_cache
	... clobber
	... install
	... docs
	... uninstall
	... build_all_h
	... list_install_components
	... cppcheck
	... clang-format
	... edit_cache
	... vsg

Most of these are standard options which you can look up in CMake and make documentation, the following are ones we've added so require explanation:

    # remove all files not part of the git repository - including all temporary CMake and build files.
    make clobber

    # run cppcheck on headers & source to generate a static analysis
    make cppcheck

    # run clang-format on headers & source to format to style specified by .clang-format specification
    make clang-format

    # generate the include/vsg/all.h from all the files that match include/vsg/*/*.h
    make build_all_h

---

## Using the VSG within your own projects

The project is currently a prototype that is undergoing continuous development so it isn't recommend to use as base for long term software development. At this point it's available for developers who want to test the bleeding edge and provide feedback on it's fitness for purpose. Following instructions assume your project uses CMake, which at this early stage in the project is the recommended route when using the VSG.

To assist with setting up software to work with the VSG when you install the library a CMake package configuration file will be installed in the lib/cmake/vsg directory. Within your CMake CMakeLists.txt script to find the VSG related dependencies you'll need to add:

	find_package(vsg)

To select C++17 compilation you'll need:

	set_property(TARGET mytargetname PROPERTY CXX_STANDARD 17)

To link your lib/application to required dependencies you'll need:

	target_link_libraries(mytargetname vsg::vsg)

This will tell CMake to set up all the appropriate include paths, libs and any definitions (such as the VSG_SHARED_LIBRARY #define that is required under Windows with shared library builds to select the correct declspec().)

For example, a bare minimum CMakeLists.txt file to compile a single file application would be:

	cmake_minimum_required(VERSION 3.7)
	find_package(vsg REQUIRED)
	add_executable(myapp "myapp.cpp")
	set_property(TARGET myapp PROPERTY CXX_STANDARD 17)
	target_link_libraries(myapp vsg::vsg)

---

## Detailed instructions for setting up your environment and building for Microsoft Windows

The VSG has one dependency, the Vulkan SDK itself. LunarG provides a convenient installer for the Vulkan SDK and runtime on Windows.

[Vulkan Downloads](https://vulkan.lunarg.com/sdk/home#windows)

From there download and install the Vulkan SDK (1.1 or later) and the Vulkan runtime. Once installed we need to let CMake know where to find the Vulkan SDK. The VSG uses the VULKAN_SDK environment variable to find the Vulkan SDK so go ahead and add it.

	VULKAN_SDK = C:\VulkanSDK\1.1.85.0

So now we have the Vulkan SDK installed and findable by CMake so we can go ahead and build VSG. Below are simple instructions for downloading the VSG source code, generating a Visual Studio project using CMake and finally building and installing VSG onto your system.

    git clone https://github.com/vsg-dev/VulkanSceneGraphPrototype.git
    cd VulkanSceneGraphPrototype
    cmake . -G "Visual Studio 15 2017 Win64"

After running CMake open the generated VSG.sln file and build the All target. Once built you can run the install target. If you are using the default CMake install path (in Program Files folder), ensure you have started Visual Studio as administrator otherwise the install will fail.

It's recommended at this point that you add the VSG install path to you CMAKE_PREFIX_PATH, this will allow other CMake projects, like the vsgExamples project to find your VSG installation. CMAKE_PREFIX_PATH can be set as an environment variable on you system.

    CMAKE_PREFIX_PATH = C:\Program Files\VSG

---

## Detailed instructions for setting up your environment and building for Android

This guide is to build VSG for Android, these steps have been completed on macOS but should be almost identical on Linux and similar on Windows. Inorder to build VSG for Android you'll need the following installed on your machine.

	Android NDK 18
	CMake 3.13

The easiest way to get the Android NDK installed is via Android Studio. Follow the link below to download and install it for your OS.

[Android Studio](https://developer.android.com/studio/)

If you got to the 'SDK Manager' ensure you have at least Android API level 24 installed, then go to the 'SDK Tools' tab and check the 'NDK' option. Once done click apply and Android Studio should download and install these components for you.

If you already have Android Studio and or the NDK installed. Still go to the 'SDK Manager' and see if you need to update your NDK to version 18.

Take note of the 'Android SDK Location' as you'll need it when running CMake to generate our Android make files.

So now we have the Android NDK installed lets go ahead and fetch the VSG source then use CMake to generate the make files.

	git clone https://github.com/vsg-dev/VulkanSceneGraphPrototype.git
	cd VulkanSceneGraphPrototype
	cmake ./ \
	-DCMAKE_BUILD_TYPE="Debug" \
	-DCMAKE_SYSTEM_NAME="Android" \
	-DCMAKE_SYSTEM_VERSION=24 \
	-DCMAKE_ANDROID_STL_TYPE="c++_static" \
	-DCMAKE_ANDROID_ARCH_ABI=armeabi-v7a \
	-DCMAKE_ANDROID_NDK=/location/of/Android/sdk/ndk-bundle \
	-DCMAKE_INSTALL_PREFIX=/usr/local/android

Make sure you change the -DCMAKE_ANDROID_NDK path to the path of your NDK, typically this is the 'Android SDK Location'/ndk-bundle. Also note the -DCMAKE_INSTALL_PREFIX. This is where the VSG library and header will be installed. It's useful to change this from the default to seperate your Android version from your native OS version. Depending where you put it you may need to manually create the top level folder first depending on permissions.

Now we've generated the make files we can simply run

	make -j 8
	make install

That's it, you've built VSG for Android and installed the required headers and library files onto your machine ready to use with your project or the Android vsgExamples.


## Detailed instructions for setting up your environment and building for macOS

macOS does not natively support Vulkan. However the excellent MoltenVK libary has been developed which translates Vulkan calls into the Metal equivalents allowing you to run Vulkan applications on macOS and iOS. This can be downloaded from the LunarG website and has been packaged in a way it's extremely similar to the other platform sdks.

[Vulkan Downloads](https://vulkan.lunarg.com/sdk/home#mac)

Download the sdk and unpack it. There's no form of installer but you're able to place the root sdk folder anywhere on your machine. The sdk contains detailed instuctions on how to setup MoltenVK to work on your machine as well has how to redistribute your application contained in the /Documentation/getting_started_macos.md file.

As with other platforms we need the VULKAN_SDK variable which should point to your downloaded sdk folder. Specifically the macOS subfolder of the sdk. This is needed so CMake can find the sdk. Unique to macOS we also need to set environment variables pointing a few files within the sdk. Again the getting started document in the sdk has detailed information relating to these. A quick cheat sheet is provided here, if you use a .bash_profile file in your user folder you can add the following.

	export VULKAN_SDK="/path/to/your/vulkansdk/macOS"
	export VK_LAYER_PATH="$VULKAN_SDK/etc/vulkan/explicit_layer.d"
	export VK_ICD_FILENAMES="$VULKAN_SDK/etc/vulkan/icd.d/MoltenVK_icd.json"
	export PATH="$VULKAN_SDK:$VULKAN_SDK/bin:$PATH"
	export DYLD_LIBRARY_PATH="$VULKAN_SDK/lib:$DYLD_LIBRARY_PATH"

At this point MoltenVK application should be able to run on your machine, as a quick test it's worth running vulkaninfo executable contained within vulkansdk/macOS/bin. If this runs and doesn't produce any errors it's a good indication the sdk is setup correctly.

So now we're ready to build VSG. With the SDK installed this is very similar to other platforms. You can simple run the following commands to clone the source and use CMake to generate and Xcode project.

	git clone https://github.com/vsg-dev/VulkanSceneGraphPrototype.git
	cd VulkanSceneGraphPrototype
	cmake . -G "Xcode"
	
Once CMake has finished you can open the generated Xcode project and build the 'install' target. This will build VSG and install the headers and generated library onto your machine.

Again, as with other platforms it's useful to now set your CMAKE_PREFIX_PATH to point to the VSG library we have just installed. If you've installed to the default location you can add the following to you .bash_profile file.

	export CMAKE_PREFIX_PATH="/usr/local/lib/cmake/vsg"
	
That's it, we've installed the MoltenVK sdk, built VSG and prepared are machine so other CMake projects can find and use the VSG library.

**Important Note!**

Xcode typically ignores the system environment variables, so when running a VSG application from within Xcode you may run into issues. One solution is to add the environment variables to to the run scheme. This can be done by going to 'Product>Scheme>Edit Scheme>Arguments. Then added the above mentioned environment variables.




MIT License

Copyright(c) 2018 Robert Osfield

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
| [View as Website](https://vsg-dev.github.io/VulkanSceneGraph/) |  [View as GitHub repository](https://github.com/vsg-dev/VulkanSceneGraph) |


VulkanSceneGraph/VkSceneGraph (VSG), currently under development, is a modern, cross platform, high performance scene graph library built upon [Vulkan](https://www.khronos.org/vulkan/) graphics/compute API. The software is written in [C++17](https://en.wikipedia.org/wiki/C%2B%2B17), and follows the [CppCoreGuidlines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines) and [FOSS Best Practices](https://github.com/coreinfrastructure/best-practices-badge/blob/master/doc/criteria.md).  The source code is published under the [MIT License](LICENSE.md).

The project aims to bring the performance of Vulkan to the wider developer community by providing a modern, high quality software library that is easy to use and focused on making the development of high performance graphics and compute applications a productive and fun experience. Our aim is reach a standard usable professional compute and graphics applications in the second half of 2019.

This repository contains basic documentation, C++ headers and source and CMake build scripts to build the prototype libvsg library.  Additional support libraries and examples are provided in separate repositories, links to these are provided below.  The software currently builds under Linux, Windows, Android and macOS (using [MoltenVk](https://github.com/KhronosGroup/MoltenVK)). Support for iOS will be added in 2019.

## Public discussion list/forum
We have created a [VulkanSceneGraph Developer Discussion Group](https://groups.google.com/forum/#!forum/vsg-users), if you want discuss the project, how to contribute etc. then please join the discussion group.

## Useful links in codebase and to associated projects
* Detailed build and install [instructions](INSTALL.md)
* Headers - the public interface : [include/vsg/](include/vsg)
* Source - the implementation : [src/vsg/](src/vsg)
* Tests & Examples - companion repository : [https://github.com/vsg-dev/vsgExamples](https://github.com/vsg-dev/vsgExamples)
* Software development [Road Map](ROADMAP.md)
* Design : [Principles and Philosophy](docs/Design/DesignPrinciplesAndPhilosophy.md),  [High Level Decisions](docs/Design/HighLevelDesignDecisions.md)
* Community resources :  [Code of Conduct](docs/CODE_OF_CONDUCT.md), [Contributing guide](docs/CONTRIBUTING.md)
* Exploration Phase Materials (*completed*): [Areas of Interest](docs/ExplorationPhase/AreasOfInterest.md), [3rd Party Resources](docs/ExplorationPhase/3rdPartyResources.md) and [Exploration Phase Report](docs/ExplorationPhase/VulkanSceneGraphExplorationPhaseReport.md)
* Prototype Phase Materials (*completed*): [Workplan](docs/PrototypePhase/Workplan.md) and [Prototype Phase Report](docs/PrototypePhase/PrototypePhaseReport.md)

---

## Quick Guide to building the VSG

### Prerequisites:
* C++17 compliant compiler i.e.. g++ 7.3 or later, Clang 6.0 or later, Visual Studio S2017 or later.
* [Vulkan](https://vulkan.lunarg.com/) 1.1 or later.
* [CMake](https://www.cmake.org) 3.7 or later.

The above dependency versions are known to work so they've been set as the current minimum, it may be possible to build against older versions.  If you find success with older versions let us know and we can update the version info.

### Command line build instructions:
To build and install the static libvsg library (.a/.lib) in source:

    git clone https://github.com/vsg-dev/VulkanSceneGraph.git
    cd VulkanSceneGraph
    cmake .
    make -j 8
    make install

Full details on how to build of the VSG (Unix/Windows/Android/macOS) can be found in the [INSTALL.md](INSTALL.md) file.

---

## Examples of the VSG in use

It's still very early days for the project so we don't have many projects that use to the VSG to reference, for our own testing purposes we have two project which may serve as an illustration of how to compile against the VSG and how to use parts of it's API.  These projects are:

* [vsgExamples](https://github.com/vsg-dev/vsgExamples) example programs that we are using to test out VSG functionality and illustrates usage.
* [osg2vsg](https://github.com/vsg-dev/osg2vsg) utility library that integrates OpenSceneGraph with the VSG to leverages 3d model and image loaders and converts them to VSG equivalents.  Once converted they can be viewed with the osg2vsg application, or loaded and rendered by [vsgviewer](https://github.com/vsg-dev/vsgExamples/tree/master/Desktop/vsgviewer) provided by vsgExamples.

Three examples within the vsgExamples project that may be of particular interest are ports of Vulkan tutorials to the VSG API.  In each case the VSG version requires less than 1/5th the amount of code to achieve the same functionality.

* [Vulkan Tutorial](https://vulkan-tutorial.com/) ported as [vsgExamples/Desktop/vsgdraw](https://github.com/vsg-dev/vsgExamples/blob/master/Desktop/vsgdraw/)
* [vulkan_minimal_compute](https://github.com/Erkaman/vulkan_minimal_compute) tutorial ported to VSG [vsgExamples/Desktop/vsgcompute](https://github.com/vsg-dev/vsgExamples/blob/master/Desktop/vsgcompute/)

## Roadmap

### 1. Exploration Phase, June-September 2018 (completed)
**Goal : Establish which technologies and broad techniques to use**

Learn and experiment with Vulkan, modern C++, and possible 3rd party dependencies.
Experimenting with different approaches to object/scene graph design and implementation. Exploration Phase Materials :

* [Principles and Philosophy](docs/Design/DesignPrinciplesAndPhilosophy.md)
* [High Level Design Decisions](docs/Design/HighLevelDesignDecisions.md)
* [Exploration Phase Report](docs/ExplorationPhase/VulkanSceneGraphExplorationPhaseReport.md)
* [Areas of Interest](docs/ExplorationPhase/AreasOfInterest.md)
* [3rd Party Resources](docs/ExplorationPhase/3rdPartyResources.md)

### 2. Prototype Phase, October-December 2018 (completed)
**Goal : Rapid prototyping of main classes, library and test applications to establish how the scene graph API will broadly look and work.**

Prototype Phase Materials:

* [Prototype Phase Workplan](docs/PrototypePhase/Workplan.md)
* [Prototype Phase Report](docs/PrototypePhase/PrototypePhaseReport.md)

### 3. Core Development Phase, January-Summer 2019
**Goal: Create the final class interfaces and implementation**

Using the prototyping work as a guide implement the final scene graph library with the aim of creating a solid interface and implementation.

* Development of final VSG Library
* Support for multi-threaded database paging
* Support for multi-threaded viewer, cull and dispatch traversals
* Support for multi-pass rendering
* Support for large scale whole world databases (double support for scene graph transforms)
* Development of add on libraries that provide:
    * Support for major image formats
    * Support for major 3D model formats, including FBX, glTF.
    * Support for PBR shaders
    * Support for Text rendering
* Development of test suite of programs and data
* Support for RTX Mesh shaders and ray tracing
* Support for integration with OpenGL/OSG applications via [EXT\_external\_object](https://www.khronos.org/registry/OpenGL/extensions/EXT/EXT_external_objects.txt) & [VK\_KHR\_external\_memory](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/man/html/VK_KHR_external_memory.html#versions-1.1-promotions)
* Port to iOS

### 4. Release Phase,  Fall 2019 onwards
**Goal: Test scene graph library against real-world applications and shake down the API and implementation for it's first stable release.**

* Refinement of API and implementation
* Build relationships with application developers and involve them in testing
* Create tutorial and example programs to illustrate how to use VSG
* Test, debug, refine and release 1.0.0!
# Pull Request Template

## Description

Please include a summary of the change and which issue is fixed. Please also include relevant motivation and context. List any dependencies that are required for this change.

Fixes # (issue)

## Type of change

Please delete options that are not relevant.

- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] This change requires a documentation update

## How Has This Been Tested?

Please describe the tests that you ran to verify your changes. Provide instructions so we can reproduce. Please also list any relevant details for your test configuration

- [ ] Test A
- [ ] Test B

**Test Configuration**:
* Firmware version:
* Hardware:
* Toolchain:
* SDK:

## Checklist:

- [ ] My code follows the style guidelines of this project
- [ ] I have performed a self-review of my own code
- [ ] I have commented my code, particularly in hard-to-understand areas
- [ ] I have made corresponding changes to the documentation
- [ ] My changes generate no new warnings
- [ ] I have added tests that prove my fix is effective or that my feature works
- [ ] New and existing unit tests pass locally with my changes
- [ ] Any dependent changes have been merged and published in downstream modules
---
name: Bug report
about: Create a report to help us improve

---

**Describe the bug**
A clear and concise description of what the bug is.

**To Reproduce**
Steps to reproduce the behavior:
1. Go to '...'
2. Click on '....'
3. Scroll down to '....'
4. See error

**Expected behavior**
A clear and concise description of what you expected to happen.

**Screenshots**
If applicable, add screenshots to help explain your problem.

**Desktop (please complete the following information):**
 - OS: [e.g. iOS]
 - Browser [e.g. chrome, safari]
 - Version [e.g. 22]

**Smartphone (please complete the following information):**
 - Device: [e.g. iPhone6]
 - OS: [e.g. iOS8.1]
 - Browser [e.g. stock browser, safari]
 - Version [e.g. 22]

**Additional context**
Add any other context about the problem here.
---
name: Feature request
about: Suggest an idea for this project

---

**Is your feature request related to a problem? Please describe.**
A clear and concise description of what the problem is. Ex. I'm always frustrated when [...]

**Describe the solution you'd like**
A clear and concise description of what you want to happen.

**Describe alternatives you've considered**
A clear and concise description of any alternative solutions or features you've considered.

**Additional context**
Add any other context or screenshots about the feature request here.
// suppress Key related errors
noExplicitConstructor:*include/vsg/core/ref_ptr.h:45

// suppress C union Key related false positives
unusedStructMember:*include/vsg/introspection/c_interface.h

// suppress the warning about valid C++17 if (init; condition) usage
syntaxError:*include/vsg/core/Inherit.h
syntaxError:*src/vsg/io/AsciiOutput.cpp
syntaxError:*src/vsg/io/AsciiInput.cpp
syntaxError:*src/vsg/io/BinaryOutput.cpp
syntaxError:*src/vsg/io/BinaryInput.cpp
syntaxError:*src/vsg/io/ReaderWriter.cpp
syntaxError:*src/vsg/io/FileSystem.cpp

// suppress the warning about valid C++17 if (init; condition) usage
syntaxError:*include/vsg/utils/CommandLine.h

// suppress warnings about never used variables that are used in .cpp's
unusedStructMember:include/vsg/core/Data.h
#pragma once

/* <editor-fold desc="MIT License">

Copyright(c) 2018 Robert Osfield

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

</editor-fold> */
# Contributor Covenant Code of Conduct

## Our Pledge

In the interest of fostering an open and welcoming environment, we as contributors and maintainers pledge to making participation in our project and our community a harassment-free experience for everyone, regardless of age, body size, disability, ethnicity, gender identity and expression, level of experience, nationality, personal appearance, race, religion, or sexual identity and orientation.

## Our Standards

Examples of behaviour that contributes to creating a positive environment include:

* Using welcoming and inclusive language
* Being respectful of differing viewpoints and experiences
* Gracefully accepting constructive criticism
* Focusing on what is best for the community
* Showing empathy towards other community members

Examples of unacceptable behaviour by participants include:

* The use of sexualized language or imagery and unwelcome sexual attention or advances
* Trolling, insulting/derogatory comments, and personal or political attacks
* Public or private harassment
* Publishing others' private information, such as a physical or electronic address, without explicit permission
* Other conduct which could reasonably be considered inappropriate in a professional setting

## Our Responsibilities

Project maintainers are responsible for clarifying the standards of acceptable behaviour and are expected to take appropriate and fair corrective action in response to any instances of unacceptable behaviour.

Project maintainers have the right and responsibility to remove, edit, or reject comments, commits, code, wiki edits, issues, and other contributions that are not aligned to this Code of Conduct, or to ban temporarily or permanently any contributor for other behaviours that they deem inappropriate, threatening, offensive, or harmful.

## Scope

This Code of Conduct applies both within project spaces and in public spaces when an individual is representing the project or its community. Examples of representing a project or community include using an official project e-mail address, posting via an official social media account, or acting as an appointed representative at an online or offline event. Representation of a project may be further defined and clarified by project maintainers.

## Enforcement

Instances of abusive, harassing, or otherwise unacceptable behaviour may be reported by contacting the project team at robert@openscenegraph.com. The project team will review and investigate all complaints, and will respond in a way that it deems appropriate to the circumstances. The project team is obligated to maintain confidentiality with regard to the reporter of an incident. Further details of specific enforcement policies may be posted separately.

Project maintainers who do not follow or enforce the Code of Conduct in good faith may face temporary or permanent repercussions as determined by other members of the project's leadership.

## Attribution

This Code of Conduct is adapted from the [Contributor Covenant][homepage], version 1.4, available at [http://contributor-covenant.org/version/1/4][version]

[homepage]: http://contributor-covenant.org
[version]: http://contributor-covenant.org/version/1/4/
# How to contribute
Developers can help contribute to the VSG through testing, reporting issues, bug fixing, feature development and creation of tutorials and documentation.

## Report an bug

Please use the Issue tracker on github. We provide two templates, a bug report template and a feature request template to help guide what type of information is useful to us.

## Bug fixes

If you have made a bug fix please make a pull request on github. With the PR please use a descriptive but short title line, followed by a paragraph explaining the bug and changes, with references to the github Issue if one has been raised for it.

## Feature request

If you wish to make a feature request, this can be done via our github Issue tracker. Please be prepared to step forward to help with this feature development, or help fund others to do this feature development. If features are not aligned well with the projects scope and goals then these requests will be closed and a path forward for developing this as a 3rd party development will be suggested.

## Feature development

If you have refinement of existing features or added new feature please a make pull requests.

## In source documentation

In source documentation can be provided in the form of markdown (.MD) files to be found in the docs/ directory, or as doxygen style comments within the header files. Please use a pull request.

## 3rd Party tutorials, documentation, libraries and program

If you have written documentation, tutorials, libraries or programs and wish to inform developers about then please considering adding details about them to the docs/3rdParty files and generate a pull request.
# Design Principles and Philosophy

> *"Successful Software Lives For Ever"*

This document introduces the design principles/philosophy of the project lead Robert Osfield.  The principles draw upon the experience of being project lead of the [OpenSceneGraph](https://www.openscenegraph.org) and lessons learned from the real-time compute graphics, C++, and open source/free software communities.

First lets break down the opening phrase, *"Successful Software Lives For Ever"*, one I coined for a training course over a decade ago:

* What is *"Success Software"* : Software that is useful and reliable enough for developers and/or users to adopt it as a part of their work or personal lives and rely upon it to live for as long as they need it.

* How long is *"For Ever"* : Long enough that time during maintenance and evolution is significantly longer than initial time to develop the first stable release. Software that is unreliable, hard to maintain and evolve becomes unsustainable in the long term, it looses it's relevance because of it and fails. Success demands good design, implementation and responsive curation over many years.


For the OpenSceneGraph project what made it a success was it achieved *performance* levels that competed well with the best proprietary and open source scene graphs, and was well designed enough to help developers be *Productive* over long term application development and deployment. Responsive of contributors to support the community has also been crucial for the OpenSceneGraph remaining relevant to real-time graphics application developers for nearly two decades.

Technology moves on, Vulkan is displacing OpenGL as the graphics API of choice for high performance cross platform graphics development.  C++ has begun evolving more rapidly and now C++17 offers many features that make applications faster, more robust and easier to develop and maintain. Ideas on scene graphs have also advanced, a well designed clean room scene graph has the potential for improving graphics and compute performance and developer productivity beyond the previous start of art.  The VulkanSceneGraph project goal is to embody the potential of Vulkan and modern C++ and create middle-ware for the next generation of graphics applications, and for it to remain a valued tool for the next decade and beyond.

There are two broad areas that will determine the success of the VulkanSceneGraph : [***Performance***](#performance) and [***Productivity***](#productivity).  The rest of this document will break these areas down and discuss the design principles that will aim to deliver in these areas. I'll coin another phrase to emphasise how both are equally crucial to success:

> ***"You live for Performance, but die a slow, painful death without Productivity"***

### Making allowances for living at the *Bleeding Edge*

The below discussion outlines what is guiding the path forward - it's our compass heading, as of the fall of 2018, it's still very early days so the code is in flux and is not ready for wide use out in the industry. During this phase of rapid development early adopters will have to accept lower Performance and Productivity associated with working with alpha software.

Early adopters are hugely important for the success of the project, the extra work you have to put in will benefit us all in helping shape and refine the software so that it's fit for purpose by the time we reach our first stable release and genuinely deliver on what we are striving for.


## Performance

Performance can be mean different things to different applications, some applications maximum frame-rate may be the goal, others avoiding frame drops when targetting a fixed frame rate is critical, for VR minimizing latency is crucial, while others may look to minimize power demands required to achieve a target frame rate and visual quality. In all these cases overall efficiency of taking a representation of a 2D or 3D world and rendering it on a GPU is the key determiner, the lower overhead on the complete computer system the better the efficiency and potential performance.

The stages of work that are crucial to undertake efficiently with a graphics application are:

1. Creation and destructions of scenes, paged scenes must run in a parallel to rendering
1. Updating the scene(s)
1. Cull traversal - view frustum etc. culling to generate a dispatch graph
1. Dispatch traversal - sending the data in the dispatch graph to the GPU(s)
1. Graphics Processing - graphics and compute work done on the GPU(s)

The adoption of Vulkan provides a significant reduction in CPU overhead with dispatching data compared to OpenGL and Direct3D(prior to 11), this immediately reduces the cost of stage 4 - dispatch traversal. However, the benefits are only fully realized if the scene graph overhead involved in dispatch traversal stage and cost of paging, updating and cull traversal are proportionally reduced. To deliver on all the potential benefits that Vulkan has the scene graph must take similar strides forwards in reducing overheads and improving efficiency.

The principles used as a guide to achieving efficiency include:

* Benchmarking is fundamental to determining performance bottlenecks and qualifying that changes are effective - beware of premature optimization!
* Minimize memory footprint of scene graph objects
* Avoid non essential data storage
* Pack commonly accessed data for cache friendly access
* Avoid non essential conditionals
* Choose coding techniques that are friendly to compiler optimization and CPU parallelism

An example of minimizing footprint, non essential conditions and data storage has already impacted the design and implementation can be seen in minimizing the size of the core [vsg::Object](../../include/vsg/core/Object.h) that is backbone of the scene graph by moving all optional data out into an optional [vsg::Auxiliary](../../include/vsg/core/Auxiliary.h) class.  This change reduces the size of vsg::Object to 24 bytes, compared to the OpenSceneGraph's osg::Object class that is 72 bytes.  The vsg::Node class adds no extra data members overhead so remains at 24 bytes, while the OpenSceneGraph's osg::Node class footprint is 20 bytes.  These memory footprint reductions are carried over to all objects in the scene graph.

Scene graphs are fundamentally a graph of objects connected by pointers between those objects.  The size of those objects is inextricably connected to the size of pointers. C++11 onwards provides the std::shared_ptr<> which on 64-bit systems has a size of 16 bytes, while the VSG's intrusive reference counting enables the vsg::ref_ptr<> to have a size of 8 bytes.  In experiments with creation of a quad tree scene graph using std::shared_ptr<> vs vsg:::ref_ptr<>, the shared_ptr<> results in a 75% more memory used overall, and 65% slower traversal speeds. This significant difference illustrates that one should not assume that C++ core features are always the most efficient tool.

Traversals of a scene graph and dispatch graphs are the main operations that a scene graph undertakes each frame, cache misses and lowering the cycle overhead per object visited is key to reducing traversal times.  The memory footprint reduction immediately reduces the number of page faults that occur and avoiding non essential conditionals provides a second improvement as it reduces number of cycles required per object visited.

The way that avoiding non essential conditionals has been addressed is to drop the NodeMask and TraversalMode parameters that are found in the OpenSceneGraph's osg::Node and osg::NodeVisitor respectively.  When NodeMask functionality is required in a scene graph the task will fall to a MaskGroup that will have a local mask and undertake the conditional during traversals that is required, so that only scene graphs that require a mask will pay the penalty for it.  Decision of what type of traversal to undertake is also moved to the Visitor subclass rather than the Visitor base class.  Finally the NodePath that is automatically accumulated by the OpenSceneGraph's NodeVisitor is also dispensed with, if Visitor implementation require this functionality then they are left to implement it.

To test the effectiveness of these design differences a test program, vsgroups (found in vsgFrameworks project) was used. The results of these seemingly small design changes over the OpenSceneGraph have a dramatic improvement in performance.

* quad tree construction and destruction times are 3 x faster in VSG vs OSG.
* quad tree traversal is 6 to 10 x faster in VSG vs OSG (depends upon Node and Visitor type.)

The reason for this dramatic improvement is due to:

* significant reduction in page faults due to memory footprint reduction
* reduction in conditionals, reducing number of instructions per object visited and improving CPU ability to prefetch and speculative execute
* improvement in number of instructions per cycle that the CPU can sustain

These are benefits even before we compared Vulkan vs OpenGL improvements, it's still too early in the projects life to be able to compare on realistic scenes, as things progress we'll provide more results.  We can be confident that the improvements in efficiency of the scene graph traversals combined with the efficiency of Vulkan will substantially improve the ability to have large and complex worlds, and reduce the power over-head required to achieve a specific level of visual quality.


## Productivity

The tools and middle-ware you choose for your projects are key determinants of the amount of work needed to achieve required functionality and to maintain and enhance that functionality through the software's life. The approach that we take within the VulkanSceneGraph project not only determines how productive it's own development is, it will have a great influence on how productive users of it will be. The following are principles that we are adopting to help us all achieve better productivity.

### General project development principles that aid Productivity:

* Use Best Practices that have been established in the wider industry:
    * [FOSS Best Practices](https://github.com/coreinfrastructure/best-practices-badge/blob/master/doc/criteria.md) are used as a guide of how to organize and maintain the project
    * [CppCoreGuidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines) are used as a guide to design and implementation
* Use C++17 to benefit from the improvements in C++ that result in cleaner and more maintainable code
    * Use features and idioms that make sense for a scene graph
    * Don't use features because they are new, trendy, or the "standard" way of doing things - they must make the code cleaner and more maintainable without hindering performance (i.e don't use std::shared_ptr<> as it has huge performance penalty.)
    * Don't make assumptions, implement and benchmark.
* Use CMake for cross-platform as it's effective and the de-facto standard build tool used in real-time graphics industry, when implementing scripts make them work in standard ways that developers will be familiar with
* Minimize dependencies for the VukanSceneGraph library to ensure it's quick and easy to build:
    * C++17
    * Vulkan
    * CMake
    * Native Windowing
* Use github as it's widely used, and structure the repository in ways that are familiar to others and work well with standard tools so no need to learn new tools & workflows
* Create documentation to help others use the VSG, and contribute to the VSG development
* Build a community to enable developers to help each other and coordinate testing, debugging and feature development, and to share best practice
* Work towards building a cohesive collection of companion libraries and high level frameworks on-top of the VSG to enable developers to use high level, domain specific frameworks and tools


### Scene Graph related principles that aid Productivity:

* ***"minimal and complete"*** : VulkanSceneGraph library to be focused on creating and traversing a scene graph and basic rendering in a viewer.
    * Additional libraries and frameworks to provide domain specific types of functionality, such as 3rd party data loaders to be provided by a family of supplementary libraries.
    * Developers to just pick the libraries they need from the family and only inherit the 3rd party dependencies they need for the project they have.
* Meaningful encapsulation of Vulkan
    * Vulkan is fast and flexible, but it is also long winded to implement basic functionality - it can take 1500 lines of code just to get a depth sorted quads on screen!
    * Simply wrapping Vulkan within C++ classes doesn't address what developers actually need
    * Developers need higher level functionality to manage their scenes and computational workflow
    * Need to encapsulate Vulkan in a way that reduces the work required to set up and use Vulkan
    * Encapsulation of Vulkan to fit coherently in with how it's used in a scene graph
    * Scene graph design and implementation must also fit with how Vulkan works - a symbiotic relationship
* ***""If it ain't broke, don't fix it."*** : A number of approaches used in OpenSceneGraph project remain relevant to the new scene graph:
    * Visitor pattern variation that couples type safe operation and scene graph traversals
    * Multi-pass, multi-stage rendering
    * Viewer, View and Camera and Windowing relationships
    * Intrusive reference counting
* Good baseline *Performance* opens the door to better *Productivity* : The lower overheads achieved with the new scene graph and Vulkan reduces the need for complex application level optimizations - to hit frame rate or latency targets less work needs to be done to workaround CPU bottlenecks previously associated with scene graph traversal and GL dispatch.

### Software quality principles that aid Productivity:

* Short cuts in code quality are *"Fools Gold"* when it comes to Productivity
* Take pride in clarity and efficiency of code
* Take time to understand and appreciate the code and techniques used by others - such as CppCoreGuidelines
* You want your work to be a *Success*, so write it like it'll *Live Forever* (and be looked at forever:-)
* If a problem exists, be honest about it, solve it right way and learn from the error and solution found
* *"Prepare to throw one away, you will anyhow"* (source : Mythical Man Month): don't get too wrapped up solving all the worlds problems in one place, solve the problems you have at hand and test the results, and if in the future it's found to be insufficient then refactor/rewrite it with everything you've learnt and now need to achieve
* Make use of static and dynamic analysis tools straightforward and a regular practice for developers and users


# High Level Design Decisions

**Project name:** VulkanSceneGraph preferred, may need to use VkSceneGraph if permission from Khronos is not secured.

**Language:** C++17 minimum standard.

**Build tool:** lead choice CMake due to familiarity and market penetration.

**Source code control:** git hosted on github.

**Maths :** local GLSL style [maths](../../include/vsg/maths/) classes, inspired by GLSL, GLM and the Vulkan conventions.

**Windowing:** local native Windowing integrated with core VSG library, with ability to use 3rd party Windowing (short term use GLFW to get started quickly.)

**Vulkan integration:** Aim for coherent naming and granularity as underlying Vulkan API

* lightweight [local C++ encapsulation](../../include/vsg/vk) of Vulkan objects, naming and style inspired by Vulkan C API.
* Provide convenient and robust setup and clean of resources.
* Standard naming VkFeature -> vsg::Feature in include/vsg/vk/Feature
* Cmd naming VkCmdFeature -> vsg::Feature, sub-classed from [vsg::Command](../../include/vsg/vk/Command.h)
* State VkCmdFeature -> vsg::Feature, sub-classed from vsg::StateComponent and aggregated within a [vsg::StateGroup](../../include/vsg/nodes/StateGroup.h) node.


**Single library:** all core, maths, nodes, utilities, vulkan and viewer provided in libvsg library, can be either be used as static or dynamic library.

**Namespace:** vsg used for all categories of functionality within the libvsg library.

**Headers:** .h used for public classes/functions

Categories of functionality placed in appropriately named subdirectories i.e.

* [include/vsg/core](../../include/vsg/core/)/Object.h
* [include/vsg/nodes/](../../include/vsg/nodes/)Group.h
* [include/vsg/vk/](../../include/vsg/vk/)Instance.h
For convenience high level include/vsg/all.h head to includes all vsg/*/*.h

**Source:** .cpp extension used

Categories of functionality placed in appropriate named subdirectories i.e.

* [src/vsg/core/](../../src/vsg/core/)Visitor.cpp
* [src/vsg/viewer/](../../src/vsg/viewer/)Viewer.cpp


**Memory:** To address the main scene graph performance bottleneck have a general goal of improving cache coherency and lowering memory bandwidth load.

Intrusive reference counting twice as memory efficient as std::shared_ptr<>, and results in ~50% better traversals speeds. Use [vsg::ref_ptr<>](../../include/vsg/core/ref_ptr.h), [vsg::observer_ptr<>](../../include/vsg/core/observer_ptr.h) and vsg::Object.

Use std::atomic to provide efficient, thread safe reference counts

To minimize the size of majority of internal scene graph nodes and leave nodes the ancillary data that only a few objects required are moved out of the base vsg::Object/Node classes into an [vsg::Auxiliary](../../include/vsg/core/Auxiliary.h) object.

To enable greater control over memory management [vsg::Allocator](../../include/vsg/core/Allocator.h) class to enable application to control how the scene graph allocates and deletes memory.

**Unification:**
All vsg::Object support intrusive reference counting and meta data support All vsg::Object support type safe query via [vsg::Visitor](../../include/vsg/core/Visitor.h) and [vsg::ConstVisitor](../../include/vsg/core/ConstVisitor.h)

All uniform and vertex array data can be handled via the [Data](../../include/vsg/core/Data.h) interface Single value data via the [vsg::Value](](../../include/vsg/core/Value.h)) template Array data via the [vsg::Array](](../../include/vsg/core/Array.h)) template classes

The main scene graph and the rendering back-ends command graph utilize the same scene graph hierarchy.

Vulkan [Compute](../../include/vsg/vk/ComputePipeline.h) and [Graphics](../../include/vsg/vk/GraphicsPipeline.h) to be supported with the same Vulkan wrappers, scene graph and command graph hierarchies.


**Usage models:** Application developers will be able to dispatch data directly to Vulkan using the VSG’s Vulkan wrappers in a form of an immediate mode, creating their own command graphs that use standard vsg command visitors or their own custom visitors, through to using visitor to cull the main scene graph down to a command graph each frame and dispatching this vulkan.


**Introspection:** Not explored during Exploration Phase so will need to be addressed in future. Aim to provide introspection/reflection for all core scene graph objects to provide support for reading/writing scene graph objects and open the door to scripting.


**IO:** Support for loading 3rd party images and 3D models is currently deemed out of scope of the core libvsg library. Only IO supported will be via the native scene graph objects support for reflection. This IO support will enable scene graphs, images and shaders to read and written without any additional libraries.


Support for 3rd party images, 3D models and shaders will be provided by add
on libraries. To aid with porting of OpenSceneGraph application a osg2vsg
library will be developed so that all loaders that the OpenSceneGraph has will
be available.  These 3rd party on libraries providing image. 3D model and shaders will form an important part of testing of the VSG project as it evolves and are expected to develop in conjunction with the VSG project.
# 3rd Party Resources of interest

## C++ Core Guidelines etc.

* [C++ Core Guidelines](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)
* [CppCon Resources](https://github.com/cppcon)
* [GNU Reserved-Names](https://www.gnu.org/software/libc/manual/html_node/Reserved-Names.html)

## Best Practices
* [Best Practices Criteria for Free/Libre and Open Source Software (FLOSS)](https://github.com/coreinfrastructure/best-practices-badge/blob/master/doc/criteria.md)
* [include-what-you-use tool](https://include-what-you-use.org/)
* [clang address sanitizer](https://clang.llvm.org/docs/AddressSanitizer.html)
* [clang thread sanitizer](https://clang.llvm.org/docs/ThreadSanitizer.html)
* [clang memory sanitizer](https://clang.llvm.org/docs/MemorySanitizer.html)

## Package managers
* [conan](https://conan.io/), [github](https://github.com/conan-io/conan)
* [hunter](https://docs.hunter.sh/en/latest/), [github](https://github.com/ruslo/hunter)
* [vcpkg](https://github.com/Microsoft/vcpkg)

## Documentation tools
* [doxygen](http://www.doxygen.org/)
* [cldoc](http://jessevdk.github.io/cldoc/)
* [DoxyPress](http://www.copperspice.com/documentation-doxypress.html)
* [Using github](http://stat545.com/bit006_github-browsability-wins.html) and [example of images, csv and pdf rendering](https://github.com/kbroman/FruitSnacks)
* [GitHub Pages](https://pages.github.com/)

## Runtime analysis tools
* [chrome://tracer](https://www.chromium.org/developers/how-tos/trace-event-profiling-tool), [gettings started](https://google.github.io/tracing-framework/getting-started.html#installing), [JSON format](https://docs.google.com/document/d/1CvAClvFfyA5R-PhYUmn5OOQtYMH4h6I0nSsKchNAySU/preview#heading=h.5n45avt6fg8n)

## Video presentations
* [GDC 2016: High-performance, Low-Overhead Rendering with OpenGL and Vulkan](https://www.youtube.com/watch?v=PPWysKFHq9c)
* [C++Now 2017: Daniel Pfeifer “Effective CMake"]()https://www.youtube.com/watch?v=bsXLMQ6WgIk)

## Tutorials
* [Vulkan Tutorial](https://vulkan-tutorial.com/)
* [2017 Khronos UK Vulkanised  presentations](https://www.khronos.org/developers/library/2017-khronos-uk-vulkanised)
* [Multi-threading in Vulcan](https://community.arm.com/graphics/b/blog/posts/multi-threading-in-vulkan)

## Vulkan Presentations
* [Keeping-your-GPU-fed](https://www.khronos.org/assets/uploads/developers/library/2016-vulkan-devday-uk/7-Keeping-your-GPU-fed.pdf)
* [Samsung Vulkan Usage Recommendations](https://developer.samsung.com/game/usage)
* [AMD Vulkan Device Memory](https://gpuopen.com/vulkan-device-memory/)
* [NVIDIA Vulkan Memory management](https://developer.nvidia.com/vulkan-memory-management)
* [Vulkan Spec](https://renderdoc.org/vkspec_chunked/index.html)
* [Vulkan Shader Resource Binding](https://developer.nvidia.com/vulkan-shader-resource-binding)
* [Lessons Learned While Building a Vulkan Material System](http://kylehalladay.com/blog/tutorial/2017/11/27/Vulkan-Material-System.html)

## Vulkan based projects
* [Pumex](https://github.com/pumexx/pumex)
* [VkHLF NVidia's C++ layer on-top of Vulkan](https://github.com/nvpro-pipeline/VkHLF)
* [Vulkan Memory Allocator](https://github.com/GPUOpen-LibrariesAndSDKs/VulkanMemoryAllocator)

## Maths
* [Rotors for angles](http://marctenbosch.com/quaternions/)
* [GLM](http://glm.g-truc.net) - GLSL style maths classes/functions
* [GMTL](http://ggt.sourceforge.net/html/main.html)
* [GLSL data types](https://www.khronos.org/opengl/wiki/Data_Type_GLSL)

## Image and 3D model loaders
* [Assimp](https://github.com/assimp/assimp) 3D models loading
* [GLI](http://gli.g-truc.net) Loading/manipulating images/textures
* [STB](https://github.com/nothings/stb) stb_image.h etc.
* [DevIL](http://openil.sourceforge.net/) DevIL image library, [repo](https://github.com/DentonW/DevIL)
* [FreeImage] (http://freeimage.sourceforge.net/) FreeImage image library (GPLv2/GPLv3/FreeImage License), [repo] (https://sourceforge.net/p/freeimage/code/) 

## Introspection
* [Cereal](https://github.com/USCiLab/cereal)
* [cson - C++ Simple Object Notation](https://github.com/snawaz/cson)
* [A Flexible Reflection System in C++: Part 1](http://preshing.com/20180116/a-primitive-reflection-system-in-cpp-part-1/ )
* [A Flexible Reflection System in C++: Part 2](http://preshing.com/20180124/a-flexible-reflection-system-in-cpp-part-2/)
* [Small example of use of std::make_type, std::ref etc.](http://coliru.stacked-crooked.com/a/25638f2ebc6424bf)

## 3rd party scene graphs
* Paul Martz's [JAG](https://github.com/pmartz/jag-3d/)
* Jeremy Moles' Heirograph scene graph (need reference)

## Suggestions in osg-users ML/forum post from Paweł Księżopolski
Vulkan specification is the most comprehensive source of knowledge about
the API - it's long but it is a must for any developer taking it seriously :

* [Vulkan Specification](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html)

As for the books I recommend "Vulkan Programming Guide" written
by Graham Sellers. Sometime ago it was even available for free in
certain countries on Google Play bookstore :

* [Vulkan Programming Guide](http://www.vulkanprogrammingguide.com/)

Active forums discussing Vulkan include Khronos forums :

* [Khronos Vulkan Discussion Forum](https://forums.khronos.org/forumdisplay.php/114-Vulkan-High-Efficiency-GPU-Graphics-and-Compute)

and Vulkan subreddit :

 * [Vulkan Reddit](https://www.reddit.com/r/vulkan/)

Sascha Willems wrote a good set of Vulkan demos, that show how to
implement certain features :

* [Vulkan Demos](https://github.com/SaschaWillems/Vulkan)
* [Sascha Willems website](https://www.saschawillems.de/)
* [JHerico's Vukan examples](https://github.com/jherico/Vulkan)
* [gliterop example](https://github.com/jherico/Vulkan/tree/cpp/examples/glinterop)

Vulkan Compute examples:

* [vulkan_minimal_compute](https://github.com/Erkaman/vulkan_minimal_compute)

There's also a curated list of useful links to everything
associated with Vulkan :

* [Awesome List of Vulkan resources](https://github.com/vinjn/awesome-vulkan)

# Areas of Interest during Exploration Phase

## General

* Selection of Open Source License
* Project websites
* Community mailing list/forum
* Social media
* Testing frameworks/approach/projects - [SceneGraphTestBed](https://github.com/openscenegraph/SceneGraphTestBed)
* Build tools
  * [CMake](https://cmake.org/)
  * [xmake](https://xmake.io/#/)

## Vulkan

* Setup and Configuration
* State and geometry data
  * Creation of buffers
  * Uniforms
  * Textures
  * Arrays
  * Primitives
* Shaders
  * tools for offline and runtime .glsl -> SPIR-V
  * runtime shader compilation options
* Presentation of graphics
* Threading
* Synchronization

## C++
* Features and availability of C++ 11, 14 and 17
* Threading
* Containers
* Algorithms
* Memory management
* Templates
* Lambda
* Style Guide

## Core class
* Memory
  * ref_ptr
  * Object
  * Backbone data - local data used during standard traversals/operations
  * Extra - data used rarely : parents, observers, user data
* Introspection
  * Wrappers
  * Serialization
  * I/O
* Threading
  * C++ now has threading but no Affinity
  * Thread pools

## Scene Graph
* Scope out the minimal set of Node classes required
  * NullNode to avoiding the need for if (!node) doSomething
  * Fixed size vs variable size Containers in Groups etc.
  * Level of Detail
  * CullNode (shift bounding volumes from all nodes to specialized node?)
  * MaskNode (shift node mask checks from all nodes to specialized node?)
  *Cameras
* Traversal
  * Visitor Pattern
  * Possibilities for inlining vs virtual functions
  * RenderTraversal
  * ComputeTraversal
  * UpdateTraversal
  * EventTraversal
  * Multi-pass and Multi-stage rendering control
* State
  * Buffers
  * Uniforms
  * Textures
  * Arrays
  * Primitives
  * Shaders
  * Shader composition
* Threading
  * Traversals
  * Database paging

## Viewer
* Window creation
* Vulkan initialization and synchronization
* Presentation of graphics, swap management
* Threading
* Single view vs multi view

## Interoperability
* Converting scene graph data from OpenSceneGraph data to leverages loaders
* Rendering Vulkan graphics within a OpenGL graphics context

# VSG Exploration Phase Report
This document discusses the work carried out during the Exploration Phase and conclusions and results from this work.  Links to 3rd party resources used are included inline with this document, click on highlighted keywords to follow links.

## Original Plan for topics to be tackled during exploration phase:
1. Gain familiarity and experiment with Vulkan API and associated tools such as glslang, SPIR-V Tools etc.
2. Develop an intuitive, flexible and high performing conceptual and class mapping for Vulkan functionality into the Application and Scene Graph domains.
3. Experiment with different approaches to core scene graph design and implementation to find out which approaches deliver the best balance between performance, flexibility and scalability, whilst providing a clean and intuitive design and implementation.
4. Explore the scope of functionality to be placed in the core VulkanSceneGraph library/project and functionality that should be provided by additional/3rd party libraries or frameworks.
5. Gain familiarity and experiment with C++11, C++14 and C++17 features and make choices which provide the best balance between a clean scene graph design, implementation and compiler compatibility.
6. Test build tool options CMake and xmake to inform decision which tools to use.


The document will discuss the work and findings from each of these areas, numbering of sections follows the above guide from the original plan. A final section in this document will provide:


7. [Exploration Conclusions](#7-exploration-phase-conclusions)
8. [High Level Design Decisions](../Design/HighLevelDesignDecisions.md)

## VulkanPlayground repository and successors:
To provide a base for experimental work during the exploration a project was created on github : [VulkanPlayground](
https://github.com/vsg-dev/VulkanPlayground) which has been kept a private repository.

The VulkanPlayground is meant as a throwaway prototyping repository rather than an alpha version of the final scene graph project. The project contains:

* prototype vsg library that contains:
    * core : base classes and templates, such as Object, Array, ref_ptr
    * nodes : scene graph classes  Node, Group, StateGroup, LOD classes
    * maths: vec2, vec3, vec4 and mat4 template classes
    * vk : Vulkan wrapper classes
   * viewer :  Viewer, Window and GraphicsStage classes
* prototype osg2vsg utility library for loading images using the OSG and converting to vsg/Vulkan objects
* Test-bed applications that experiment with various aspects of the vsg prototype

Now that the Exploration Phase is completed the work on VulkanPlayground has fed into the Prototype Phase, with the repository being broken up into three component repositories that are publicly available and public under the MIT License:

* [VulkanSceneGraphPrototype](https://github.com/vsg-dev/VulkanSceneGraphPrototype) the core scene graph
* [osg2vsg](https://github.com/vsg-dev/osg2vsg) helper library to read/writes images using the OSG
* [vsgFramework](https://github.com/vsg-dev/vsgFramework) experiment with building applications and libraries


---

## 1. Gain familiarity and experiment with Vulkan API and tools
The process of familiarization with Vulkan and associated tools was progressed by working through the VulkanTutorial and vulkan_minimal_compute tutorials, remapping the functionality that these tutorials provided into reusable C++ class wrappers for Vulkan functionality.  The Vulkan Programming Guide book and Khronos online reference guides for Vulkan were used to fill out knowledge of the API and how it functioned.


GLFW was used for creating Vulkan windows and glslang used to convert GLSL Vulkan compatible shaders into SPIRV .spv shaders usable by Vulkan.


The work on following the VulkanTutorial can be found in the vsgdraw example, and vulkan_minimal_compute can be found in the vsgcompute test-bed applications. Both of these applications provide similar functionality as the original examples, but do so by using the prototype vsg classes. The benefit from the vsg classes is that the vsgdraw.cpp and vsgcompute.cpp are less than 1/5th the size of the original tutorials that they are mapped from. The vsg versions are also more linear in their layout and should be easier to follow than the originals that they recreate.


The vsgdraw test-bed using some basic graph functionality it is very simplistic compared to what the final scene graph will provide - there is no culling, a graph is used just to hang state and command functionality in the form of a command graph that is traversed to dispatch to Vulkan.


The vsgcompute test-bed uses the vsg Vulkan wrappers directly as immediate mode, setting up and dispatching data and commands to Vulkan directly.

---

## 2. Develop class mapping for Vulkan functionality
Two of the three months of the Exploration Phase have been dedicated to learning and experimenting with Vulkan. Vulkan requires a great deal of setup to do basic things so progress in this area was been slow. The current Vulkan encapsulation that can be found in VulkanPlayground/include/vsg/vk and src/vsg/vk are functional and usable as is, but should be considered a first pass implementation.


The current encapsulation of Vulkan has followed the principle of one C++ class to each key Vulkan object type, so VkPipeline is wrapped up in vsg::Pipeline class found in include/vsg/vk/Pipeline etc.


Initial work has been done on exposing the Vulkan functionality within the scene graph and viewers. This work is ongoing and will not be resolvable within the original three month Exploration Phase. Areas in Vulkan left to be resolved are how multi-threading and multi-device support will be handled, and by what means the Vulkan objects will be connected to the scene, command graphs and viewers.

---

## 3. Exploration of core scene graph design and implementation
The core functionality such as memory management, type safe object operations, extensible object properties, maths functionality and memory footprint were fleshed out in a series of classes within the prototype vsg library and the application test-beds. The general approach has been to create core classes that are smaller in memory footprint, more flexible and coherent than their counterparts within the OpenSceneGraph.

### 3.1 Efficient memory management
The smaller memory footprint is a key part of addressing the memory bandwidth that is the main bottleneck for scene graph traversals.  Several approaches have been tested to address memory footprint and cache coherency:


* Move properties that aren’t used on all Objects out into an optional Ancillary class
* Provided option for using fixed sized arrays to improve cache coherency


The osggroups test-bed application provides a comparison of different approaches within the VSG as well as comparing to OSG equivalents testing creation, destruction and traversal of quad tree test scene graphs. This test-bed illustrates how time to create, delete and traverse are all related to the memory footprint. Findings are:


* Fixed sized vsg::QuadGroup requires 56 bytes vs 264 for osg::Group with 4 children
* vsg::QuadGroup, time to create is 1/5th of osg::Group with 4 children
* Traversals can be up to 10 times faster than OpenSceneGraph


Smart pointer usage also has a profound effect on memory footprint and hence performance. The osgpointer test-bed compares use a intrusive reference counting (vsg::ref_ptr) vs using C++11’s std::shared_ptr.  On 64 bit Linux systems vsg::ref_ptr<> is 8 bytes in size vs std::shared_ptr<> that is 16 bytes.  The internal nodes of a scene graph use smart pointers to hold references to their children so also are impacted by the smart pointer size.  vsg::QuadGroup using ref_ptr<> is 56 bytes vs 104 bytes required for the equivalent fixed size Group using shared_ptr<>. This test illustrates how std::shared_ptr<> is a significant step back compared to the intrusive reference counting and should not be used in any performance sensitive areas of the VSG project.

### 3.2 Improving Flexibility and coherence
The OpenSceneGraph’s long life has meant that features have been added over time with multiple class hierarchies being used for different purposes. For instance the scene graph is distinct to the rendering back-end graphs, uniforms are different to arrays, traversal and type safe operations on object also have different mechanisms.


To address traversal and type safe operations in a more generic way the osg::NodeVisitor (and other equivalents within the OSG) are replaced by a single vsg::Visitor base class that all vsg::Objects can be interfaced with.


Uniforms and vertex arrays are also supported using the same vsg::Data base class with vsg::Value and vsg::Array template classes to provide wrapping of single value or arrays of values respectively.


The lightweight nodes within the scene graph also mean that the cost of creating companion graphs is lower so there is no need for specialized graphs as is done with the OSG. The same node classes can now be used for both the main scene graph and the rendering back-end which is done with a command graph - which is essentially a scene graph used to hold data and commands that will be dispatched into the Vulkan Command Buffers.

---

## 4. Scope of core VulkanSceneGraph vs 3rd party libraries
There are a range of 3rd party libraries that could be useful and a range of ways that they might be integrated:

* used as external dependencies
* included within VSG source code as git submodules
* cherry-picked source code or
* used as inspiration for design and implementations written as original work within the VSG project


Possible areas where 3rd party libraries could be utilized include:

1. Maths
2. Windowing
3. Vulkan wrappers


Each of these areas we review the 3rd party libraries to look at their relevance and usefulness, and where useful how best to use them.  As a general principle external dependencies can reduce the amount of work required in the core VSG project, but increase the work required to assemble the required dependencies and has the potential for creating an incoherent user experience with different dependencies using their own design style and tools.


Creating this same functionality directly ourselves offers the opportunity of creating a coherent design for all features and minimizing the work required for assembling dependencies, with the downside that all locally implemented features must be designed, implemented, tested, debugged and maintained ourselves.

### 4.1 Maths
To improve the coherence between the VSG and Vulkan’s use of GLSL the plan is to use the same naming and conventions as GLSL. The GLM library fulfils this goal so has been reviewed with consideration of using it as 3rd party dependencies.


GLM is well established, this is both a positive and a negative. It is likely to be well tested across platforms and should be reliable, it’s design and implementation follow GLSL equivalents very closely to a high level providing a coherent experience between the C++ application domain and the shaders passed to the graphics hardware.


The disadvantage of GLM is that is very large, 46913 lines of code in headers, and the majority of it’s functionality will be rarely used by a scene graph user. GLM is also written for OpenGL, while GLSL is usable with Vulkan, the application level elements and conventions are not all compatible. The depth range and vertical orientation of clip space are different between OpenGL and Vulkan so require GLM results to be adapted so they can be used with Vulkan - the projection matrix setup is an example of this.


GLM is used by a number of Vulkan based projects, for instance NVidia’s VkHLF, vulkan-cpp-library pumex, the VulkanTutorial all use GLM.


When considering whether to create local classes vs using 3rd party dependencies a key aspect is just how much work would be required to create the subset of functionality that the VSG requires. The key elements for the VSG are vec2, vec3, vec4 and mat4 classes, so as an experiment VSG template classes for each of these were implemented, enabling the standard float variations as well as double and integer versions are very local cost. GLM provide a few design/implementation pointers that helped in this work. The total code base for this functionality is presently just 429 lines of code (found in VulkanPlayground/include/vsg/maths). This is 1/100th of the code base of GLM.  These locally created classes were also written to be directly compatible with Vulkan’s clip space conventions so no application level adaptation is required.


The prototype maths classes provided in vsg/maths are still very basic, it’s likely that the total code base dedicated to this will need to more than double in size. It will however remain well below the footprint of GLM. Experience with maths classes in the OSG suggests that once written they tend to be very easy to maintain so handling this functionality within the VSG project will not be burdensome.


For the VSG project is looks best to provide our own maths classes, it gives us the ability to be fully coherent with how Vulkan works and with the conventions that will be used in the rest of the VSG, and provides a small code footprint for users to navigate and learn, and avoids adding a large 3rd party dependency.


### 4.2 Windowing
The work carried out in replicating the VulkanTutorial used the same GLFW library the the VulkanTutorial uses to create a Window and associated Vulkan surface. GLFW is a C library and requires initialization and clean up in a particular order controlled at the application level.


To make the window creation and clean up easier GLFW_Window and GLFW_Instance classes were written to provide a C++ interface and an automatic means of clean up, decoupling the test-bed applications from having to handle this task. This functionality was eventually wrapped up inside the prototype vsg library completely so the public vsg interface is now entirely agnostic of windowing library used to create the windows. The total GLFW codebase is presently 37,246 lines of code. GLFW is licensed under zlib License.


Another Windowing library that provides Vulkan support is WSI-Window. This is written specifically for Vulkan in C++ and has Windows, Linux and Android support. Feature wise WSI-Window is a possibility, however, the style of WSI-Window interface is not coherent with Vulkan, or VSG work so far, and some elements of the implementation are somewhat odd. WSI-Window codebase is currently 3,679 lines of code. WSI-Windows is licensed under Apache License.


Another reference for Windowing is pumex (a C++ rendering based framework based on Vulkan). It provides it’s own local Windows and Unix windowing implementations which are very small - just 423 lines of code for Win32, and 403 for Xcb (X11/Unix). Pumex is licensed under the MIT License.


Paweł Księżopolski, the author of Pumex, is a previous contributor to the OpenSceneGraph project and I believe remains an OpenSceneGraph user in his professional career. Pumex is probably the closest any 3rd party project has come to delivering what the VSG aims to provide, so is technically a competitor, but I am optimistic that Pawel will view our work on VSG favourably and may wish to collaborate and share work.


The small size of WSI-Window and in particular the tiny size of Windowing support in pumex provides encouragement that implementation native Windowing within the VSG will not be a large task. We can either learn form or possibly even share code directly for the implementation side.


To provide the most coherent user experience the approach for the VSG will be:

* Provide a platform agnostic public interface to creating/destroying Windows and handling events
* Provide native windowing implementations for all the major platforms - the implementations would be internal to the VSG library, either directly with source code or by linking to 3rd party libraries. First pass would be linking to 3rd party library, then moving source code internally to keep dependencies simple.
* Public interface to Windowing and Events need to be adaptable to 3rd party windowing libraries such as Qt etc.

### 4.3 Vulkan wrappers
The main Vulkan headers are all C headers that contain functions to create and destroy objects and functions dispatch commands, as well as structs used to pack properties used to setup the Vulkan objects and control the commands, queues etc. Using Vulkan C headers directly can result in large amount of setup code and careful management of the lifetime of resources.


There are a series of C++ headers/libraries that encapsulate the Vulkan C objects and functions and provide additional type safety or features. Each of these C++ wrappers have their own advantages and disadvantages.


The vulkan.hpp header is an auto-generated C++11 compatible wrapper for vulkan.h. To quote directly the description of vulkan:


“The goal of the Vulkan-Hpp is to provide header only C++ bindings for the Vulkan C API to improve the developers Vulkan experience without introducing CPU runtime cost. It adds features like type safety for enums and bitfields, STL container support, exceptions and simple enumerations.”


The vulkan.hpp in the 1.1.82.0 release of the VulkanSDK is 45177 lines of code.  This single header is so large that github reports “(Sorry about that, but we can’t show files that are this big right now.)”. All the classes that this header provide are in this single header, this in exact opposition to widely adopted best practice for C++ of having a single class per header.


For the huge size of vulkan.hpp there is few really compelling features added over the C API. There is some primitive memory management support but no where near sufficient for the purpose of serious application or scene graph development. To use Vulkan within the scene graph we still need to add this coherent memory/resource management - we still need to wrap the Vulkan objects, so if one uses vulkan.hpp you have two extra levels of wrapper and indirection for the underlying Vulkan objects and functions that are doing the work.


Managing complexity of design and implementation is of key importance for all software projects, adding complexity should only ever be done when it adds value that justifies it. Vulkan.hpp performs poorly by this metric and does not justify itself for use in the VSG project.


The vulkan-cpp-library was also considered. This is C++11 library that uses the Apache License and authored by an Google employee as their own project. The project has laid dormant for 2 years. The class naming and coding style takes notes far more from the C++ standard library than Vulkan that it wraps. This approach means that resulting code breaks with the style of all Vulkan headers and documentation, this incoherence is really jarring. This project is clearly an experiment that was dropped by the author before it was complete and no one else has come along to pick it up to finish it or maintain it.


The VkHLF (Vulkan High Level Framework) is a C++11 wrapper for Vulkan that builds upon vulkan.hpp adding better memory management and other facilities. VkHLF is developed by NVidia is a up to date and looks to be actively maintained. The class naming and style is also coherent with Vulkan so it’s relatively easy to relate VkHLF code to underlying Vulkan C API and Vulkan documentation that is predominately relates to the Vulkan C API.  VkHLF uses a NVidia drafted LICENSE that looks similar in principle to the MIT LICENSE.


The VkHLF is a serious body of work but still quite modest in size - 3,633 lines of code in the headers and another 5,142 lines of code in implementation. However, it depends upon the vulkan.hpp C++ bindings, so we have vkhlf::Instance (from vkhlf/Instance.h) wrapping a vk::Instance (from vulkan/vulkan.hpp) wrapping VkInstance from vulkan_core.h. This tells us vulkan.hpp is flawed - it simply doesn’t provide enough useful functionality to be useful on it’s own, so VkHLF adds some of those missing features.


However, design and implementation wise it’s simply not a good practice - working around flaws in a 3rd party body work functionality by building upon that flawed body of work. It may resolve some of the flaws but it’s still built upon a flawed foundation. You don’t build upon a sandy beach and expect your your building to remain robust long term.


The existence of VkHLF shout out that what if Khronos want to provide a C++ wrapper to Vulkan then it should be in the form of VkHLF without any extra levels of auto-generated headers in between. Perhaps in the future Khronos will do just this, but at this point in time VkHLF is a step in the wrong direction, it’s building upon sand (vulkan.hpp) not rock (vulkan.h).


For a scene graph the Vulkan objects and functions need to be created and invoked in specific ways that make sense for the scene graph and the applications that build upon it. For a scene graph wrapping Vulkan in a C++ API is not it’s primary purpose, the primary purpose is efficiently passing data to graphics hardware to be processed by the GPU. Extra facilities that make usage in the context of a scene graph easier don’t exist in a general purpose C++ wrapper for Vulkan, so you’d need to add them, and when you do you add an extra layer of classes and objects. One has to be careful how you wrap Vulkan, if done well it works efficiently and adds clarity of how the functionality relates to the underlying API, if done badly it adds memory or computation overhead and obfuscated what the software is doing.


The pumex project has also tackled this same issue - how to wrap up Vulkan functionality in the context of a scene graph. The approach that Pawel has taken is to use the vulkan.h C API wrapping selected features with pumex classes named in a coherent way to the underlying Vulkan features, so VkDevice maps to pumex::Device. The Vulkan C API is a well designed and easy to follow API - it’s very verbose, but it’s coherent, the layers you need on-top to make it useful to a C++11 scene graph are actually quite lightweight.


Pumex is a rendering library in it’s own right, it’s not a Vulkan wrapper, it has basic scene graph functionality already provided - elements of which are reminiscent of the OpenSceneGraph that reveal it’s author's long exposure to the OSG. Pumex can be thought of as a prototype for the VSG project rather than a 3rd party library that the VSG library would build upon. It illustrates nicely that wrapping Vulkan ourselves need not be an significant task, and offers opportunities to build a coherent bridge between the C++11 application domain and the lower level C domain that Vulkan works within.


The VulkanPlayground work experimenting with wrapping Vulkan is not based on pumex, rather it’s a based of incrementally recreating the VulkanTutorial functionality in a series of C++ wrappers for Vulkan objects. The wrappers are all located in VulkanPlayground/include/vsg/vk. The vsg namespace is used so VkDevice maps to vsg::Device.  The granularity of the approach is similar to what pumex uses but completely independently derived, with interface and implementation which are far more minimal in the vsg equivalents.  The vsg wrappers focus on creation, automatic resource clean-up and memory management. This is only prototype work so focus on key functionality rather than completeness of API and implementation.


The vsg/vk headers now total 1,839 lines of code, while the vsg/vk implementations total 2,337 lines of code for a total of 4167 lines of code. This is slightly less than half the size of VkHLF headers and source, and less than 1/10th the size of vulkan.hpp C++11 headers.  Despite the vsg/vk wrappers for Vulkan being a fraction of the size of vulkan.hpp they are far more useful for the purpose of creating a scene graph. The naming conventions have been kept coherent with the underlying vulkan.h C API and were possible the C structs and enums can be used directly. The prototype work done in VulkanPlayground illustrate how providing our own Vulkan wrappers is the best way to provide lightweight, coherent and useful encapsulation of Vulkan.

---

## 5. Gain familiarity and experiment with C++11, C++14 and C++17
The VulkanPlayground has adopted C++11 from the start, both the application test-beds and the vsg prototype library have been used to trial various C++11 features. C++11 is huge step forward for C++ programmers, enabling code to be cleaner, more succinct and more robust.

Not all features of C++11 are useful for scene graphs - testing of std::shared_ptr<> found that it’s memory overhead compared to locally provided intrusive reference counting is prohibitive and precludes its use in the context of a scene graph where memory footprint and bandwidth are key bottlenecks.

There has not been time during the Exploration Phase to experiment with C++14 and C++17 - work on learning and experimenting with Vulkan has taken precedence. At this point in time it’s clear that C++11 is very useful and sufficient for a major step forward in scene graph development. Whether C++14 and C++17 will probably crucial features is not something that can be established without spending time evaluating them.

Notes for September Extension of Exploration Phase: explored C++14 and C++17 and found that features in C++17 offer cleaner and more compact code that is easier to read and maintain. The memory allocator and filesystem features of C++17 are useful additions but at this point in time clang and gcc compiler support is experimental, only VisualStudio has full support. The improvements in code clarity alone justify adoption of C++17 going forward.

---

## 6. Test build tool options CMake and xmake.
Familiarity with Cmake made it an easy choice for the first pass of work on VulkanPlayground. There hasn’t been sufficient time to look at xmake within the three month Exploration Phase so it hasn’t been possible to evaluate the pros and cons of CMake vs xmake for the final VSG project.


As a general comment, all of the 3rd party projects and all of the Khronos toolsets reviewed during this phase use CMake. All OpenSceneGraph users will also be familiar with CMake. Market penetration of CMake within the computer graphics developer community makes it an uncontroversial choice.

For xmake to be adopted it will need to offer benefits for VSG developers and users to justify introduction of an unfamiliar tool. One way to evaluate xmake would be to port the present VulkanPlayground project from CMake to xmake.  If required this can be done after the completion of the present Exploration Phase.

---

## 7 Exploration Phase Conclusions
The Exploration Phase has covered most of key areas of investigation outlined in the original plan for this phase. Vulkan while well designed is verbose and complex to work with so has taken the majority of the available time to explore, to an extent that there has been insufficient time to research use of C++14, 17 and xmake within the scope of the 8 weeks work available. The one month extension to the Exploration Phase focused on C++17 and confirmed as appropriate version for final VSG.


A range of 3rd party maths, windowing and vulkan wrappers were reviewed as means of learning what is possible and for consideration as a 3rd party dependency. In the area of Maths GLM is a possibility but it’s implementation is messy and sprawling and supports GL rather than Vulkan so isn’t a perfect fit. Implementing our own GLSL style, Vulkan centric maths classes is a straightforward task so the need for GLM to minimize our own work effort is not compelling enough to justify it as a 3rd party dependency.


VkHLF is the best of the C++ wrappers of Vulkan but builds upon the autogenerated vulkan.hpp wrapper of vulkan C API, that is so large that standard developer tools like github fail to handle it as normal C++ header. VkHLF also creates a double wrapping of Vulkan classes, something that is a crude means of compensating for the lack of useful functionality that the Vulkan C++ header provides. The final C++ class Vulkan wrappers that VkHLF provides, while higher level than the Vulkan C API, still falls short of what is required to make the Vulkan objects directly usable within a scene graph.

A key part of the work in this phase has been focused on learning Vulkan and to this end creation of C++ wrappers for key Vulkan objects directly using the Vulkan C API provided a way of testing Vulkan and how best to manage it in C++ and within a scene graph. The Vulkan C API is well designed and favours wrapping in C++ objects that add resource management. The general approach has been to take a Vulkan object like VkDevice and map to a vsg::Device class.

Recreating the the VulkanTutorial was done using these C++ wrappers and has enabled a reduction in code size from 1530 lines to 275 lines in the vsgdraw.cpp test-bed. A similar code size reduction was achieved with the porting of the vulkan_minimal_compute tutorial to use these vsg Vulkan wrappers - 805 lines down to 141 lines.


Work has begun on adapting the Vulkan wrappers to work with the needs of a general purpose scene graph.  his work has not been completed, there has simply been too much work required to tame Vulkan to complete this experimental work within the 3 month time frame. This means parts of the VSG design is still open ended.


Windowing has not been a major focus during this phase, GLFW has been used as it provides an easy means for creating a Vulkan capable Window and Surface on which vulkan can be rendered with. GLFW was used primarily because the VulkanTutorial and other tutorial code use it, rather than using this to evaluate it’s suitability for VSG to use as it’s main mains for creating windows. The pumex project has its own windowing support that while more limited than GLFW is small and entirely focused on Vulkan rather than a GL windowing library that has been adapted to support Vulkan as well. The small size of the code required to providing windowing and event handling in pumex shows that handling native windowing within the VSG project will not be a significant challenge. Providing native windowing support ourselves will provide a coherent public interface and avoid adding external dependencies. Pumex is an open source project under the MIT license so sharing code is also a possibility.


As a general finding, the 3rd party dependencies reviewed have all provided useful insight into how or not to implement various features, ultimately none are useful enough directly to justify using as a direct 3rd party dependency, in the areas of maths, vulkan integration and windowing we can provide our own classes that are coherent with each other and tuned to the requirements of use with a scene graph and graphics applications that build upon them.

# VulkanSceneGraph Prototype Phase Report

The objective of the three month Prototype Phase, October-December 2018, was to flesh out:

1. High level project systems to be used in software development and community support
2. Portability of code base and systems to ensure easy cross platform development
3. Range of functionality to be encompassed in core library
4. How best to support add on libraries and applications built on top of VSG.
5. Test different lower level design and implementation approaches
6. Build upon and refine the work carried out in the Exploration Phase to provide a more rounded base for the Core Development Phase that will begin in January 2019.

## 1. High level project systems
**Hosting:** CMake, C++17, Vulkan were chosen in the Exploration Phase as the core software technologies that the VulkanSceneGraph project would be based upon. Github was chosen as the venue for software development, during the Exploration Phase this was hosted as part private repository, then made public at the start of the Prototype Phase, and then finally a dedicated [https://github.com/vsg-dev](https://github.com/vsg-dev) github account was created for VulkanSceneGraph project work going forward.

**Website:** The focus of the first year of development on the VulkanSceneGraph will be software development which will limit how much time can be dedicated to creation of websites and supporting materials, the project still requires a conventional website interface so to minimize the time required to support a website [Github's Pages](https://help.github.com/articles/what-is-github-pages/) functionality was adopted that automatically builds a html website from the projects github repository.  This is limited in functionality compared to a full-blown website but for the purposes of the first year of work on VulkanSceneGraph it should be sufficient. The [vulkanscenegraph.org](http://www.vulkanscenegraph.org) domain was purchased and has been setup to redirect to the .io website: https://vsg-dev.github.io/VulkanSceneGraphPrototype/ 

**Social Media** : To help communicate with the wider software community a [https://twitter.com/dev_vsg](https://twitter.com/dev_vsg) twitter account was created and has been used for announcements for feature development.

**Community Discussion**: In preparation for a community of user/developers building upon around the VulkanSceneGraph project a [vsg-dev](https://groups.google.com/forum/#!forum/vsg-users) Google Group has been created.  Google Groups was chosen based on the ability to support both mailing list and forum interaction whilst minimizing the overhead in setting up and maintaining the list.  Later in the projects life it may be necessary to self host a community mailing list/forum.

# Prototype Phase Work Plan
The aim of the Prototype Phase, October-December 2018, is to fill out prototypes for main elements of the core VSG scene graph library, add-on libraries and test programs. These prototypes will help solidify the choices in supporting technologies used and the design and implementation approaches used.

## General project infrastructure

We need to flesh out the following high level project infrastructure:

- [x] Layout used in core, add-on and supporting applications/examples.
	- Follow [FOSS Best Practices](https://github.com/coreinfrastructure/best-practices-badge/blob/master/doc/criteria.md)
- [x] Conventions (naming, coding style etc.) used in core, add-on and supporting applications/examples.
    - [x] Follow [CppCoreGuidlines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)
- [x] Website(s) - what requires dedicated websites, vs embedded in git-hub repositories.
	- [x] Initial approach to see how rich the experience can be with just README.md etc.
- [x] Developer/Community discussion forum(s)
	- [x] Create googlegroup [VulkanSceneGraph Developer Discussion Group](https://groups.google.com/forum/#!forum/vsg-users)
- [ ] 3rd party tools used in development and testing
	- [x] Static code analysis (cppcheck added 19.10.18)
    - [ ] Dynamic analysis such as LLVM sanitizers and valgrind

## Core Scene Graph development
Core scene graph work will be primarily tackled by Robert Osfield.

- [x] Support for object serialization and reading/writing to native ascii/binary format.
- [x] Creation of vsg::Array2d (completed), vsg::Array3D (completed) classes to mirror the existing [vsg::Array](../../include/vsg/core/Array.h) class to enable more streamlined support for texture data.
- [ ] Create a unified memory allocator interface to enable custom memory allocation for both scene graph objects and Vulkan objects.  Need to bring together the current [vsg::Allocator](../../include/vsg/core/Allocator.h) and [VkAllocationCallbacks](../../include/vsg/vk/AllocationCallback.h)
- [ ] Create basic [CullTraversal](../../include/traversal/CullTraversal.h) class that culls subgraphs, based on bounding sphere vs view frustum polytope, and accumulates scene graph state to generate a Command Graph
- [ ] Flesh out more [DispatchTraversal](../../include/traversals/DispatchTraversal.h) class that traverses the Command Graph
- [ ] Investigate unifying the [vsg::QuadGroup](../../include/nodes/QuadGroup.h) and [vsg::Group](../../include/nodes/Group.h) classes using a small size array optimization approach. Currently vsg::QuadGroup with is fixed size children array is faster than vsg::Group for creation and traversal, but is less flexible. Can we avoid the user space complexity of having two classes using small size optimizations?
- [ ] Restructure the scene graph level Vulkan object creation to use on-demand Vulkan object creation to enable handling of multiple logical devices and scene graph creation prior to viewer/logical device setup.
- [ ] Restructure the viewer/window level Vulkan object creation so that it uses a more standard MyClass::create(..) API and returns a vsg::ref_ptr<MyClass> rather than a vsg::Result<MyClass>. Use exceptions to handle errors.

## Cross platform support
The initial development work has been done under Linux, with support for additional platform to be tackled in the prototype phase. Cross platform work to be led by Thomas Hogarth.

- [x] Initial Windows support was added in October, this will be refined to provide as straight forward developer experience as we can achieve.
- [x] Development of platform specific Windowing support to replace the dependency on GLFW (done.)
	- [x] Win32_Window native windowing class for Windows
	- [x] Xcb_Window native Windowing for Unices
- [x] Port to Android : completed with vsgExample/Android example illustrating how to create an Android application
- [x] Port to macOS near completion (just key events left to resolve) with  native windowing provided by MacOS_Window.mm 

## Add-on library development
Add-on libraries will provide image and 3d model loaders, and integration with 3rd party software.

- [ ] [osg2vsg](https://github.com/vsg-dev/osg2vsg) OpenSceneGraph/VSG integration support library:
	- [x] Convert existing osg::Image loading/vulkan object creation to use vsg::Array2D(completed)/3D
	- [ ] Basic support for converting osg::Node scene graph objects to vsg::Node equivalents

- [ ] vsg*Image - possible integration of the 3rd party image readers/writers
- [ ] vsg*Model - possible integration of the 3rd party model readers/writers
- [ ] vsgGLSLang - possible integration with the [GLSLslang](https://github.com/KhronosGroup/glslang) library for reading GLSL shaders and converting to SPIRV shaders compatible with Vulkan/VSG.

## Example/Testbed development
All the software developed above needs testing, so we need to continue to expand the list of test applications that can test both the API usage and runtime behaviour/performance. Testing software is the primary focus during the **Prototype Phase** so applications developed during just as examples will not be attempted. The test programs can still serve as examples for others to learn from. Two main places for testbed development will be:
- [ ] [vsgExamples](https://github.com/vsg-dev/vsgExamples) - a set of test programs that will later evolve into our example set. Unit tests will likely need to be spawned off this project, possibly integrated into core VSG repository.
- [ ] [vsgFramework](https://github.com/vsg-dev/vsgFramework) - an experiment with using CMake to find external dependencies and if they aren't available fallback to using  [ExternalProject_Add()](https://cmake.org/cmake/help/latest/module/ExternalProject.html) to check out and build 3rd party dependencies.
# Vulkan/VkSceneGraph Headers
For convenience the [include/vsg/all.h](all.h) header is provided that includes all headers for you.  While quick to add to your code it will likely slow compilation compared to explicitly including just the headers you need.

```C++
#include <vsg/all.h> // prefer convenience over compile speed
```

The headers that provide the library classes and definitions are organized in subdirectories with the *include/vsg/directory_name* based on the category of functionality the header provides.  All C++ classes and function definitions provided are enclosed in vsg namespace.  The vsg subdirectories/categories are:

* [include/vsg/core](core/) - Base classes & memory management

* [include/vsg/maths](maths/) - GLSL style maths classes

* [include/vsg/nodes](nodes/) - Graph node classes

* [include/vsg/traversals](traversals/) - Graph traversals

* [include/vsg/vk](vk/) - Vulkan integration classes

* [include/vsg/io](io/) - File system, stream and native file format support

* [include/vsg/ui](ui/) - User Interface Event classes

* [include/vsg/viewer](viewer/) - Viewer/Windowing classes

* [include/vsg/platform](platform/) - Platform specific Windowing/support classes

* [include/vsg/utils](utils/) - Utility classes/template functions

* [include/vsg/introspection](introspection) - introspection/reflection classes/functions
# include/vsg/core headers
The **include/vsg/core** header directory contains the base classes, smart pointers and memory management classes.


## Base Object classes

* [include/vsg/core/Object.h](Object.h) - main base class that provides intrusive std::atomic based thread safe reference counting and meta data interface
* [include/vsg/core/Auxiliary.h](Auxiliary.h) - an optional object class used by vsg::Object to store meta data when required, or links to allocators used.

## Smart pointers & Memory management classes
* [include/vsg/core/ref_ptr.h](ref_ptr.h) - template smart pointer class that uses vsg::Object's intrusive reference count to robustly management object lifetime. Similar to role std::shared_ptr<> but higher performance virtual of having half the memory footprint, holding just a single C pointer internally rather than two pointers that std::shared_ptr<> requires.
* [include/vsg/core/observer_ptr.h](observer_ptr.h) - template smart pointer class for non owning pointer references. Similar in role to std::weak_ptr<> but works with the VSG's intrusive reference counting.
* [include/vsg/core/Allocator.h](Allocator.h) - base class that provides a standard interface for custom allocation and deleting of allocated memory.

## Data container classes
* [include/vsg/core/Data.h](Data.h) - base class that abstracts the provision of data (typically passed to Vulkan or for storing meta data.)
* [include/vsg/core/Value.h](Value.h) - template Data class that provides a single simple type (such as int, vsg::vec2 etc.)  Typical uses : storing meta data values, uniforms and vertex array data.
* [include/vsg/core/Array.h](Array.h) - template Data class that provides an 1D Array of simpler types (such as int, vsg::vec2 etc.).  Typical uses : storing uniforms, vertex array data, and 1D texture/image data.

## Visitor pattern classes

* [include/vsg/core/Visitor.h](Visitor.h) - base visitor class for non const objects/graphs
* [include/vsg/core/ConstVisitor.h](ConstVisitor.h) - base visitor class for const objects/graphs

## C++ template helper classes
* [include/vsg/core/Inherit.h](Inherit.h) - Curiously Recurring Template Pattern used to implement standardized visitor, traversal and memory allocation methods
* [include/vsg/core/Result.h](Result.h) - template class used by Object creation methods for returning of object ownership on success and errors if they occur.

## General build support headers 
* [include/vsg/core/Export.h](Export.h) - provides Windows __declspec() macros abstraction
* [include/vsg/core/Version.h](Version.h) - autogenerated header with libvsg version information
# include/vsg/introspection headers

The include/vsg/introspection header contains classes and C functions for querying class interfaces, creating objects and calling methods via generic interface.

* [include/vsg/introspection/c_interface.h](c_interface.h) - very early experiment with what a C introspection interface might look like.# include/vsg/io headers
The **include/vsg/io** header directory contains std::i/ostream operators, and input/output serilizations support.

## stream support
[include/vsg/io/stream.h](stream.h) provides overloads of the << and >> stream operators for std::pair<>, and the vsg::vec2, vsg::vec3, vsg::vec4 and vsg::mat4 in both their float and double variants.


## File system support
Original plan was to use C++17's filesystem support, unfortunately this is only fully supported under VisualStudio 2017 at this point in time so we've fallen back to providing a set of helper functions for checking for file existence and searching file paths.

[include/vsg/io/FileSystem.h](FileSystem.h) - provides vsg::getEnvPaths(..), fileExist(..), concactPaths(..) and findFile(..) convinience functions

Example usage:

```c++
    // read shaders
    vsg::Paths searchPaths = vsg::getEnvPaths("VSG_FILE_PATH");

    vsg::ref_ptr<vsg::Shader> vertexShader = vsg::Shader::read( VK_SHADER_STAGE_VERTEX_BIT, "main", vsg::findFile("shaders/vert.spv", searchPaths));
    vsg::ref_ptr<vsg::Shader> fragmentShader = vsg::Shader::read(VK_SHADER_STAGE_FRAGMENT_BIT, "main", vsg::findFile("shaders/frag.spv", searchPaths));
```


# include/vsg/maths headers
The **include/vsg/maths** header directory contains the vector, matrix classes and maths functions. The interface and conventions are kept the same as GLSL so C++ usage can be kept consistent with shaders usage.

The vector and maths classes are simple types, do not subclass from vsg::Object, so should be treated like ints, floats etc. The memory storage used aligns with the types expected by Vulkan so can be used directly for uniform, vertex and image data.

## Vector classes
* [include/vsg/maths/vec2.h](vec2.h) - template class for 2d vectors, provides vsg::vec2 (float), vsg::dvec2 (double) versions.
* [include/vsg/maths/vec3.h](vec3.h) - template class for 3d vectors, provides vsg::vec3 (float), vsg::dvec3 (double) versions.
* [include/vsg/maths/vec4.h](vec4.h) - template class for 4d vectors, provides vsg::vec4 (float), vsg::dvec4 (double) versions.

## Matrix classes
* [include/vsg/maths/mat4.h](mat4.h) - template class for 4x4 matrix, providing vsg::mat4 (float) and vsg::dmat4 (double) versions.

## Matrix/Vector support functions
* [include/vsg/maths/transform.h](transform.h) - provides a range of convenience functions for creation of matrices and operations on matrices and vector.
# include/vsg/nodes headers
The **include/vsg/nodes** header directory contains the graph node classes.  These classes are used to create scene graphs, command graphs and graphs used for custom purposes.

The design is based on the concept of top down Direct Acyclic Graph (DAG), where the internal nodes of the graph aggregate lists of smart pointers to other internal or leaf nodes. Node subclasses add specific data and behaviours to the graph to provided guidance how the graph should be traversed and processed.

## Node base class
* [include/vsg/nodes/nodes/Node.h](Node.h) - base Node class, currently it doesn't provide any functionality and just serves as a base class, it's role will likely expand as the project advances.

## Group classes
* [include/vsg/nodes/nodes/Group.h](Group.h) - general purpose group that aggregates a list of children using variable sized vector of `vsg::ref_ptr<vsg::Node>`.

* [include/vsg/nodes/nodes/QuadGroup.h](QuadGroup.h) - a performance orientated group with sized fixed to four children.

## LOD class
* [include/vsg/nodes/nodes/LOD.h](LOD.h) - an experiment with a stripped down level of details class that has just two children and one distance value to guidance choice between them.

## State classes
* [include/vsg/nodes/nodes/StateGroup.h](StateGroup.h) - a subclass from vsg::Group that add a list of `ref_ptr<vsg::StateComponent>`that encapsulate Vulkan state such as shader, uniform and vertex bindings.
# include/vsg/traversals headers
The **include/vsg/traversals** header directory contains the main traversal classes, currently includes the beginnings of cull and dispatch traversals but as the project progress these will be joined by other traversals such update, event and other traversals that are found to be useful.

* [include/vsg/traversals/CullTraversal.h](CullTraversal.h) - Currently just a shell.  During [Prototype Phase](../../../docs/PrototypePhase/Workplan.md) will be implementing basic cull traversal that will cull nodes with bounding volumes against view frustum, accumulate state, and create a dispatch graph to passed on to the dispatch traversal to pass data and commands to Vulkan.
* [include/vsg/traversals/DispatchTraversal.h](DispatchTraversal.h) - Very early cut of dispatch traversal that dispatches data and commands into to a Vulkan command queue.  Currently only tracks a subset of Vulkan state components and does so with relatively slow std::map<> containers.  This will be fleshed out further in Prototype Phase to enable basic scene graph rendering capabilities.# include/vsg/utils headers
The **include/vsg/utils** header directory contains general utility classes and functions.

## CommandLine parsing
[include/vsg/utils/CommandLine.h](CommandLine.h) provides convenience class for reading command line arguments into basic types like int, string, and compound types like vsg::vec2, std::pair<>, as well as providing a means for setting default values.

Example usage:

```c++
int main(int argc, char** argv)
{
    // set up defaults and read command line arguments to override them
    vsg::CommandLine arguments(&argc, argv);
    auto debugLayer = arguments.read({"--debug","-d"});
    auto apiDumpLayer = arguments.read({"--api","-a"});
    auto printFrameRate = arguments.read("--fr");
    auto numFrames = arguments.value(-1, "-f");
    auto numWindows = arguments.value(1, "--num-windows");
    auto [width, height] = arguments.value(std::pair<uint32_t, uint32_t>(800, 600), {"--window", "-w"});
    if (arguments.errors()) return arguments.writeErrorMessages(std::cerr);
    ...
}
```
# include/vsg/viewer headers

The include/vsg/viewer header directory contains the Windowing  and Viewer classes required to create a Vulkan window(s) and viewer to render to it/then.

* [include/vsg/viewer/GraphicsStage.h](GraphicsStage.h) - class for managing the dispatch of Vulkan state and geometry data into the Vulkan graphics queue.
* [include/vsg/viewer/Window.h](Window.h) - base class for creation of Windows with Vulkan support.  Subclasses from vsg::Window provide the implementation for the different target platforms.  Currently a GLFW based Window is provided internally by libvsg to server the role as cross platform Window implementation.  Plan is to replace the GLFW version with native Windowing implementations.
* [include/vsg/viewer/Viewer.h](Viewer.h) - high level viewer class for managing vsg::Window(s) and rendering of graphics to them.
# include/vsg/vk headers
The **include/vsg/vk** header directory contains the Vulkan C API integration classes.

## Naming convention
The Vulkan integration wrappers follow the convention **VkName -> vsg::Name** with the wrapper class found in the header **include/vsg/vk/Name.h**. For example **VkInstance** is wrapped by the class vsg::Instance which is located in header [include/vsg/vk/Instance.h](Instance.h).

## Vulkan object creation and validity
The Vulkan integration classes are all created use a ```vsg::Result<vsg::VulkanClass>  vsg::VulkanClass::create(..)``` method that only returns a valid vsg::VulkanClass via the Result object if the associated Vulkan object has been successfully created, on failure a VK_* error is returned via the Result object. The associated Vulkan object is also only destroyed by the vsg::VulkanClass destructor.  The combination of the VulkanClass::create and destructor behaviour ensures that the associated Vulkan object is valid for the whole lifetime of VulkanClass object.

## Memory management
The Vulkan integration classes add support automatic lifetime management to ensure that Vukan objects can not be deleted while they are still be used, and finally automatic clean up was once the references are removed.

The lifetime management is provided by leveraging the vsg's intrusive reference counting support provided by vsg::ref_ptr<> and vsg::Object base class. To ensure that higher level Vulkan objects (vkDevice/vsg::Device etc.) are not deleted before lower level Vulkan objects (vsg::CommandPool, vsg::BufferData etc.) are still using/reference them the lower level Vulkan wrapper classes hold a vsg::ref_ptr<> reference to the high level Vulkan wrapper classes.

The scheme of lower level Vulkan wrappers holding reference to high level Vulkan Wrappers is outwardly the inverse of how one would normally think of ownership hierarchy, which would be along the lines of an Instance owning a list logical Devices, but the power behind this scheme is it enables decoupled, thread safe and robust lifetime management whilst remaining simple to implement and easy to use. The following pseudo code illustrates:

```c++
{
    vsg::ref_ptr<vsg::Instance> instance = vsg::Instance::create(...);
    vsg::ref_ptr<vsg::Device> device = vsg::Device::create(instance,...); // device holds a ref_ptr<> to instance

   // even if we try to discard the instance explicitly,
   // or it goes out of scope things remain safe
   instance = nullptr; // Instance object isn't deleted, as Device still needs it

   ...
   // application code using Device
   ...

} // device goes out of scope, both Device and Instance automatically
  // cleaned up in the correct order : VkDevice then VkInstance.
```

To see an example of memory management working in a full blown code see the [vsgdraw](https://github.com/vsg-dev/vsgExamples/tree/master/Desktop/vsgdraw) found in [vsgExample](https://github.com/vsg-dev/vsgExamples) repository. The key is there won't asee any explicit management of lifetime, it's all done for you when all the ref_ptr<> go out of scope at the end of main. To see that Vulkan is being cleaned up correctly run this example with the --api command line thus: ```vsgdraw --api``` to see all Vulkan API calls output to the console.

## High Level Vulkan integration classes

High level Vulkan integration concerns Vulkan objects that are created at the Application, Window and Viewer level and don't change as scene graph/command graph level Vulkan objects are created and destroyed.

* [include/vsg/vk/Instance.h](Instance.h) - wrapper for [vkInstance](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/man/html/VkInstance.html)
* [include/vsg/vk/PhysicalDevice.h](PhysicalDevice.h) - wrapper for [vkPhysicalDevice](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/man/html/VkPhysicalDevice.html)
* [include/vsg/vk/Surface.h](Surface.h) - wrapper for vkSurface
* [include/vsg/vk/Device.h](Device.h) -
* [include/vsg/vk/RenderPass.h](RenderPass.h) -
* [include/vsg/vk/Semaphore.h](Semaphore.h) -
* [include/vsg/vk/Swapchain.h](Swapchain.h) -
* [include/vsg/vk/CommandBuffer.h](CommandBuffer.h) -
* [include/vsg/vk/CommandPool.h](CommandPool.h) -
* [include/vsg/vk/Fence.h](Fence.h) -
* [include/vsg/vk/Framebuffer.h](Framebuffer.h) -
* [include/vsg/vk/State.h](State.h) -

## Low level Vulkan integration classes

Low level Vulkan integration concern Vulkan objects that relate to data and commands defined in Scene Graphs and Command Graphs.

* [include/vsg/vk/BufferData.h](BufferData.h) -
* [include/vsg/vk/Buffer.h](Buffer.h) -
* [include/vsg/vk/Buffer.h](Buffer.h) -
* [include/vsg/vk/Descriptor.h](Descriptor.h) -
* [include/vsg/vk/DescriptorPool.h](DescriptorPool.h) -
* [include/vsg/vk/DescriptorSet.h](DescriptorSet.h) -
* [include/vsg/vk/DescriptorSetLayout.h](DescriptorSetLayout.h) -
* [include/vsg/vk/DeviceMemory.h](DeviceMemory.h) -
* [include/vsg/vk/Image.h](Image.h) -
* [include/vsg/vk/ImageView.h](ImageView.h) -
* [include/vsg/vk/Pipeline.h](Pipeline.h) -
* [include/vsg/vk/PipelineLayout.h](PipelineLayout.h) -
* [include/vsg/vk/GraphicsPipeline.h](GraphicsPipeline.h) -
* [include/vsg/vk/ComputePipeline.h](ComputePipeline.h) -
* [include/vsg/vk/PushConstants.h](PushConstants.h) -
* [include/vsg/vk/Sampler.h](Sampler.h) -
* [include/vsg/vk/ShaderModule.h](ShaderModule.h) -

## Vulkan command integration classes

Vulkan commands have a specific role in Vulkan so to encapsulate this the [vsg::Command](Commnd.h) pure virtual base class provides **virtual void dispatch(CommandBuffer&) const** is overridden in the subclasses to provide specific Vulkan command calls.

* [include/vsg/vk/Command.h](Command.h) -
* [include/vsg/vk/Draw.h](Draw.h) -
* [include/vsg/vk/BindIndexBuffer.h](BindIndexBuffer.h) -
* [include/vsg/vk/BindVertexBuffers.h](BindVertexBuffers.h) -

## Memory management classes

* [include/vsg/vk/AllocationCallbacks.h](AllocationCallbacks.h) -
* [include/vsg/vk/MemoryManager.h](MemoryManager.h) -
# collect all the headers in the source directory
file(GLOB HEADERS ${CMAKE_SOURCE_DIR}/include/vsg/*.h ${CMAKE_SOURCE_DIR}/include/vsg/*/*.h)

# for out of source builds collect all the auto-generated headers in the build directory
if (NOT (${CMAKE_SOURCE_DIR} STREQUAL ${CMAKE_BINARY_DIR}))
    file(GLOB AUTOGENERATED_HEADERS ${CMAKE_BINARY_DIR}/include/vsg/*.h ${CMAKE_BINARY_DIR}/include/vsg/*/*.h)
    set(HEADERS ${HEADERS} ${AUTOGENERATED_HEADERS})
endif()

# set up the source files explicitly.
set(SOURCES

    core/Allocator.cpp
    core/Auxiliary.cpp
    core/ConstVisitor.cpp
    core/Data.cpp
    core/External.cpp
    core/Object.cpp
    core/Objects.cpp
    core/Result.cpp
    core/Visitor.cpp
    core/Version.cpp

    introspection/c_interface.cpp

    maths/transform.cpp

    nodes/Commands.cpp
    nodes/Group.cpp
    nodes/Geometry.cpp
    nodes/Node.cpp
    nodes/QuadGroup.cpp
    nodes/StateGroup.cpp
    nodes/CullGroup.cpp
    nodes/CullNode.cpp
    nodes/LOD.cpp
    nodes/PagedLOD.cpp
    nodes/MatrixTransform.cpp
    nodes/VertexIndexDraw.cpp


    io/FileSystem.cpp
    io/AsciiInput.cpp
    io/DatabasePager.cpp
    io/AsciiOutput.cpp
    io/BinaryInput.cpp
    io/BinaryOutput.cpp
    io/Input.cpp
    io/ObjectCache.cpp
    io/Output.cpp
    io/Options.cpp
    io/ObjectFactory.cpp
    io/ReaderWriter.cpp
    io/ReaderWriter_vsg.cpp
    io/read.cpp
    io/write.cpp

    traversals/DispatchTraversal.cpp
    traversals/CullTraversal.cpp
    traversals/CompileTraversal.cpp
    traversals/ComputeBounds.cpp

    threading/OperationQueue.cpp
    threading/OperationThreads.cpp

    viewer/Camera.cpp
    viewer/GraphicsStage.cpp
    viewer/View.cpp
    viewer/Viewer.cpp
    viewer/Window.cpp
    viewer/Trackball.cpp

    vk/Buffer.cpp
    vk/BufferData.cpp
    vk/BufferView.cpp
    vk/BindIndexBuffer.cpp
    vk/BindVertexBuffers.cpp
    vk/Command.cpp
    vk/CommandBuffer.cpp
    vk/CommandPool.cpp
    vk/ComputePipeline.cpp
    vk/Context.cpp
    vk/Descriptor.cpp
    vk/DescriptorBuffer.cpp
    vk/DescriptorImage.cpp
    vk/DescriptorTexelBufferView.cpp
    vk/DescriptorPool.cpp
    vk/DescriptorSet.cpp
    vk/DescriptorSetLayout.cpp
    vk/Device.cpp
    vk/DeviceMemory.cpp
    vk/Draw.cpp
    vk/Extensions.cpp
    vk/Fence.cpp
    vk/Framebuffer.cpp
    vk/GraphicsPipeline.cpp
    vk/Image.cpp
    vk/ImageData.cpp
    vk/ImageView.cpp
    vk/Instance.cpp
    vk/MemoryManager.cpp
    vk/PhysicalDevice.cpp
    vk/PipelineLayout.cpp
    vk/PipelineBarrier.cpp
    vk/PushConstants.cpp
    vk/Queue.cpp
    vk/RenderPass.cpp
    vk/ResourceHints.cpp
    vk/Sampler.cpp
    vk/Semaphore.cpp
    vk/ShaderModule.cpp
    vk/ShaderStage.cpp
    vk/Surface.cpp
    vk/Swapchain.cpp
)

# add platform specific Window implementation

# set up library dependencies
set(LIBRARIES PUBLIC
    Vulkan::Vulkan
    Threads::Threads
)

if (ANDROID)
    set(HEADERS ${HEADERS} ${CMAKE_SOURCE_DIR}/include/vsg/platform/android/Android_Window.h)
    set(SOURCES ${SOURCES} platform/android/Android_Window.cpp)

    if(CMAKE_SYSTEM_VERSION GREATER 24)
        set(LIBRARIES ${LIBRARIES} PRIVATE ${AndroidLib} PRIVATE ${AndroidNativeWindowLib})
    else()
        set(LIBRARIES ${LIBRARIES} PRIVATE ${AndroidLib})
    endif()

elseif (WIN32)
    set(SOURCES ${SOURCES} platform/win32/Win32_Window.cpp)
elseif (APPLE)
    set(SOURCES ${SOURCES} platform/macos/MacOS_Window.mm)
    set(LIBRARIES ${LIBRARIES} PRIVATE ${COCOA_LIBRARY} PRIVATE ${QUARTZCORE_LIBRARY})
else()
    set(SOURCES ${SOURCES} platform/unix/Xcb_Window.cpp)
    set(LIBRARIES ${LIBRARIES} PRIVATE PkgConfig::xcb)
endif()


add_library(vsg ${HEADERS} ${SOURCES})

if(MSVC)
    # ensure the libraries are all built in the lib directory
    macro(SET_OUTPUT_DIR_PROPERTY TARGET_TARGETNAME RELATIVE_OUTDIR)
        # Global properties (All generators but VS & Xcode)
        set_target_properties(${TARGET_TARGETNAME} PROPERTIES ARCHIVE_OUTPUT_DIRECTORY "${OUTPUT_LIBDIR}/${RELATIVE_OUTDIR}")
        set_target_properties(${TARGET_TARGETNAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${OUTPUT_LIBDIR}/${RELATIVE_OUTDIR}")
        set_target_properties(${TARGET_TARGETNAME} PROPERTIES LIBRARY_OUTPUT_DIRECTORY "${OUTPUT_LIBDIR}/${RELATIVE_OUTDIR}")

        # Per-configuration property (VS, Xcode)
        foreach(CONF ${CMAKE_CONFIGURATION_TYPES})        # For each configuration (Debug, Release, MinSizeRel... and/or anything the user chooses)
            string(TOUPPER "${CONF}" CONF)                # Go uppercase (DEBUG, RELEASE...)

            # We use "FILE(TO_CMAKE_PATH", to create nice looking paths
            set_target_properties(${TARGET_TARGETNAME} PROPERTIES "ARCHIVE_OUTPUT_DIRECTORY_${CONF}" "${OUTPUT_LIBDIR}/${RELATIVE_OUTDIR}")
            set_target_properties(${TARGET_TARGETNAME} PROPERTIES "RUNTIME_OUTPUT_DIRECTORY_${CONF}" "${OUTPUT_LIBDIR}/${RELATIVE_OUTDIR}")
            set_target_properties(${TARGET_TARGETNAME} PROPERTIES "LIBRARY_OUTPUT_DIRECTORY_${CONF}" "${OUTPUT_LIBDIR}/${RELATIVE_OUTDIR}")
        endforeach()
    endmacro()

    SET_OUTPUT_DIR_PROPERTY(vsg "")
	
    option(ENABLE_MP_FLAG "Turning on this option will add the multi-processor flag in MSVC for VSG and it's included projects" ON)
	
    if(ENABLE_MP_FLAG)
        target_compile_options(vsg PRIVATE "/MP")
    endif()

endif()


# place header and source files into group folders to help IDE's present the files in a logical manner
function(ASSIGN_SOURCE_GROUPS GROUP_NAME ROOT_FOLDER)
    foreach(FILE IN ITEMS ${ARGN})
        if (IS_ABSOLUTE "${FILE}")
            file(RELATIVE_PATH RELATIVE_SOURCE "${ROOT_FOLDER}" "${FILE}")
        else()
            set(RELATIVE_SOURCE "${FILE}")
        endif()
        get_filename_component(SOURCE_PATH "${RELATIVE_SOURCE}" PATH)
        string(REPLACE "/" "\\" SOURCE_PATH_MSVC "${SOURCE_PATH}")
        source_group("${GROUP_NAME}\\${SOURCE_PATH_MSVC}" FILES "${FILE}")
    endforeach()
endfunction(ASSIGN_SOURCE_GROUPS)

# enable folders for MSVC
set_property(GLOBAL PROPERTY USE_FOLDERS ON)

# group source files and headers
ASSIGN_SOURCE_GROUPS("Source Files" "${CMAKE_CURRENT_SOURCE_DIR}" ${SOURCES})
ASSIGN_SOURCE_GROUPS("Header Files" "${CMAKE_SOURCE_DIR}/include/vsg" ${HEADERS})


# set up versions and position independent code that is required for unix platforms
set_property(TARGET vsg PROPERTY VERSION ${VSG_VERSION_MAJOR}.${VSG_VERSION_MINOR}.${VSG_VERSION_PATCH})
set_property(TARGET vsg PROPERTY SOVERSION ${VSG_SOVERSION})
set_property(TARGET vsg PROPERTY POSITION_INDEPENDENT_CODE ON)
set_property(TARGET vsg PROPERTY CXX_STANDARD 17)

target_include_directories(vsg PUBLIC $<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/include> $<BUILD_INTERFACE:${CMAKE_BINARY_DIR}/include>)


target_link_libraries(vsg ${LIBRARIES})


install(TARGETS vsg EXPORT vsgTargets
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION bin
        INCLUDES DESTINATION include
)

if (BUILD_SHARED_LIBS)
    target_compile_definitions(vsg INTERFACE VSG_SHARED_LIBRARY)
endif()

install(DIRECTORY ${CMAKE_SOURCE_DIR}/include/vsg DESTINATION include)
if (NOT(${CMAKE_BINARY_DIR} STREQUAL ${CMAKE_SOURCE_DIR}))
    install(DIRECTORY ${CMAKE_BINARY_DIR}/include/vsg DESTINATION include)
endif()

# [==[
install(EXPORT vsgTargets
    FILE vsgTargets.cmake
    NAMESPACE vsg::
    DESTINATION lib/cmake/vsg
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file("${CMAKE_BINARY_DIR}/src/vsg/vsgConfigVersion.cmake" COMPATIBILITY SameMajorVersion)

install(FILES "vsgConfig.cmake" "${CMAKE_BINARY_DIR}/src/vsg/vsgConfigVersion.cmake" DESTINATION lib/cmake/vsg)

# ]==]
# src/vsg source directories

The implementations provided by the src/vsg directories mirror the structure of the include/vsg header directory structure.  

* [src/vsg/core](core) - core library class implementstion

* [src/vsg/nodes](nodes) - graph node implementations

* [src/vsg/traversals](traversals) - traversal implementations

* [src/vsg/vk](vk) - Vulkan integration

* [src/vsg/vk](viewer)- Viewer implementations

* [src/vsg/utils](utils) - Utility implementations

* [src/vsg/introspection](introspection) - Introspection implementations
