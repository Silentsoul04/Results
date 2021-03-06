# Copyright (c) Dean Michael Berris 2010.
# Copyright 2016 Google, Inc.
# Distributed under the Boost Software License, Version 1.0.
# (See accompanying file LICENSE_1_0.txt or copy at
# http://www.boost.org/LICENSE_1_0.txt)

cmake_minimum_required(VERSION 2.8)
project(CPP-NETLIB)

option( CPP-NETLIB_BUILD_SHARED_LIBS "Build cpp-netlib as shared libraries." OFF )
option( CPP-NETLIB_BUILD_TESTS "Build the cpp-netlib project tests." ON)
option( CPP-NETLIB_BUILD_EXAMPLES "Build the cpp-netlib project examples." ON)
option( CPP-NETLIB_ENABLE_HTTPS "Build cpp-netlib with support for https if OpenSSL is found." ON)
option( CPP-NETLIB_STATIC_OPENSSL "Build cpp-netlib using static OpenSSL" OFF)
option( CPP-NETLIB_STATIC_BOOST "Build cpp-netlib using static Boost" OFF)

include(GNUInstallDirs)

# determine install path for CMake config files
if(WIN32 AND NOT CYGWIN)
    set(DEF_INSTALL_CMAKE_DIR CMake)
else()
    set(DEF_INSTALL_CMAKE_DIR ${CMAKE_INSTALL_LIBDIR}/cmake/cppnetlib)
endif()
set(INSTALL_CMAKE_DIR ${DEF_INSTALL_CMAKE_DIR} CACHE PATH "Installation directory for CMake files")

# Make relative cmake install path absolute (needed later on)
if(NOT IS_ABSOLUTE "${INSTALL_CMAKE_DIR}")
    set(INSTALL_CMAKE_DIR "${CMAKE_INSTALL_PREFIX}/${INSTALL_CMAKE_DIR}")
endif()

if(CPP-NETLIB_BUILD_SHARED_LIBS OR BUILD_SHARED_LIBS)
  message (STATUS "Linking boost testing libs dynamically...")
  set(CPP-NETLIB_BUILD_SHARED_LIBS ON)
  set(BUILD_SHARED_LIBS ON)
else()
  set(CPP-NETLIB_BUILD_SHARED_LIBS OFF)
  set(BUILD_SHARED_LIBS OFF)
endif()

# Use Boost's static libraries
if (CPP-NETLIB_STATIC_BOOST)
  set(Boost_USE_STATIC_LIBS ON)
endif()

# We need this for all tests to use the dynamic version.
add_definitions(-DBOOST_TEST_DYN_LINK)

# Always use multi-threaded Boost libraries.
set(Boost_USE_MULTI_THREADED ON)

find_package(Boost 1.55.0 REQUIRED COMPONENTS system thread)

if (CPP-NETLIB_ENABLE_HTTPS)
  if (APPLE)
    # If we're on OSX check for Homebrew's copy of OpenSSL instead of Apple's
    if (NOT OpenSSL_DIR)
      find_program(HOMEBREW brew)
      if (HOMEBREW STREQUAL "HOMEBREW-NOTFOUND")
        message(WARNING "Homebrew not found: not using Homebrew's OpenSSL")
        if (NOT OPENSSL_ROOT_DIR)
          message(WARNING "Use -DOPENSSL_ROOT_DIR for non-Apple OpenSSL")
        endif()
      else()
        execute_process(COMMAND brew --prefix openssl
          OUTPUT_VARIABLE OPENSSL_ROOT_DIR
          OUTPUT_STRIP_TRAILING_WHITESPACE)
      endif()
    endif()
  endif()
 if (CPP-NETLIB_STATIC_OPENSSL)
   set(CMAKE_FIND_LIBRARY_SUFFIXES .a)
 endif()
  find_package(OpenSSL)
endif()

find_package( Threads )
set(CMAKE_VERBOSE_MAKEFILE true)

set(CPPNETLIB_VERSION_MAJOR 0) # MUST bump this whenever we make ABI-incompatible changes
set(CPPNETLIB_VERSION_MINOR 12)
set(CPPNETLIB_VERSION_PATCH 0)
set(CPPNETLIB_VERSION_STRING ${CPPNETLIB_VERSION_MAJOR}.${CPPNETLIB_VERSION_MINOR}.${CPPNETLIB_VERSION_PATCH})

if (CMAKE_BUILD_TYPE MATCHES Debug)
    add_definitions(-DBOOST_NETWORK_DEBUG)
endif()

if (OPENSSL_FOUND)
    add_definitions(-DBOOST_NETWORK_ENABLE_HTTPS)
    include_directories(${OPENSSL_INCLUDE_DIR})
endif()

if (${CMAKE_CXX_COMPILER_ID} MATCHES GNU)
  # Use C++11 when using GNU compilers.
  set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -std=c++11")
elseif (${CMAKE_CXX_COMPILER_ID} MATCHES Clang)
  # We want to link in C++11 mode in Clang too, but also set a high enough
  # template depth for the template metaprogramming.
  set (CMAKE_CXX_FLAGS
    "${CMAKE_CXX_FLAGS} -Wall -ftemplate-depth=256 -std=c++11 -DBOOST_ASIO_HAS_STD_CHRONO -DBOOST_ASIO_HAS_STD_ARRAY -DBOOST_ASIO_HAS_STD_SHARED_PTR -DBOOST_ASIO_HAS_STD_ATOMIC -DBOOST_ASIO_HAS_VARIADIC_TEMPLATES -DBOOST_ASIO_HAS_MOVE -DBOOST_THREAD_VERSION=3")
  if (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    # Use libc++ only in OS X.
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++")
    set (CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -lc++")
  elseif (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    # Use libstdc++ for Linux.
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libstdc++")
    set (CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -lstdc++")
  endif()
endif()

set(Uri_BUILD_TESTS OFF)
set(Uri_BUILD_DOCS OFF)
set(Uri_DISABLE_LIBCXX ON)
add_subdirectory(deps/uri)
include_directories(deps/uri/include)

if (Boost_FOUND)
    if (MSVC)
      add_definitions(-D_SCL_SECURE_NO_WARNINGS)
    endif(MSVC)
    if (WIN32)
      add_definitions(-D_WIN32_WINNT=0x0501)
    endif(WIN32)
    include_directories(${Boost_INCLUDE_DIRS})

    # # Asio
    # add_definitions(-DASIO_STANDALONE)
    # include_directories(deps/asio/asio/include)

    enable_testing()
    add_subdirectory(libs/network/src)
    if (CPP-NETLIB_BUILD_TESTS)
      add_subdirectory(deps/googletest)
      add_subdirectory(deps/uri/test)
      add_subdirectory(libs/network/test)
    endif (CPP-NETLIB_BUILD_TESTS)
    if (CPP-NETLIB_BUILD_EXAMPLES)
      add_subdirectory(libs/network/example)
    endif (CPP-NETLIB_BUILD_EXAMPLES)
endif(Boost_FOUND)

if (MSVC)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /bigobj")
endif()

# See whether we can find the ccache program -- if we can, then use it for the build.
find_program(CCACHE_FOUND ccache)
if(CCACHE_FOUND)
  set_property(GLOBAL PROPERTY RULE_LAUNCH_COMPILE ccache)
  set_property(GLOBAL PROPERTY RULE_LAUNCH_LINK ccache)
endif(CCACHE_FOUND)

enable_testing()

install(DIRECTORY boost DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

# ###
# ## Export Targets
# # (so cpp-netlib can be easily used by other CMake projects)
# # [see http://www.cmake.org/Wiki/CMake/Tutorials/How_to_create_a_ProjectConfig.cmake_file]
#
# # Add all targets to the build-tree export set
# export(TARGETS cppnetlib-client-connections cppnetlib-server-parsers cppnetlib-uri
#     FILE "${PROJECT_BINARY_DIR}/cppnetlibTargets.cmake")
# # Export the package for use from the build-tree
# # (this registers the build-tree with a global CMake-registry)
# export(PACKAGE cppnetlib)
# # Create the cppnetlibConfig.cmake and cppnetlibConfigVersion files
# file(RELATIVE_PATH REL_INCLUDE_DIR "${INSTALL_CMAKE_DIR}"
#     "${CMAKE_INSTALL_FULL_INCLUDEDIR}")
# # ... for the build tree
# set(CONF_INCLUDE_DIRS "${PROJECT_SOURCE_DIR}" ${Boost_INCLUDE_DIRS})
# configure_file(cppnetlibConfig.cmake.in
#     "${PROJECT_BINARY_DIR}/cppnetlibConfig.cmake" @ONLY)
# # ... for the install tree
# set(CONF_INCLUDE_DIRS "\${CPPNETLIB_CMAKE_DIR}/${REL_INCLUDE_DIR}")
# set(CONF_INCLUDE_DIRS ${CONF_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS})
# configure_file(cppnetlibConfig.cmake.in
#     "${PROJECT_BINARY_DIR}${CMAKE_FILES_DIRECTORY}/cppnetlibConfig.cmake" @ONLY)
# # ... for both
# configure_file(cppnetlibConfigVersion.cmake.in
#     "${PROJECT_BINARY_DIR}/cppnetlibConfigVersion.cmake" @ONLY)
# # Install the cppnetlibConfig.cmake and cppnetlibConfigVersion.cmake
# install(FILES
#     "${PROJECT_BINARY_DIR}${CMAKE_FILES_DIRECTORY}/cppnetlibConfig.cmake"
#     "${PROJECT_BINARY_DIR}/cppnetlibConfigVersion.cmake"
#     DESTINATION "${INSTALL_CMAKE_DIR}"
#     COMPONENT dev)
# # Install the export set for use with the install-tree
# install(EXPORT cppnetlibTargets
#     DESTINATION "${INSTALL_CMAKE_DIR}"
#     COMPONENT dev)
# Contributor Covenant Code of Conduct

## Our Pledge

In the interest of fostering an open and welcoming environment, we as
contributors and maintainers pledge to making participation in our project and
our community a harassment-free experience for everyone, regardless of age, body
size, disability, ethnicity, gender identity and expression, level of experience,
nationality, personal appearance, race, religion, or sexual identity and
orientation.

## Our Standards

Examples of behavior that contributes to creating a positive environment
include:

* Using welcoming and inclusive language
* Being respectful of differing viewpoints and experiences
* Gracefully accepting constructive criticism
* Focusing on what is best for the community
* Showing empathy towards other community members

Examples of unacceptable behavior by participants include:

* The use of sexualized language or imagery and unwelcome sexual attention or
advances
* Trolling, insulting/derogatory comments, and personal or political attacks
* Public or private harassment
* Publishing others' private information, such as a physical or electronic
  address, without explicit permission
* Other conduct which could reasonably be considered inappropriate in a
  professional setting

## Our Responsibilities

Project maintainers are responsible for clarifying the standards of acceptable
behavior and are expected to take appropriate and fair corrective action in
response to any instances of unacceptable behavior.

Project maintainers have the right and responsibility to remove, edit, or
reject comments, commits, code, wiki edits, issues, and other contributions
that are not aligned to this Code of Conduct, or to ban temporarily or
permanently any contributor for other behaviors that they deem inappropriate,
threatening, offensive, or harmful.

## Scope

This Code of Conduct applies both within project spaces and in public spaces
when an individual is representing the project or its community. Examples of
representing a project or community include using an official project e-mail
address, posting via an official social media account, or acting as an appointed
representative at an online or offline event. Representation of a project may be
further defined and clarified by project maintainers.

## Enforcement

Instances of abusive, harassing, or otherwise unacceptable behavior
may be reported by contacting the project team at
glyn.matthews@gmail.com or dberris@google.com. All complaints will be
reviewed and investigated and will result in a response that is deemed
necessary and appropriate to the circumstances. The project team is
obligated to maintain confidentiality with regard to the reporter of
an incident.  Further details of specific enforcement policies may be
posted separately.

Project maintainers who do not follow or enforce the Code of Conduct in good
faith may face temporary or permanent repercussions as determined by other
members of the project's leadership.

## Attribution

This Code of Conduct is adapted from the [Contributor Covenant][homepage], version 1.4,
available at [http://contributor-covenant.org/version/1/4][version]

[homepage]: http://contributor-covenant.org
[version]: http://contributor-covenant.org/version/1/4/
Boost Software License - Version 1.0 - August 17th, 2003

Permission is hereby granted, free of charge, to any person or organization
obtaining a copy of the software and accompanying documentation covered by
this license (the "Software") to use, reproduce, display, distribute,
execute, and transmit the Software, and to prepare derivative works of the
Software, and to permit third-parties to whom the Software is furnished to
do so, all subject to the following:

The copyright notices in the Software and this entire statement, including
the above license grant, this restriction and the following disclaimer,
must be included in all copies of the Software, in whole or in part, and
all derivative works of the Software, unless such copies or derivative
works are solely in the form of machine-executable object code generated by
a source language processor.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE, TITLE AND NON-INFRINGEMENT. IN NO EVENT
SHALL THE COPYRIGHT HOLDERS OR ANYONE DISTRIBUTING THE SOFTWARE BE LIABLE
FOR ANY DAMAGES OR OTHER LIABILITY, WHETHER IN CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
DEALINGS IN THE SOFTWARE.
C++ Networking Library
Goals and Scope


Objectives
----------

 o  Develop a high quality, portable, easy to use C++ networking library

 o  Enable users to easily extend the library

 o  Lower the barrier to entry for cross-platform network-aware C++ 
    applications


Goals
-----

 *  Implement a simple message implementation which can be used in
    network protocol-specific routines for inter-operability and
    to provide a generic interface to manipulating network-oriented
    messages.

 *  Implement easy to use protocol client libraries such as (but not
    limited to):
    
        -  HTTP 1.0/1.1
        -  (E)SMTP
        -  SNMP
        -  ICMP

 *  Implement an easy to embed HTTP server container type that supports
    most modern HTTP 1.1 features.
    
 *  Implement an efficient easy to use URI class/parser.

 *  Implement a fully compliant cross-platform asynchronous DNS resolver
    either as a wrapper to external (C) libraries or as hand-rolled
    implementation.

 *  Implement a MIME handler which builds message objects from either
    data retrieved from the network or other sources and create
    text/binary representations from existing message objects intended
    for transport over the network.


Scope
-----

 *  The library will provide a generic message class which is intended 
    to be the common message type used by the protocol libraries.

 *  The library will only contain client implementations for the various 
    supported protocols.

 *  The library will use only STL and Boost C++ library components, 
    utilities, and libraries throughout the implementation.

 *  The library will strive to use C++ templates and template 
    metaprogramming techniques in order to not require the building of
    external shared/static libraries. In other words, the library will be
    header-only and compliant with the C++ standard.


C++ Network Library
===================

Modern C++ network programming libraries.

.. image:: https://travis-ci.org/cpp-netlib/cpp-netlib.svg?branch=master
    :target: https://travis-ci.org/cpp-netlib/cpp-netlib

.. image:: https://scan.coverity.com/projects/6714/badge.svg
    :target: https://scan.coverity.com/projects/cpp-netlib

.. image:: https://img.shields.io/badge/license-boost-blue.svg
    :target: https://github.com/cpp-netlib/cpp-netlib/blob/master/LICENSE_1_0.txt

Join us on Slack: http://slack.cpp-netlib.org/

Subscribe to the mailing list: https://groups.google.com/forum/#!forum/cpp-netlib

Downloading cpp-netlib
----------------------

You can find official release packages of the library at::

    http://github.com/cpp-netlib/cpp-netlib/downloads

If you want the latest code from the master branch of the project, you can
follow these instructions for cloning the project repository::

    $ git clone https://github.com/cpp-netlib/cpp-netlib
    $ cd cpp-netlib
    $ git submodule init
    $ git submodule update

Introduction
------------

cpp-netlib is a collection of network-related routines/implementations
geared towards providing a robust cross-platform networking library.
cpp-netlib offers the following implementations:

  *  Common Message Type -- A generic message type which can be used
     to encapsulate and store message-related information, used by all
     network implementations as the primary means of data exchange.
  *  Network protocol message parsers -- A collection of parsers which
     generate message objects from strings.
  *  Adapters and Wrappers -- A collection of Adapters and wrappers aimed
     towards making the message type STL friendly.
  *  Network protocol client and server implementations -- A collection
     of network protocol implementations that include embeddable client
     and server types.

This library is released under the Boost Software License (please see
http://boost.org/LICENSE_1_0.txt or the accompanying LICENSE_1_0.txt file
for the full text.

Building and Installing
-----------------------

To build the libraries you will need to have CMake version 2.8 or higher
installed appropriately in your system.

::

    $ cmake --version
    cmake version 2.8.1

It is recommended that you build cpp-netlib outside of the source directory, to
avoid having issues with CMake generated files polluting the source directory::

    $ mkdir ~/cpp-netlib-build
    $ cd ~/cpp-netlib-build
    $ cmake -DCMAKE_BUILD_TYPE=Debug     \
    >       -DCMAKE_C_COMPILER=clang     \
    >       -DCMAKE_CXX_COMPILER=clang++ \
    >       $HOME/cpp-netlib    # we're assuming this is where cpp-netlib is.

Once CMake is done with generating the Makefiles and configuring the project,
you can now build the tests and run them::

    $ cd ~/cpp-netlib-build
    $ make
    $ make test

If for some reason some of the tests fail, you can send the files in
``Testing/Temporary/`` as attachments to the cpp-netlib `developers mailing
list`_.

.. _`developers mailing list`: cpp-netlib@googlegroups.com

Running Tests
-------------

If you want to run the tests that come with cpp-netlib, there are a few things
you will need. These are:

  * A compiler (GCC 4.x, Clang 3.6, MSVC 2008)
  * A build tool (CMake_ is required)
  * OpenSSL headers (optional)

.. note:: This assumes that you have cpp-netlib at the top-level of
          your home directory.
.. _CMake: https://cmake.org/

Hacking on cpp-netlib
---------------------

cpp-netlib uses git_ for tracking work and is hosted on GitHub_. 
cpp-netlib is hosted on GitHub_ following the GitHub recommended practice of
forking the repository and submitting pull requests to the source repository.
You can read more about the forking_ process and submitting `pull requests`_ if
you're not familiar with either process yet. cpp-netib follows the GitHub pull
request model for accepting patches. You can read more about the process at
http://cpp-netlib.org/process.html#pull-requests. 

.. _git: http://git-scm.com/
.. _GitHub: http://github.com/
.. _forking: http://help.github.com/forking/
.. _`pull requests`: http://help.github.com/pull-requests/

Because cpp-netlib is released under the `Boost Software License`_ it is
recommended that any file you make changes to bear your copyright notice
alongside the original authors' copyright notices on the file. Typically the
copyright notices are at the top of each file in the project.

.. _`Boost Software License`: http://www.boost.org/LICENSE_1_0.txt

You can read about the cpp-netlib style guide at
http://cpp-netlib.org/style-guide.html.

The main "upstream" repository is at http://github.com/cpp-netlib/cpp-netlib.

Contact and Support
-------------------

In case you have any questions or would like to make feature requests, you can
contact the development team through the `developers mailing list`_
or by filing issues at http://github.com/cpp-netlib/cpp-netlib/issues.

Join us on Slack: http://slack.cpp-netlib.org/

.. _`developers mailing list`: cpp-netlib@googlegroups.com

You can reach the maintainers of the project through::

    Dean Michael Berris (dberris@google.com)

    Glyn Matthews (glyn.matthews@gmail.com)
To Do list for Boost.Mime:

General:
* Finish the test suites
** Compare results to python parser
** Try to parse some bad mime inputs
--> Added 0019-NoBoundary test
* Integrate into cpp-netlib
* Write some docs

Specific:
* Rename make_mime into something better. Parse, Encode?
--> Changed the name to 'parse_mime', and made the stream and iterator versions use the same name
* Start using boost::exception
* Look into making the parsing restartable
* Figure out how to include_directories(${CPP-NETLIB_SOURCE_DIR})
file ( COPY TestMessages DESTINATION ${CMAKE_CURRENT_BINARY_DIR} )

#This test causes a "too many sections" error on Windows MinGW64
#(MSVC has /bigobj, MinGW does not)
if (NOT(${CMAKE_CXX_COMPILER_ID} MATCHES GNU AND ${CMAKE_SYSTEM_NAME} MATCHES "Windows"))
  if ( Boost_FOUND )
    add_executable ( mime-roundtrip mime-roundtrip.cpp )
    target_link_libraries ( mime-roundtrip ${Boost_LIBRARIES}
      ${CMAKE_THREAD_LIBS_INIT})
    set_target_properties( mime-roundtrip
        PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/tests)
    add_test ( mime-roundtrip ${CPP-NETLIB_BINARY_DIR}/tests/mime-roundtrip )
  endif ()
endif()

Here we can collect some statistics about different areas of
performance in the :mod:`cpp-netlib`, including run-time and
compile-time.
include_directories(${CPP-NETLIB_SOURCE_DIR})
find_package( Boost 1.45.0 COMPONENTS unit_test_framework system regex thread filesystem )

add_library(cppnetlib-uri STATIC ${CPP-NETLIB_SOURCE_DIR}/libs/network/src/parse_uri_impl.cpp)
add_library(cppnetlib-server-parsers STATIC ${CPP-NETLIB_SOURCE_DIR}/libs/network/src/server_request_parsers_impl.cpp)

.. _contents:

Contents
--------

.. toctree::
   :maxdepth: 4

   index.rst
   whats_new.rst
   getting_started.rst
   examples.rst
   reference.rst
   references.rst
.. _examples:

Examples
========

The :mod:`cpp-netlib` is a practical library that is designed to aid
the development of applications for that need to communicate using
common networking protocols.  The following set of examples describe a
series of realistic examples that use the :mod:`cpp-netlib` for these
kinds of application.  All examples are built using CMake.

HTTP examples
`````````````

The HTTP component of the :mod:`cpp-netlib` contains a client and server.
The examples that follow show how to use both for programs that can be
embedded into larger applications.

.. toctree::
   :maxdepth: 1

   examples/http/http_client
   examples/http/simple_wget
   examples/http/hello_world_server
   examples/http/hello_world_client
   examples/http/atom_reader
   examples/http/twitter_search
.. _getting_started:

*****************
 Getting Started
*****************

Downloading an official release
===============================

You can find links to the latest official release from the project's official
website:

    http://cpp-netlib.org/

All previous stable versions of :mod:`cpp-netlib` can be downloaded from
Github_ from this url:

    http://github.com/cpp-netlib/cpp-netlib/downloads

Each release is available as gzipped (Using the command
``tar xzf cpp-netlib.tar.gz``) or bzipped (Using ``tar xjf
cpp-netlib.tar.bz2``) tarball, or as a zipfile (``unzip
cpp-netlib.zip``, or on Windows using a tool such as 7zip_).

.. _Github: http://github.com/cpp-netlib/cpp-netlib/downloads
.. _7zip: http://www.7-zip.org/

Downloading a development version
=================================

The :mod:`cpp-netlib` uses Git_ for source control, so to use any
development versions Git must be installed on your system.

Using the command line, the command to get the latest code is:

::

    shell$ git clone git://github.com/cpp-netlib/cpp-netlib.git

This should be enough information get to started.  To do more complex
things with Git, such as pulling changes or checking out a new branch,
refer to the `Git documentation`_.

.. note:: Previous versions of :mod:`cpp-netlib` referred to the
   *mikhailberis* repository as the main development repository. This
   account is still valid, but not always up-to-date. In the interest of
   consistency, the main repository has been changed to *cpp-netlib*.

Windows users need to use msysGit_, and to invoke the command above
from a shell.

For fans of Subversion_, the same code can be checked out from
http://svn.github.com/cpp-netlib/cpp-netlib.git.

.. _Git: http://git-scm.com/
.. _`Git documentation`: http://git-scm.com/documentation
.. _msysGit: http://code.google.com/p/msysgit/downloads/list
.. _Subversion: http://subversion.tigris.org/

.. note:: The :mod:`cpp-netlib` project is hosted on GitHub_ and follows the
   prescribed development model for GitHub_ based projects. This means in case
   you want to submit patches, you will have to create a fork of the project
   (read up on forking_) and then submit a pull request (read up on submitting
   `pull requests`_).

.. _forking: http://help.github.com/forking/
.. _`pull requests`: http://help.github.com/pull-requests/

Getting Boost
=============

:mod:`cpp-netlib` depends on Boost_.  It should work for any version
of Boost above 1.50.0.  If Boost is not installed on your system, the
latest package can be found on the `Boost web-site`_.  The environment
variable ``BOOST_ROOT`` must be defined, which must be the full path
name of the top directory of the Boost distribution.  Although Boost
is mostly header only, applications built using :mod:`cpp-netlib`
still requires linking with `Boost.System`_, `Boost.Date_time`_, and
`Boost.Regex`_.

.. _Boost: http://www.boost.org/doc/libs/release/more/getting_started/index.html
.. _`Boost web-site`: http://www.boost.org/users/download/
.. _`Boost.System`: http://www.boost.org/libs/system/index.html
.. _`Boost.Date_time`: http://www.boost.org/libs/date_time/index.html
.. _`Boost.Regex`: http://www.boost.org/libs/regex/index.html

.. note:: You can follow the steps in the `Boost Getting Started`_ guide to
   install Boost into your development system.

.. _`Boost Getting Started`:
   http://www.boost.org/doc/libs/release/more/getting_started/index.html

.. warning:: There is a known incompatibility between :mod:`cpp-netlib` and
   Boost 1.46.1 on some compilers. It is not recommended to use :mod:`cpp-netlib`
   with Boost 1.46.1. Some have reported though that Boost 1.47.0
   and :mod:`cpp-netlib` work together better.

Getting CMake
=============

The :mod:`cpp-netlib` uses CMake_ to generate platform-specific build files. If
you intend to run the test suite, you can follow the instructions below.
Otherwise, you don't need CMake to use :mod:`cpp-netlib` in your project. The
:mod:`cpp-netlib` requires CMake version 2.8 or higher.

.. _CMake: http://www.cmake.org/

Let's assume that you have unpacked the :mod:`cpp-netlib` at the top of your
HOME directory. On Unix-like systems you will typically be able to change into
your HOME directory using the command ``cd ~``. This sample below assumes that
the ``~/cpp-netlib`` directory exists, and is the top-level directory of the
:mod:`cpp-netlib` release.

Building with CMake
===================

To build the tests that come with :mod:`cpp-netlib`, we first need to configure the
build system to use our compiler of choice. This is done by running the
``cmake`` command at the top-level directory of :mod:`cpp-netlib` with
additional parameters::

    $ mkdir ~/cpp-netlib-build
    $ cd ~/cpp-netlib-build
    $ cmake -DCMAKE_BUILD_TYPE=Debug \
    >       -DCMAKE_C_COMPILER=gcc   \
    >       -DCMAKE_CXX_COMPILER=g++ \
    >       ../cpp-netlib

.. note::

    While it's not compulsory, it's recommended that
    :mod:`cpp-netlib` is built outside the source directory.
    For the purposes of documentation, we'll assume that all
    builds are done in ``~/cpp-netlib-build``.

If you intend to use the SSL support when using the HTTP client libraries in
:mod:`cpp-netlib`, you may need to build it with OpenSSL_ installed or at least
available to CMake. If you have the development headers for OpenSSL_ installed
on your system when you build :mod:`cpp-netlib`, CMake will be able to detect it
and set the ``BOOST_NETWORK_ENABLE_HTTPS`` macro when building the library to
support HTTPS URIs.

One example for building the library with OpenSSL_ support with a custom
(non-installed) version of OpenSSL_ is by doing the following::

    $ cmake -DCMAKE_BUILD_TYPE=Debug \
    >       -DCMAKE_C_COMPILER=clang \
    >       -DCMAKE_CXX_COMPILER=clang++ \
    >       -DOPENSSL_ROOT_DIR=/Users/dberris/homebrew/Cellar/openssl/1.0.1f
    >       ../cpp-netlib

.. _OpenSSL: http://www.openssl.org/

You can also use a different root directory for the Boost_ project by using the
``-DBOOST_ROOT`` configuration option to CMake. This is useful if you intend to
build the library with a specific version of Boost that you've built in a
separate directory::

    $ cmake -DCMAKE_BUILD_TYPE=Debug \
    >       -DCMAKE_C_COMPILER=clang \
    >       -DCMAKE_CXX_COMPILER=clang++ \
    >       -DOPENSSL_ROOT_DIR=/Users/dberris/homebrew/Cellar/openssl/1.0.1f \
    >       -DBOOST_ROOT=/Users/dberris/Source/boost_1_55_0
    >       ../cpp-netlib

Building on Linux
~~~~~~~~~~~~~~~~~

On Linux, this will generate the appropriate Makefiles that will enable you to
build and run the tests and examples that come with :mod:`cpp-netlib`. To build
the tests, you can run ``make`` in the same top-level directory of
``~/cpp-netlib-build``::

    $ make

.. note:: Just like with traditional GNU Make, you can add the ``-j`` parameter
   to specify how many parallel builds to run. In case you're in a sufficiently
   powerful system and would like to parallelize the build into 4 jobs, you can
   do this with::

       make -j4

   As a caveat, :mod:`cpp-netlib` is heavy on template metaprogramming and will
   require a lot of computing and memory resources to build the individual
   tests. Do this at the risk of thrashing_ your system.  However, this
   compile-time burden is much reduced in recent versions.

.. _thrashing: http://en.wikipedia.org/wiki/Thrashing_(computer_science)

Once the build has completed, you can now run the test suite by issuing::

    $ make test

You can install :mod:`cpp-netlib` by issuing::

    $ sudo make install

By default this installs :mod:`cpp-netlib` into ``/usr/local``.

.. note:: As of version 0.9.3, :mod:`cpp-netlib` produces three static
   libraries.  Using GCC on Linux these are::

      libcppnetlib-client-connections.a
      libcppnetlib-server-parsers.a
      libcppnetlib-uri.a

   Users can find them in ``~/cpp-netlib-build/libs/network/src``.

Building On Windows
~~~~~~~~~~~~~~~~~~~

If you're using the Microsoft Visual C++ compiler or the Microsoft Visual Studio
IDE and you would like to build :mod:`cpp-netlib` from within Visual Studio, you
can look for the solution and project files as the artifacts of the call to
``cmake`` -- the file should be named ``CPP-NETLIB.sln`` (the solution) along
with a number of project files for Visual Studio.

.. note:: As of version 0.9.3, :mod:`cpp-netlib` produces three static
   libraries.  Using Visual C++ on Windows they are::

      cppnetlib-client-connections.lib
      cppnetlib-server-parsers.lib
      cppnetlib-uri.lib

   Users can find them in ``~/cpp-netlib-build/libs/network/src``.

Using :mod:`cpp-netlib`
=======================

CMake projects
~~~~~~~~~~~~~~

Projects using CMake can add the following lines in their ``CMakeLists.txt`` to
be able to use :mod:`cpp-netlib`::

   set ( CMAKE_PREFIX_PATH ${CMAKE_PREFIX_PATH} ~/cpp-netlib-build )
   find_package ( cppnetlib 0.11.0 REQUIRED )
   include_directories ( ${CPPNETLIB_INCLUDE_DIRS} )
   target_link_libraries ( MyApplication ${CPPNETLIB_LIBRARIES} )

.. note:: Setting ``CMAKE_PREFIX_PATH`` is only required when :mod:`cpp-netlib`
   is not installed to a location that CMake searches.  When :mod:`cpp-netlib`
   is installed to the default location (``/usr/local``), ``CMake`` can find it.

.. note:: We assume that ``MyApplication`` is the application that you are
   building and which depends on :mod:`cpp-netlib`.


Reporting Issues, Getting Support
=================================

In case you find yourself stuck or if you've found a bug (or you want to just
join the discussion) you have a few options to choose from.

For reporting bugs, feature requests, and asking questions about the
implementation and/or the documentation, you can go to the GitHub issues page
for the project at http://github.com/cpp-netlib/cpp-netlib/issues.

You can also opt to join the developers mailing list for a more personal
interaction with the developers of the project. You can join the mailing list
through http://groups.google.com/forum/#!forum/cpp-netlib.

.. _index:
.. rubric:: Straightforward network programming in modern C++

.. :Authors: Glyn Matthews <glyn.matthews@gmail.com>
.. 	  Dean Michael Berris <dberris@google.com>
.. :Date: 2014-10-01
.. :Version: 0.11.0
.. :Description: Complete user documentation, with examples, for the :mod:`cpp-netlib`.
.. :Copyright: Copyright Glyn Matthews, Dean Michael Berris 2008-2013.
..             Copyrigh 2013 Google, Inc.
..             Distributed under the Boost Software License, Version
..             1.0. (See accompanying file LICENSE_1_0.txt or copy at
..             http://www.boost.org/LICENSE_1_0.txt)

Getting cpp-netlib
==================

You can find out more about the :mod:`cpp-netlib` project at
http://cpp-netlib.org/.

**Download**

You can get the latest official version of the library from the official
project website at:

    http://cpp-netlib.org/

This version of :mod:`cpp-netlib` is tagged as cpp-netlib-0.11.0 in the GitHub_
repository. You can find more information about the progress of the development
by checking our GitHub_ project page at:

    http://github.com/cpp-netlib/cpp-netlib

**Support**

You can ask questions, join the discussion, and report issues to the
developers mailing list by joining via:

    https://groups.google.com/group/cpp-netlib

You can also file issues on the Github_ issue tracker at:

    http://github.com/cpp-netlib/cpp-netlib/issues

We are a growing community and we are happy to accept new
contributions and ideas.

C++ Network Library
===================

:mod:`cpp-netlib` is a library collection that provides application layer
protocol support using modern C++ techniques.  It is light-weight, fast,
portable and is intended to be as easy to configure as possible.

Hello, world!
=============

The :mod:`cpp-netlib` allows developers to write fast, portable
network applications with the minimum of fuss.

An HTTP server-client example can be written in tens of lines of code.
The client is as simple as this:

.. code-block:: cpp

    using namespace boost::network;
    using namespace boost::network::http;

    client::request request_("http://127.0.0.1:8000/");
    request_ << header("Connection", "close");
    client client_;
    client::response response_ = client_.get(request_);
    std::string body_ = body(response_);

And the corresponding server code is listed below:

.. code-block:: cpp

    namespace http = boost::network::http;

    struct handler;
    typedef http::server<handler> http_server;

    struct handler {
        void operator() (http_server::request const &request,
                         http_server::response &response) {
            response = http_server::response::stock_reply(
                http_server::response::ok, "Hello, world!");
        }

        void log(http_server::string_type const &info) {
            std::cerr << "ERROR: " << info << '\n';
        }
    };

    int main(int arg, char * argv[]) {
        handler handler_;
        http_server::options options(handler_);
        http_server server_(
            options.address("0.0.0.0")
                   .port("8000"));
        server_.run();
    }

Want to learn more?
===================

    * :ref:`Take a look at the getting started guide <getting_started>`
    * :ref:`Learn from some simple examples <examples>`
    * :ref:`Find out what's new <whats_new>`
    * :ref:`Discover more through the full reference <reference>`
    * :ref:`Full table of contents <contents>`

.. warning:: Be aware that not all features are stable.  The generic
   	     message design is under review and the URI and HTTP
   	     client implementation will continue to undergo
   	     refactoring.  Future versions will include support for
   	     other network protocols.


.. _Boost: http://www.boost.org/
.. _GitHub: http://github.com/

.. _reference:

Reference Manual
================

This reference manual refers to the API documentation of the public interfaces
to the different client and/or server implementations within :mod:`cpp-netlib`.

.. toctree::
   :maxdepth: 2

   reference/http_client
   reference/http_request
   reference/http_response
   reference/http_server

References
==========

About :mod:`cpp-netlib`
~~~~~~~~~~~~~~~~~~~~~~~

* `BoostCon 2010 Slides`_
* `BoostCon 2010 Paper`_

Other sources
~~~~~~~~~~~~~

* `Template Metaprogramming`_: The best guide to C++ template metaprogramming.
* `HTTP 1.0`_: The HTTP 1.0 specification.
* `HTTP 1.1 (RFC 2616)`_: The HTTP 1.1 specification.
* `URI Generic Syntax (RFC 3986)`_: Generic URI syntax specification.
* `Format for Literal IPv6 Addresses in URLs (RFC 2732)`_: Literal IPv6 Addresses in URLs.

.. _`BoostCon 2010 Slides`: http://www.filetolink.com/b0e89d06
.. _`BoostCon 2010 Paper`: http://github.com/downloads/mikhailberis/cpp-netlib-boostcon-paper/cpp-netlib.pdf
.. _`Template Metaprogramming`: http://www.boostpro.com/mplbook/
.. _`HTTP 1.0`: http://www.w3.org/Protocols/HTTP/1.0/spec.html
.. _`HTTP 1.1 (RFC 2616)`: http://www.w3.org/Protocols/rfc2616/rfc2616.html
.. _`URI Generic Syntax (RFC 3986)`: http://www.ietf.org/rfc/rfc3986.txt
.. _`Format for Literal IPv6 Addresses in URLs (RFC 2732)`: http://www.ietf.org/rfc/rfc2732.txt
.. _whats_new:

************
 What's New
************

:mod:`cpp-netlib` 0.12
----------------------

* Added a code of conduct.
* Add TLS SNI hostname support in the HTTP Client options.
* Changes based on Coverity reports.
* Replace std::bind with lambdas.
* Use std::shared_ptr instead of boost::shared_ptr.
* Use standalone Asio instead of Boost.Asio.
* No Boost library (shared or static) dependencies.
* Use doxygen for documentation, integrated with Breathe to Sphinx.
* Require C++11 for builds, removes support for non-C++11 compilers.
* Update documentation for hello_world_server
* Use googletest for tests
* Fix XCode-generated debug binaries caused by URI parser complexity
* Remove synchronous client implementation.
* Remove support for connection keepalive (only supported in synchronous client).
* Disable SSLv3 by default.
* Use sanitisers in continuous integration (address and thread sanitiser).
* Update minimum Boost to 1.57. Always use shared libs from Boost.

:mod:`cpp-netlib` 0.11
----------------------

v0.11.2
~~~~~~~
* Support a source_port setting for connections made by the client per-request.
* Allow using cpp-netlib without OpenSSL.
* Fix build breakage for Visual Studio 2015.
* Add more options for HTTP client use of SSL/TLS options/ciphers.
* Made client_get_timeout_test less flaky.
* Fixes to URI encoding issues with multibyte strings.
* Make cpp-netlib not crash on unstable networks.
* Allow parsing empty query parameters (`#499`_).
* CMake build changes to simplify dependencies on cppnetlib-client-connections.
* Handle EOF correctly (`#496`_).
* Fix fileserver example to chunk data correctly.
* Copy hostname to avoid dangling reference to a temporary request object. (`#482`_)
* Catch exceptions in parse_headers to avoid propagating issues in parsing upwards.
* Fix some GCC warnings on signed/unsigned comparison.
* Support environment variable-based peer verification (via OpenSSL).
* Support IPv6 connections.
* Support certificate-based verification, and option to always verify hosts.

.. _`#499`: https://github.com/cpp-netlib/cpp-netlib/issues/499
.. _`#496`: https://github.com/cpp-netlib/cpp-netlib/issues/496
.. _`#482`: https://github.com/cpp-netlib/cpp-netlib/issues/482


v0.11.1
~~~~~~~
* Add support for request timeouts.
* Build configuration fixes.
* Support for Travis CI in-project config.
* Make the response parser more flexible to support older/ad-hoc servers that don't have standard format responses.
* Fix some instability in the client destructor.
* MSVC 2010 specific fixes.

v0.11.0
~~~~~~~
* Fix thread leak in DNS resolution failure (`#245`_)
* Remove unsupported `client_fwd.hpp` header (`#277`_)
* Remove support for header-only usage (`#129`_) -- this means that the BOOST_NETWORK_NO_LIB option is no longer actually supported.
* Deprecate Synchronous Client implementations (`#279`_)
* Support streaming body chunks for PUT/POST client requests (`#27`_)
* Fix non-case-sensitive header parsing for some client tags (`#313`_)
* Remove unsupported Jamfiles from the whole project (`#316`_)
* Add ``make install`` for Linux and OS X (`#285`_) 
* Fix incorrect Body processing (`#69`_)
* Support chunked transfer encoding from HTTP responses (`#86`_)
* Make OS X Clang builds use C++11 and libc++. 
* Update Boost requirement to 1.54.0.
* Experimental Base64 encoding/decoding library (`#287`_)
* *Known test failure:* OS X Xcode Clang 5.0 + Boost 1.54.0 + libc++ don't play
  well with Boost.Serialization issues, mitigate test breakage but
  ``cpp-netlib-utils_base64_test`` still fails in this platform. (`#287`_) 
* Provide a client option to always validate peers for HTTPS requests made by
  the client. (`#349`_)
* Back-port fix for `#163`_ for improved URI parsing.
* Added support for client-side certificates and private keys (`#361`_).

.. _`#129`: https://github.com/cpp-netlib/cpp-netlib/issues/129
.. _`#163`: https://github.com/cpp-netlib/cpp-netlib/issues/163
.. _`#245`: https://github.com/cpp-netlib/cpp-netlib/issues/245
.. _`#277`: https://github.com/cpp-netlib/cpp-netlib/issues/277
.. _`#279`: https://github.com/cpp-netlib/cpp-netlib/issues/279
.. _`#27`: https://github.com/cpp-netlib/cpp-netlib/issues/27
.. _`#285`: https://github.com/cpp-netlib/cpp-netlib/issues/285
.. _`#287`: https://github.com/cpp-netlib/cpp-netlib/issues/287
.. _`#313`: https://github.com/cpp-netlib/cpp-netlib/issues/313
.. _`#316`: https://github.com/cpp-netlib/cpp-netlib/issues/316
.. _`#349`: https://github.com/cpp-netlib/cpp-netlib/issues/349
.. _`#69`: https://github.com/cpp-netlib/cpp-netlib/issues/69
.. _`#86`: https://github.com/cpp-netlib/cpp-netlib/issues/86
.. _`#361`: https://github.com/cpp-netlib/cpp-netlib/pull/361

:mod:`cpp-netlib` 0.10
----------------------

v0.10.1
~~~~~~~
* Documentation updates (`#182`_, `#265`_, `#194`_, `#233`_, `#255`_)
* Fix issue with async server inadvertently stopping from listening when
  accepting a connection fails. (`#172`_)
* Allow overriding and ultimately removing defaulted headers from HTTP
  requests. (`#263`_)
* Add `-Wall` to the base rule for GCC builds. (`#264`_)
* Make the server implementation throw on startup errors. (`#166`_)

.. _`#182`: https://github.com/cpp-netlib/cpp-netlib/issues/182
.. _`#265`: https://github.com/cpp-netlib/cpp-netlib/issues/265
.. _`#194`: https://github.com/cpp-netlib/cpp-netlib/issues/194
.. _`#172`: https://github.com/cpp-netlib/cpp-netlib/issues/172
.. _`#263`: https://github.com/cpp-netlib/cpp-netlib/issues/263
.. _`#233`: https://github.com/cpp-netlib/cpp-netlib/issues/233
.. _`#264`: https://github.com/cpp-netlib/cpp-netlib/issues/264
.. _`#255`: https://github.com/cpp-netlib/cpp-netlib/issues/255
.. _`#166`: https://github.com/cpp-netlib/cpp-netlib/issues/166

v0.10.0
~~~~~~~
* Added support for more HTTP status codes (206, 408, 412, 416, 507).
* Refactored the parser for chunked encoding.
* Fixed parsing chunked encoding if the response body has ``<chunk>CLRF<hex>CLRF<data>``.
* Added librt dependency on Linux.
* Check the callback in the asynchronous client before calling it.
* Fixed issues `#110`_, `#168`_, `#213`_.

.. _`#110`: https://github.com/cpp-netlib/cpp-netlib/issues/110
.. _`#168`: https://github.com/cpp-netlib/cpp-netlib/issues/168
.. _`#213`: https://github.com/cpp-netlib/cpp-netlib/issues/213

:mod:`cpp-netlib` 0.9
---------------------

v0.9.5
~~~~~~
* Removed dependency on Boost.Parameter from HTTP client and server.
* Fixed for Clang error on Twitter example.
* Added source port to the request (HTTP server).
* Updated CMake config for MSVC 2010/2012.
* Now support chunked content encoding in client response parsing.
* Fixed bug with client not invoking callback when a request fails.

v0.9.4
~~~~~~
* Lots of URI fixes.
* Fixed async_server's request handler so it doesn't make copies of the supplied handler.
* Fix for issue `#73`_ regarding SSL connections ending in short read errors.
* Final C++03-only release.

.. _`#73`: https://github.com/cpp-netlib/cpp-netlib/issues/73

v0.9.3
~~~~~~
* URI, HTTP client and HTTP server are now built as static libraries (``libcppnetlib-uri.a``, ``libcppnetlib-client-connections.a`` and ``libcppnetlib-server-parsers.a`` on Linux and ``cppnetlib-uri.lib``, ``cppnetlib-client-connections.lib`` and ``cppnetlib-server-parsers.lib`` on Windows).
* Updated URI parser.
* A new URI builder.
* URI support for IPv6 RFC 2732.
* Fixed issues `#67`_, `#72`_, `#78`_, `#79`_, `#80`_, `#81`_, `#82`_, `#83`_.
* New examples for the HTTP client, including an Atom feed, an RSS feed and a
  very simple client that uses the Twitter Search API.

.. _`#67`: https://github.com/cpp-netlib/cpp-netlib/issues/67
.. _`#72`: https://github.com/cpp-netlib/cpp-netlib/issues/72
.. _`#78`: https://github.com/cpp-netlib/cpp-netlib/issues/78
.. _`#79`: https://github.com/cpp-netlib/cpp-netlib/issues/79
.. _`#80`: https://github.com/cpp-netlib/cpp-netlib/issues/80
.. _`#81`: https://github.com/cpp-netlib/cpp-netlib/issues/81
.. _`#82`: https://github.com/cpp-netlib/cpp-netlib/issues/82
.. _`#83`: https://github.com/cpp-netlib/cpp-netlib/issues/83

v0.9.2
~~~~~~
* Critial bug fixes to v0.9.1.

v0.9.1
~~~~~~
* Introduced macro ``BOOST_NETWORK_DEFAULT_TAG`` to allow for programmatically
  defining the default flag to use throughout the compilation unit.
* Support for streaming body handlers when performing HTTP client operations.
  See documentation for HTTP client interface for more information.
* Numerous bug fixes from v0.9.0.
* Google, Inc. contributions.

v0.9.0
~~~~~~
* **IMPORTANT BREAKING CHANGE**: By default all compile-time heavy parser
  implementations are now compiled to external static libraries. In order to use
  :mod:`cpp-netlib` in header-only mode, users must define the preprocessor
  macro ``BOOST_NETWORK_NO_LIB`` before including any :mod:`cpp-netlib` header.
  This breaks code that relied on the version 0.8.x line where the library is
  strictly header-only.
* Fix issue #41: Introduce a macro ``BOOST_NETWORK_HTTP_CLIENT_DEFAULT_TAG``
  which makes the default HTTP client use ``tags::http_async_8bit_udp_resolve``
  as the tag.
* Fix issue #40: Write the status line and headers in a single buffer write
  instead of two writes.
* More consistent message API for client and server messages (request and
  response objects).
* Refactoring of internal implementations to allow better separation of concerns
  and more manageable coding/documentation.
* Client and server constructors that support Boost.Parameter named parameters.
* Client and server constructors now take in an optional reference to a Boost.Asio
  ``io_service`` to use internally.
* Documentation updates to reflect new APIs.

:mod:`cpp-netlib` 0.8
---------------------

* Updates to URI unit tests and documentation.
* More documentation, covering the HTTP Client and HTTP Server APIs
* Asynchronous HTTP Server that now supports running request handlers on a
  different thread pool.
* An initial thread pool implementation, using Boost.Asio underneath.
* Adding a ready(...) wrapper to check whether a response object returned by
  the asynchronous client in 0.7 already has all the parts available.
* Some attempts at lowering compile time costs.

:mod:`cpp-netlib` 0.7
---------------------

* Radical documentation overhaul
* Asynchronous HTTP client
* Tag dispatch overhaul, using Boost.MPL
* HTTP Client Facade refactoring
* Bug fixes for HTTP 1.1 response parsing
* Minimized code repetition with some header macro's
* Configurable HTTPS support in the library with ``BOOST_NETWORK_ENABLE_HTTPS``


:mod:`cpp-netlib` 0.6
---------------------

* Many fixes for MSVC compiler

:mod:`cpp-netlib` 0.5
---------------------

* An embeddable HTTP 1.1 server
* An HTTP 1.1 client upgraded to support HTTPS
* An updated URI parser implementation
* An asynchronous HTTP 1.1 client
* An HTTP 1.1 client that supports streaming function handlers
.. _atom_reader:

******************
 Atom feed reader
******************

The next examples show some simple, more practical applications using
the HTTP client.  The first one reads a simple Atom_ feed and prints
the titles of each entry to the console.

.. _Atom: http://en.wikipedia.org/wiki/Atom_(standard)

The code
========

.. code-block:: c++

   #include "atom.hpp"
   #include <boost/network/protocol/http/client.hpp>
   #include <boost/foreach.hpp>
   #include <iostream>

   int main(int argc, char * argv[]) {
       using namespace boost::network;

       if (argc != 2) {
           std::cout << "Usage: " << argv[0] << " <url>" << std::endl;
           return 1;
       }

       try {
           http::client client;
           http::client::request request(argv[1]);
           request << header("Connection", "close");
           http::client::response response = client.get(request);
           atom::feed feed(response);

           std::cout << "Feed: " << feed.title()
	   	     << " (" << feed.subtitle() << ")" << std::endl;
           BOOST_FOREACH(const atom::entry &entry, feed) {
               std::cout << entry.title()
	       		 << " (" << entry.published() << ")" << std::endl;
           }
       }
       catch (std::exception &e) {
           std::cerr << e.what() << std::endl;
       }

       return 0;
   }

Building and running ``atom_reader``
====================================

.. code-block:: bash

    $ cd ~/cpp-netlib-build
    $ make atom_reader

And to run the example from the command line to access the feed that
lists of all the commits on cpp-netlib's master branch:

.. code-block:: bash

    $ ./example/atom_reader https://github.com/cpp-netlib/cpp-netlib/commits/master.atom

Diving into the code
====================

Most of this will now be familiar.  The response is passed to the
constructor to the ``atom::feed`` class, which parses the resultant
XML.  To keep this example as simple as possible, `rapidxml`_, a
header-only XML parser library, was used to parse the response.

.. _`rapidxml`: http://rapidxml.sourceforge.net/

A similar example using RSS feeds exists in
``libs/network/example/rss``.
.. _hello_world_http_client:

***************************
 "Hello world" HTTP client
***************************

Since we have a "Hello World" HTTP server, let's then create an HTTP client to
access that server. This client will be similar to the HTTP client we made
earlier in the documentation.

The code
========

We want to create a simple HTTP client that just makes a request to the HTTP
server that we created earlier. This really simple client will look like this:

.. code-block:: c++

    #include <boost/network/protocol/http/client.hpp>
    #include <string>
    #include <sstream>
    #include <iostream>

    namespace http = boost::network::http;

    int main(int argc, char * argv[]) {
        if (argc != 3) {
            std::cerr << "Usage: " << argv[0] << " address port" << std::endl;
            return 1;
        }

        try {
            http::client client;
            std::ostringstream url;
            url << "http://" << argv[1] << ":" << argv[2] << "/";
            http::client::request request(url.str());
            http::client::response response =
                client.get(request);
            std::cout << body(response) << std::endl;
        } catch (std::exception & e) {
            std::cerr << e.what() << std::endl;
            return 1;
        }
        return 0;
    }

Building and running the client
===============================

Just like with the HTTP Server and HTTP client example before, we can build this
example by doing the following on the shell:

.. code-block:: bash

    $ cd ~/cpp-netlib-build
    $ make hello_world_client

This example can be run from the command line as follows:

.. code-block:: bash

    $ ./example/hello_world_client http://127.0.0.1:8000

.. note:: This assumes that you have the ``hello_world_server`` running on
   localhost port 8000.

Diving into the code
====================

All this example shows is how easy it is to write an HTTP client that connects
to an HTTP server, and gets the body of the response. The relevant lines are:

.. code-block:: c++

    http::client client;
    http::client::request request(url.str());
    http::client::response response =
        client.get(request);
    std::cout << body(response) << std::endl;

You can then imagine using this in an XML-RPC client, where you can craft the
XML-RPC request as payload which you can pass as the body to a request, then
perform the request via HTTP:

.. code-block:: c++

    http::client client;
    http::client::request request("http://my.webservice.com/");
    http::client::response =
        client.post(request, some_xml_string, "application/xml");
    std::data = body(response);

The next set of examples show some more practical applications using
the :mod:`cpp-netlib` HTTP client.
.. _hello_world_http_server:

***************************
 "Hello world" HTTP server
***************************

Now that we've seen how we can deal with request and response objects from the
client side, we'll see how we can then use the same abstractions on the server
side. In this example we're going to create a simple HTTP Server in C++ using
:mod:`cpp-netlib`.

The code
========

The :mod:`cpp-netlib` provides the framework to develop embedded HTTP
servers.  For this example, the server is configured to return a
simple response to any HTTP request.

.. code-block:: c++

    #include <boost/network/protocol/http/server.hpp>
    #include <iostream>

    namespace http = boost::network::http;

    struct hello_world;
    typedef http::server<hello_world> server;

    struct hello_world {
        void operator()(server::request const &request, server::response &response) {
            server::string_type ip = source(request);
            unsigned int port = request.source_port;
            std::ostringstream data;
            data << "Hello, " << ip << ':' << port << '!';
            response = server::response::stock_reply(server::response::ok, data.str());
        }
        void log(const server::string_type& message) {
            std::cerr << "ERROR: " << message << std::endl;
        }
    };

    int main(int argc, char *argv[]) {

        if (argc != 3) {
            std::cerr << "Usage: " << argv[0] << " address port" << std::endl;
            return 1;
        }

        try {
            hello_world handler;
            server::options options(handler);
            server server_(options.address(argv[1]).port(argv[2]));
            server_.run();
        }
        catch (std::exception &e) {
            std::cerr << e.what() << std::endl;
            return 1;
        }

        return 0;
    }

This is about a straightforward as server programming will get in C++.

Building and running the server
===============================

Just like with the HTTP client, we can build this example by doing the following
on the shell:

.. code-block:: bash

    $ cd ~/cpp-netlib-build
    $ make hello_world_server

The first two arguments to the ``server`` constructor are the host and
the port on which the server will listen.  The third argument is the
the handler object defined previously.  This example can be run from
a command line as follows:

.. code-block:: bash

    $ ./example/hello_world_server 0.0.0.0 8000

.. note:: If you're going to run the server on port 80, you may have to run it
   as an administrator.

Diving into the code
====================

Let's take a look at the code listing above in greater detail.

.. code-block:: c++

    #include <boost/network/protocol/http/server.hpp>

This header contains all the code needed to develop an HTTP server with
:mod:`cpp-netlib`.

.. code-block:: c++

    struct hello_world;
    typedef http::server<hello_world> server;

    struct hello_world {
        void operator()(server::request const &request, server::response &response) {
            server::string_type ip = source(request);
            unsigned int port = request.source_port;
            std::ostringstream data;
            data << "Hello, " << ip << ':' << port << '!';
            response = server::response::stock_reply(server::response::ok, data.str());
        }
        void log(const server::string_type& message) {
            std::cerr << "ERROR: " << message << std::endl;
        }
    };

``hello_world`` is a functor class which handles HTTP requests.
All the operator does here is return an HTTP response with HTTP code 200
and the body ``"Hello, <ip>:<port>!"``. The ``<ip>`` in this case would be
the IP address of the client that made the request and ``<port>`` the clients port.

There are a number of pre-defined stock replies differentiated by
status code with configurable bodies.
All the supported enumeration values for the response status codes can be found
in ``boost/network/protocol/http/impl/response.ipp``.

.. code-block:: c++

    hello_world handler;
    server::options options(handler);
    server server_(options.address(argv[1]).port(argv[2]));
    server_.run();

The ``server`` constructor requires an object of the ``options`` class,
this object stores all needed options, especially the host and
the port on which the server will listen.
The ``options`` constructor's single argument is the handler object defined previously.

.. note:: In this example, the server is specifically made to be single-threaded.
   In a multi-threaded server, you would invoke the ``hello_world::run`` member
   method in a set of threads. In a multi-threaded environment you would also
   make sure that the handler does all the necessary synchronization for shared
   resources across threads. The handler is passed by reference to the server
   constructor and you should ensure that any calls to the ``operator()`` overload
   are thread-safe.

.. _http_client:

*************
 HTTP client
*************

The first code example is the simplest thing you can do with the
:mod:`cpp-netlib`.  The application is a simple HTTP client, which can
be found in the subdirectory ``libs/network/example/http_client.cpp``.
All this example doing is creating and sending an HTTP request to a server
and printing the response body.

The code
========

Without further ado, the code to do this is as follows:

.. code-block:: c++

    #include <boost/network/protocol/http/client.hpp>
    #include <iostream>

    int main(int argc, char *argv[]) {
        using namespace boost::network;

        if (argc != 2) {
            std::cout << "Usage: " << argv[0] << " [url]" << std::endl;
            return 1;
        }

        http::client client;
        http::client::request request(argv[1]);
        request << header("Connection", "close");
        http::client::response response = client.get(request);
        std::cout << body(response) << std::endl;

        return 0;
    }

Running the example
===================

You can then run this to get the Boost_ website:

.. code-block:: bash

    $ cd ~/cpp-netlib-build
    $ make http_client
    $ ./example/http_client http://www.boost.org/

.. _Boost: http://www.boost.org/

.. note::

    The instructions for all these examples assume that
    :mod:`cpp-netlib` is build outside the source tree,
    according to `CMake conventions`_.  For the sake of
    consistency we assume that this is in the
    ``~/cpp-netlib-build`` directory.

.. _`CMake conventions`: http://www.cmake.org/Wiki/CMake_FAQ#What_is_an_.22out-of-source.22_build.3F

Diving into the code
====================

Since this is the first example, each line will be presented and
explained in detail.

.. code-block:: c++

    #include <boost/network/protocol/http/client.hpp>

All the code needed for the HTTP client resides in this header.

.. code-block:: c++

    http::client client;

First we create a ``client`` object.  The ``client`` abstracts all the
connection and protocol logic.  The default HTTP client is version
1.1, as specified in `RFC 2616`_.

.. code-block:: c++

    http::client::request request(argv[1]);

Next, we create a ``request`` object, with a URI string passed as a
constructor argument.

.. code-block:: c++

    request << header("Connection", "close");

:mod:`cpp-netlib` makes use of stream syntax and *directives* to allow
developers to build complex message structures with greater
flexibility and clarity.  Here, we add the HTTP header "Connection:
close" to the request in order to signal that the connection will be
closed after the request has completed.

.. code-block:: c++

    http::client::response response = client.get(request);

Once we've built the request, we then make an HTTP GET request
throught the ``http::client`` from which an ``http::response`` is
returned.  ``http::client`` supports all common HTTP methods: GET,
POST, HEAD, DELETE.

.. code-block:: c++

    std::cout << body(response) << std::endl;

Finally, though we don't do any error checking, the response body is
printed to the console using the ``body`` directive.

That's all there is to the HTTP client.  In fact, it's possible to
compress this to a single line:

.. code-block:: c++

   std::cout << body(http::client().get(http::request("http://www.boost.org/")));

The next example will introduce the ``uri`` class.

.. _`RFC 2616`: http://www.w3.org/Protocols/rfc2616/rfc2616.html
.. _simple_wget:

***************
 Simple `wget`
***************

This example is a very simple implementation of a ``wget`` style
clone.  It's very similar to the previous example, but introduces the
``uri`` class.

The code
========

.. code-block:: c++

   #include <boost/network/protocol/http/client.hpp>
   #include <boost/network/uri.hpp>
   #include <string>
   #include <fstream>
   #include <iostream>

   namespace http = boost::network::http;
   namespace uri = boost::network::uri;

   namespace {
   std::string get_filename(const uri::uri &url) {
       std::string path = uri::path(url);
       std::size_t index = path.find_last_of('/');
       std::string filename = path.substr(index + 1);
       return filename.empty()? "index.html" : filename;
   }
   } // namespace

   int
   main(int argc, char *argv[]) {
       if (argc != 2) {
           std::cerr << "Usage: " << argv[0] << " url" << std::endl;
           return 1;
       }

       try {
           http::client client;
           http::client::request request(argv[1]);
           http::client::response response = client.get(request);

           std::string filename = get_filename(request.uri());
           std::cout << "Saving to: " << filename << std::endl;
           std::ofstream ofs(filename.c_str());
           ofs << static_cast<std::string>(body(response)) << std::endl;
       }
       catch (std::exception &e) {
           std::cerr << e.what() << std::endl;
           return 1;
       }

       return 0;
   }

Running the example
===================

You can then run this to copy the Boost_ website:

.. code-block:: bash

    $ cd ~/cpp-netlib-build
    $ make simple_wget
    $ ./example/simple_wget http://www.boost.org/
    $ cat index.html

.. _Boost: http://www.boost.org/

Diving into the code
====================

As with ``wget``, this example simply makes an HTTP request to the
specified resource, and saves it on the filesystem.  If the file name
is not specified, it names the resultant file as ``index.html``.

The new thing to note here is use of the ``uri`` class.  The ``uri``
takes a string as a constructor argument and parses it.  The ``uri``
parser is fully-compliant with `RFC 3986`_.  The URI is provided in
the following header:

.. _`RFC 3986`: http://www.ietf.org/rfc/rfc3986.txt

.. code-block:: c++

   #include <boost/network/uri.hpp>

Most of the rest of the code is familiar from the previous example.
To retrieve the URI resource's file name, the following function is
provided:

.. code-block:: c++

   std::string get_filename(const uri::uri &url) {
       std::string path = uri::path(url);
       std::size_t index = path.find_last_of('/');
       std::string filename = path.substr(index + 1);
       return filename.empty()? "index.html" : filename;
   }

The ``uri`` interface provides access to its different components:
``scheme``, ``user_info``, ``host``, ``port``, ``path``, ``query`` and
``fragment``.  The code above takes the URI path to determine the
resource name.

Next we'll develop a simple client/server application using
``http::server`` and ``http::client``.
.. _twitter_search:

****************
 Twitter search
****************

This example uses `Twitter's search API`_ to list recent tweets given
a user query.  New features introduced here include the URI builder
and ``uri::encoded`` function.

.. _`Twitter's search API`: https://dev.twitter.com/docs/using-search

The code
========

.. code-block:: c++

   #include <boost/network/protocol/http/client.hpp>
   #include "rapidjson/rapidjson.h"
   #include "rapidjson/document.h"
   #include <iostream>

   int main(int argc, char *argv[]) {
       using namespace boost::network;
       using namespace rapidjson;

       if (argc != 2) {
           std::cout << "Usage: " << argv[0] << " <query>" << std::endl;
           return 1;
       }

       try {
           http::client client;

           uri::uri base_uri("http://search.twitter.com/search.json");

           std::cout << "Searching Twitter for query: " << argv[1] << std::endl;
           uri::uri search;
           search << base_uri << uri::query("q", uri::encoded(argv[1]));
           http::client::request request(search);
           http::client::response response = client.get(request);

           Document d;
           if (!d.Parse<0>(response.body().c_str()).HasParseError()) {
               const Value &results = d["results"];
               for (SizeType i = 0; i < results.Size(); ++i)
               {
                   const Value &user = results[i]["from_user_name"];
                   const Value &text = results[i]["text"];
                   std::cout << "From: " << user.GetString() << std::endl
                             << "  " << text.GetString() << std::endl
                             << std::endl;
               }
           }
       }
       catch (std::exception &e) {
           std::cerr << e.what() << std::endl;
       }

       return 0;
   }

.. note:: To parse the results of these queries, this example uses
          `rapidjson`_, a header-only library that is released under
          the `MIT License`_.

.. _`rapidjson`: https://github.com/miloyip/rapidjson
.. _`MIT License`: http://www.opensource.org/licenses/mit-license.php

Building and running ``twitter_search``
=======================================

.. code-block:: bash

    $ cd ~/cpp-netlib-build
    $ make twitter_search

Twitter provides a powerful set of operators to modify the behaviour
of search queries.  Some examples are provided below:

.. code-block:: bash

   $ ./example/twitter_search "Lady Gaga"

Returns any results that contain the exact phrase "Lady Gaga".

.. code-block:: bash

   $ ./example/twitter_search "#olympics"

Returns any results with the #olympics hash tag.

.. code-block:: bash

   $ ./example/twitter_search "flight :("

Returns any results that contain "flight" and have a negative
attitude.

More examples can be found on `Twitter's search API`_ page.

Diving into the code
====================

.. code-block:: c++

   uri::uri base_uri("http://search.twitter.com/search.json");

   std::cout << "Searching Twitter for query: " << argv[1] << std::endl;
   uri::uri search;
   search << base_uri << uri::query("q", uri::encoded(argv[1]));

The :mod:`cpp-netlib` URI builder uses a stream-like syntax to allow
developers to construct more complex URIs.  The example above re-uses
the same base URI and allows the command line argument to be used as
part of the URI query.  The builder also supports percent encoding
using the ``encoded`` directive.

HTTP Client API
===============

General
-------

:mod:`cpp-netlib` includes and implements a number of HTTP clients that you can
use and embed in your own applications. All of the HTTP client implementations:

  * **Cannot be copied.** This means you may have to store instances of the
    clients in dynamic memory if you intend to use them as function parameters
    or pass them around in smart pointers or by reference.
  * **Assume that requests made are independent of each other.** There currently
    is no cookie or session management system built-in to cpp-netlib's HTTP client
    implementations.

The HTTP clients all share the same API, but the internals are documented in
terms of what is different and what to expect with the different
implementations.

Features
--------

The HTTP client implementation supports requesting secure HTTP (HTTPS) content
only in the following situations:

  * **Client libraries are built with ``BOOST_NETWORK_ENABLE_HTTPS``.** This
    tells the implementation to use HTTPS-specific code to handle HTTPS-based
    content when making connections associated with HTTPS URI's. This requires
    a dependency on OpenSSL_.
  * **The ``BOOST_NETWORK_ENABLE_HTTPS`` macro is set when compiling user
    code.** It is best to define this either at compile-time of all code using
    the library, or before including any of the client headers.

To use the client implementations that support HTTPS URIs, you may explicitly
do the following:

.. code-block:: c++

   #define BOOST_NETWORK_ENABLE_HTTPS
   #include <boost/network/include/http/client.hpp>

This forces HTTPS support to be enabled and forces a dependency on OpenSSL_.
This dependency is imposed by `Boost.Asio`_

.. _OpenSSL: http://www.openssl.org/
.. _`Boost.Asio`: http://www.boost.org/libs/asio

Client Implementation
---------------------

There is a single user-facing template class named ``basic_client`` which takes
three template parameters:

  * **Tag** - which static tag you choose that defines the behavior of the client.

  * **http_version_major** - an unsigned int that defines the HTTP major version
    number, this directly affects the HTTP messages sent by the client.

  * **http_version_minor** - an unsigned int that defines the HTTP minor version
    number.

.. include:: ../in_depth/http_client_tags.rst

In the above table the tags follow a pattern for describing the behavior
introduced by the tags. This pattern is shown below:

    <protocol>_<modifier>_<character-width>_<resolve-strategy>

For example, the tag ``http_default_8bit_tcp_resolve`` indicates the protocol
``http``, a modifier ``default``, a character width of ``8bit``, and a resolve
strategy of ``tcp_resolve``.

The  client is implemented as an `Active Object`_. This means that the client
has and manages its own lifetime thread, and returns values that are
asynchronously filled in. The response object encapsulates futures which get
filled in once the values are available.

.. _`Active Object`: http://en.wikipedia.org/wiki/Active_object

.. note:: The client objects are thread safe, and can be shared across many
   threads. Each request starts a sequence of asynchronous operations dedicated
   to that request. The client does not re-cycle connections and uses a
   one-request-one-connection model.

When a client object is destroyed, it waits for all pending asynchronous
operations to finish. Errors encountered during operations on retrieving data
from the response objects cause exceptions to be thrown -- therefore it is best
that if a client object is constructed, it should outlive the response object
or be outside the try-catch block handling the errors from operations on
responses. In code, usage should look like the following:

.. code-block:: c++

    http::client client;
    try {
      http::client::response response = client.get("http://www.example.com/");
      std::cout << body(response);
    } catch (std::exception& e) {
      // deal with exceptions here
    }

A common mistake is to declare the client inside the try block which invokes
undefined behavior when errors arise from the handling of response objects.
Previous examples cited by the documentation showed the short version of the
code which didn't bother moving the ``http::client`` object outside of the same
``try`` block where the request/response objects are being used.

Member Functions
----------------

In this section we assume that the following typedef is in effect:

.. code-block:: c++

    typedef boost::network::http::basic_client<
        boost::network::http::tags::http_default_8bit_udp_resolve
        , 1
        , 1
        >
        client;

Also, that code using the HTTP client will have use the following header:

.. code-block:: c++

    #include <boost/network/include/http/client.hpp>

Constructors
~~~~~~~~~~~~

The client implementation can be default constructed, or customized at
initialization.

``client()``
    Default constructor.
``explicit client(client::options const &)``
    Constructor taking a ``client_options<Tag>`` object. The following table
    shows the options you can set on a ``client_options<Tag>`` instance.

Client Options
~~~~~~~~~~~~~~

.. doxygenclass:: boost::network::http::client_options
   :project: cppnetlib
   :members:

To use the above supported named parameters, you'll have code that looks like
the following:

.. code-block:: c++

    using namespace boost::network::http; // parameters are in this namespace
    client::options options;
    options.follow_redirects(true)
           .cache_resolved(true)
           .io_service(boost::make_shared<boost::asio::io_service>())
           .openssl_certificate("/tmp/my-cert")
           .openssl_verify_path("/tmp/ca-certs")
           .timeout(10);
    client client_(options);
    // use client_ as normal from here on out.

HTTP Methods
~~~~~~~~~~~~

The client implementation supports various HTTP methods. The following
constructs assume that a client has been properly constructed named ``client_``
and that there is an appropriately constructed request object named ``request_``
and that there is an appropriately constructed response object named
``response_`` like the following:

.. code-block:: c++

    using namespace boost::network::http;  // parameters are here
    client client_();
    client::request request_("http://cpp-netib.github.com/");
    client::response response_;


.. doxygenclass:: boost::network::http::basic_client
   :project: cppnetlib
   :members:
   :undoc-members:

.. doxygentypedef:: boost::network::http::client
   :project: cppnetlib

Streaming Body Handler
~~~~~~~~~~~~~~~~~~~~~~

As of v0.9.1 the library now offers a way to support a streaming body callback
function in all HTTP requests that expect a body part (GET, PUT, POST, DELETE).
A convenience macro is also provided to make callback handlers easier to write.
This macro is called ``BOOST_NETWORK_HTTP_BODY_CALLBACK`` which allows users to
write the following code to easily create functions or function objects that
are compatible with the callback function requirements.

An example of how to use the macro is shown below:

.. code-block:: c++

    struct body_handler {
        explicit body_handler(std::string & body)
        : body(body) {}

        BOOST_NETWORK_HTTP_BODY_CALLBACK(operator(), range, error) {
            // in here, range is the Boost.Range iterator_range, and error is
            // the Boost.System error code.
            if (!error)
                body.append(boost::begin(range), boost::end(range));
        }

        std::string & body;
    };

    // somewhere else
    std::string some_string;
    response_ = client_.get(request("http://cpp-netlib.github.com/"),
                            body_handler(some_string));

You can also use if for standalone functions instead if you don't want or need
to create a function object.

.. code-block:: c++

    BOOST_NETWORK_HTTP_BODY_CALLBACK(print_body, range, error) {
        if (!error)
            std::cout << "Received " << boost::distance(range) << "bytes."
                      << std::endl;
        else
            std::cout << "Error: " << error << std::endl;
    }

    // somewhere else
    response_ = client_.get(request("http://cpp-netlib.github.com/"),
                            print_body);

The ``BOOST_NETWORK_HTTP_BODY_CALLBACK`` macro is defined in
``boost/network/protocol/http/client/macros.hpp``.

HTTP Request
============

This part of the documentation talks about the publicly accessible API of the
HTTP Request objects. This section details the `Request Concepts`_ requirements,
the implemented and required Directives_, Modifiers_, and Wrappers_ that work
with the HTTP Request objects.

Request Concepts
----------------

There are two generally supported Request Concepts implemented in the library.
The first of two is the `Normal Client Request Concept`_ and the second is the
`Pod Server Request Concept`_.

The `Normal Client Request Concept`_ is what the HTTP Client interface requires.
All operations performed internally by the HTTP Client abide by the interface
required by this concept definition.

The `Pod Server Request Concept`_ is as the name suggests what the HTTP Server
implementation requires from Request Objects.

Switching on whether the `Request` concept chooses either of the `Normal Client
Request Concept`_ or the `Pod Server Request Concept`_ is done through the
nested ``tag`` type and whether that tag derives from the root tag ``pod``.
Simply, if the Request type's nested ``tag`` type derives from
``boost::network::tags::pod`` then it chooses to enforce the `Pod Server Request
Concept`_, otherwise it chooses the `Normal Client Request Concept`_.

Normal Client Request Concept
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A type models the Normal Client Request Concept if it models the `Message
Concept`_ and also supports the following constructs.

**Legend**

:R: The request type.
:r: An instance of R.
:S: The string type.
:s: An instance of S.
:P: The port type.
:p: An instance of P.

+-----------------------+-------------+----------------------------------------+
| Construct             | Result      | Description                            |
+=======================+=============+========================================+
| ``R::string_type``    | ``S``       | The nested ``string_type`` type.       |
+-----------------------+-------------+----------------------------------------+
| ``R::port_type``      | ``P``       | The nested ``port_type`` type.         |
+-----------------------+-------------+----------------------------------------+
| ``R r(s)``            | **NA**      | Construct a Request with an ``s``      |
|                       |             | provided. This treats ``s`` as the URI |
|                       |             | to where the request is destined for.  |
+-----------------------+-------------+----------------------------------------+
| ``host(request)``     | Convertible | Return the host to where the request   |
|                       | to ``S``    | is destined for.                       |
+-----------------------+-------------+----------------------------------------+
| ``port(request)``     | Convertible | Return the port to where the request   |
|                       | to ``P``    | is destined for.                       |
+-----------------------+-------------+----------------------------------------+
| ``path(request)``     | Convertible | Return the path included in the URI.   |
|                       | to ``S``    |                                        |
+-----------------------+-------------+----------------------------------------+
| ``query(request)``    | Convertible | Return the query part of the URI.      |
|                       | to ``S``    |                                        |
+-----------------------+-------------+----------------------------------------+
| ``anchor(request)``   | Convertible | Return the anchor part of the URI.     |
|                       | to ``S``    |                                        |
+-----------------------+-------------+----------------------------------------+
| ``protocol(request)`` | Convertible | Return the protocol/scheme part of the |
|                       | to ``S``    | URI.                                   |
+-----------------------+-------------+----------------------------------------+
| ``r << uri(s)``       | ``R&``      | Set the URI of the request.            |
+-----------------------+-------------+----------------------------------------+
| ``uri(r, s)``         | ``void``    | Set the URI of the request.            |
+-----------------------+-------------+----------------------------------------+

Pod Server Request Concept
~~~~~~~~~~~~~~~~~~~~~~~~~~

A type models the Pod Server Request Concept if it models the `Message Concept`_
and also supports the following constructs.

**Legend**

:R: The request type.
:r: An instance of R.
:S: The string type.
:I: An unsigned 8 bit integer.
:V: The vector type for headers.

+-------------------------------+--------+-------------------------------------+
| Construct                     | Result | Description                         |
+===============================+========+=====================================+
| ``R::string_type``            | ``S``  | The nested ``string_type`` type.    |
+-------------------------------+--------+-------------------------------------+
| ``R::headers_container_type`` | ``V``  | The nested                          |
|                               |        | ``headers_container_type`` type.    |
+-------------------------------+--------+-------------------------------------+
| ``r.source``                  | ``S``  | The nested source of the request.   |
+-------------------------------+--------+-------------------------------------+
| ``r.method``                  | ``S``  | The method of the request.          |
+-------------------------------+--------+-------------------------------------+
| ``r.destination``             | ``S``  | The destination of the request.     |
|                               |        | This is normally the URI of the     |
|                               |        | request.                            |
+-------------------------------+--------+-------------------------------------+
| ``r.version_major``           | ``I``  | The major version number part of    |
|                               |        | the request.                        |
+-------------------------------+--------+-------------------------------------+
| ``r.version_minor``           | ``I``  | The minor version number part of    |
|                               |        | the request.                        |
+-------------------------------+--------+-------------------------------------+
| ``r.headers``                 | ``V``  | The vector of headers.              |
+-------------------------------+--------+-------------------------------------+
| ``r.body``                    | ``S``  | The body of the request.            |
+-------------------------------+--------+-------------------------------------+

.. _Message Concept: ../in_depth/message.html#message-concept

Directives
----------

This section details the provided directives that are provided by
:mod:`cpp-netlib`. The section was written to assume that an appropriately
constructed request instance is either of the following:

.. code-block:: c++

    boost::network::http::basic_request<
      boost::network::http::tags::http_default_8bit_udp_resolve
    > request;

    // or

    boost::network::http::basic_request<
      boost::network::http::tags::http_server
    > request;

The section also assumes that there following using namespace declaration is in
effect:

.. code-block:: c++

    using namespace boost::network;

Directives are meant to be used in the following manner:

.. code-block:: c++

    request << directive(...);

.. warning::

    There are two versions of directives, those that are applicable to
    messages that support narrow strings (``std::string``) and those that are
    applicable to messages that support wide strings (``std::wstring``). The
    :mod:`cpp-netlib` implementation still does not convert wide strings into
    UTF-8 encoded narrow strings. This will be implemented in subsequent
    library releases.

    For now all the implemented directives are listed, even if some of them still
    do not implement things correctly.

*unspecified* ``source(std::string const & source_)``
    Create a source directive with a ``std::string`` as a parameter, to be set
    as the source of the request.
*unspecified* ``source(std::wstring const & source_)``
    Create a source directive with a ``std::wstring`` as a parameter, to be set
    as the source of the request.
*unspecified* ``destination(std::string const & source_)``
    Create a destination directive with a ``std::string`` as a parameter, to be
    set as the destination of the request.
*unspecified* ``destination(std::wstring const & source_)``
    Create a destination directive with a ``std::wstring`` as a parameter, to be
    set as the destination of the request.
*unspecified* ``header(std::string const & name, std::string const & value)``
    Create a header directive that will add the given name and value pair to the
    headers already associated with the request. In this case the name and
    values are both ``std::string``.
*unspecified* ``header(std::wstring const & name, std::wstring const & value)``
    Create a header directive that will add the given name and value pair to the
    headers already associated with the request. In this case the name and
    values are both ``std::wstring``.
*unspecified* ``remove_header(std::string const & name)``
    Create a remove_header directive that will remove all the occurences of the
    given name from the headers already associated with the request. In this
    case the name of the header is of type ``std::string``.
*unspecified* ``remove_header(std::wstring const & name)``
    Create a remove_header directive that will remove all the occurences of the
    given name from the headers already associated with the request. In this
    case the name of the header is of type ``std::wstring``.
*unspecified* ``body(std::string const & body_)``
    Create a body directive that will set the request's body to the given
    parameter. In this case the type of the body is an ``std::string``.
*unspecified* ``body(std::wstring const & body_)``
    Create a body directive that will set the request's body to the given
    parameter. In this case the type of the body is an ``std::wstring``.

Modifiers
---------

This section details the provided modifiers that are provided by
:mod:`cpp-netlib`.

``template <class Tag> inline void source(basic_request<Tag> & request, typename string<Tag>::type const & source_)``
    Modifies the source of the given ``request``. The type of ``source_`` is
    dependent on the ``Tag`` specialization of ``basic_request``.
``template <class Tag> inline void destination(basic_request<Tag> & request, typename string<Tag>::type const & destination_)``
    Modifies the destination of the given ``request``. The type of ``destination_`` is
    dependent on the ``Tag`` specialization of ``basic_request``.
``template <class Tag> inline void add_header(basic_request<Tag> & request, typename string<Tag>::type const & name, typename string<Tag>::type const & value)``
    Adds a header to the given ``request``. The type of the ``name`` and
    ``value`` parameters are dependent on the ``Tag`` specialization of
    ``basic_request``.
``template <class Tag> inline void remove_header(basic_request<Tag> & request, typename string<Tag>::type const & name)``
    Removes a header from the given ``request``. The type of the ``name``
    parameter is dependent on the ``Tag`` specialization of ``basic_request``.
``template <class Tag> inline void clear_headers(basic_request<Tag> & request)``
    Removes all headers from the given ``request``.
``template <class Tag> inline void body(basic_request<Tag> & request, typename string<Tag>::type const & body_)``
    Modifies the body of the given ``request``. The type of ``body_`` is
    dependent on the ``Tag`` specialization of ``basic_request``.

Wrappers
--------

This section details the provided request wrappers that come with
:mod:`cpp-netlib`. Wrappers are used to convert a message into a different type,
usually providing accessor operations to retrieve just part of the message. This
section assumes that the following using namespace directives are in
effect:

.. code-block:: c++

    using namespace boost::network;
    using namespace boost::network::http;

``template <class Tag>`` *unspecified* ``source(basic_request<Tag> const & request)``
    Returns a wrapper convertible to ``typename string<Tag>::type`` that
    provides the source of a given request.
``template <class Tag>`` *unspecified* ``destination(basic_request<Tag> const & request)``
    Returns a wrapper convertible to ``typename string<Tag>::type`` that
    provides the destination of a given request.
``template <class Tag>`` *unspecified* ``headers(basic_request<Tag> const & request)``
    Returns a wrapper convertible to ``typename headers_range<basic_request<Tag>
    >::type`` or ``typename basic_request<Tag>::headers_container_type`` that
    provides the headers of a given request.
``template <class Tag>`` *unspecified* ``body(basic_request<Tag> const & request)``
    Returns a wrapper convertible to ``typename string<Tag>::type`` that
    provides the body of a given request.


HTTP Response
=============

This part of the documentation talks about the publicly accessible API of the
HTTP Response objects. This section details the `Response Concept`_ requirements,
the implemented and required Directives_, Modifiers_, and Wrappers_ that work
with the HTTP Response objects.

.. note:: The HTTP server response object is a POD type, which doesn't support
   any of the following details. There are only a few fields available in the
   HTTP server response type, which can be seen in
   ``boost/network/protocol/http/impl/response.ipp``.

Response Concept
----------------

A type models the Response Concept if it models the `Message Concept`_ and also
supports the following constructs.

**Legend**

:R: The response type.
:r: An instance of R.
:S: The string type.
:s,e,g: Instances of S.
:P: The port type.
:p: An instance of P.
:V: The version type.
:v: An instance of v.
:T: The status type.
:t: An instance of T.
:M: The status message type.
:m: An instance of M.
:U: An unsigned 16-bit int.
:u: An instance of U.

.. note:: In the table below, the namespace ``traits`` is an alias for
   ``boost::network::http::traits``.

+-------------------------------------+----------+-----------------------------+
| Construct                           | Result   | Description                 |
+=====================================+==========+=============================+
| ``R::string_type``                  | ``S``    | The nested ``string_type``  |
|                                     |          | type.                       |
+-------------------------------------+----------+-----------------------------+
| ``traits::version<R>::type``        | ``V``    | The version type associated |
|                                     |          | with R.                     |
+-------------------------------------+----------+-----------------------------+
| ``traits::status<R>::type``         | ``T``    | The status type associated  |
|                                     |          | with R.                     |
+-------------------------------------+----------+-----------------------------+
| ``traits::status_message<R>::type`` | ``M``    | The status message type     |
|                                     |          | associated with R.          |
+-------------------------------------+----------+-----------------------------+
| ``r << version(v)``                 | ``R&``   | Sets the version of ``r``.  |
+-------------------------------------+----------+-----------------------------+
| ``r << status(t)``                  | ``R&``   | Sets the status of ``r``.   |
+-------------------------------------+----------+-----------------------------+
| ``r << status_message(m)``          | ``R&``   | Sets the status message of  |
|                                     |          | ``r``.                      |
+-------------------------------------+----------+-----------------------------+
| ``version(r, v)``                   | ``void`` | Sets the version of ``r``.  |
+-------------------------------------+----------+-----------------------------+
| ``status(r, t)``                    | ``void`` | Sets the status of ``r``.   |
+-------------------------------------+----------+-----------------------------+
| ``status_message(r, m)``            | ``void`` | Sets the status message of  |
|                                     |          | ``r``.                      |
+-------------------------------------+----------+-----------------------------+
| ``S e = version(r)``                | **NA**   | Get the version of ``r``.   |
+-------------------------------------+----------+-----------------------------+
| ``U u = status(r)``                 | **NA**   | Get the status of ``r``.    |
+-------------------------------------+----------+-----------------------------+
| ``S g = status_message(r)``         | **NA**   | Get the status message of   |
|                                     |          | ``r``.                      |
+-------------------------------------+----------+-----------------------------+

.. _Message Concept: ../in_depth/message.html#message-concept

Directives
----------

This section details the provided directives that are provided by
:mod:`cpp-netlib`. The section was written to assume that an appropriately
constructed response instance is either of the following:

.. code-block:: c++

    boost::network::http::basic_response<
      boost::network::http::tags::http_default_8bit_udp_resolve
    > response;

    // or

    boost::network::http::basic_response<
      boost::network::http::tags::http_server
    > response;

The section also assumes that there following using namespace declaration is in
effect:

.. code-block:: c++

    using namespace boost::network;

Directives are meant to be used in the following manner:

.. code-block:: c++

    response << directive(...);

.. warning:: There are four versions of directives, those that are applicable
   to messages that support narrow strings (``std::string``), those that are
   applicable to messages that support wide strings (``std::wstring``), those
   that are applicable to messages that support future-wrapped narrow and wide
   strings (``boost::shared_future<std::string>`` and
   ``boost::shared_future<std::wstring>``).

   The :mod:`cpp-netlib` implementation still does not convert wide strings into
   UTF-8 encoded narrow strings. This will be implemented in subsequent
   library releases.

   For now all the implemented directives are listed, even if some of them still
   do not implement things correctly.

*unspecified* ``source(std::string const & source_)``
    Create a source directive with a ``std::string`` as a parameter, to be set
    as the source of the response.
*unspecified* ``source(std::wstring const & source_)``
    Create a source directive with a ``std::wstring`` as a parameter, to be set
    as the source of the response.
*unspecified* ``source(boost::shared_future<std::string> const & source_)``
    Create a source directive with a ``boost::shared_future<std::string>`` as a parameter, to be set
    as the source of the response.
*unspecified* ``source(boost::shared_future<std::wstring> const & source_)``
    Create a source directive with a ``boost::shared_future<std::wstring>`` as a parameter, to be set
    as the source of the response.
*unspecified* ``destination(std::string const & source_)``
    Create a destination directive with a ``std::string`` as a parameter, to be
    set as the destination of the response.
*unspecified* ``destination(std::wstring const & source_)``
    Create a destination directive with a ``std::wstring`` as a parameter, to be
    set as the destination of the response.
*unspecified* ``destination(boost::shared_future<std::string> const & destination_)``
    Create a destination directive with a ``boost::shared_future<std::string>`` as a parameter, to be set
    as the destination of the response.
*unspecified* ``destination(boost::shared_future<std::wstring> const & destination_)``
    Create a destination directive with a ``boost::shared_future<std::wstring>`` as a parameter, to be set
    as the destination of the response.
*unspecified* ``header(std::string const & name, std::string const & value)``
    Create a header directive that will add the given name and value pair to the
    headers already associated with the response. In this case the name and
    values are both ``std::string``.
*unspecified* ``header(std::wstring const & name, std::wstring const & value)``
    Create a header directive that will add the given name and value pair to the
    headers already associated with the response. In this case the name and
    values are both ``std::wstring``.
*unspecified* ``remove_header(std::string const & name)``
    Create a remove_header directive that will remove all the occurences of the
    given name from the headers already associated with the response. In this
    case the name of the header is of type ``std::string``.
*unspecified* ``remove_header(std::wstring const & name)``
    Create a remove_header directive that will remove all the occurences of the
    given name from the headers already associated with the response. In this
    case the name of the header is of type ``std::wstring``.
*unspecified* ``body(std::string const & body_)``
    Create a body directive that will set the response's body to the given
    parameter. In this case the type of the body is an ``std::string``.
*unspecified* ``body(std::wstring const & body_)``
    Create a body directive that will set the response's body to the given
    parameter. In this case the type of the body is an ``std::wstring``.
*unspecified* ``body(boost::shared_future<std::string> const & body_)``
    Create a body directive that will set the response's body to the given
    parameter. In this case the type of the body is an ``boost::shared_future<std::string>``.
*unspecified* ``body(boost::shared_future<std::wstring> const & body_)``
    Create a body directive that will set the response's body to the given
    parameter. In this case the type of the body is an ``boost::shared_future<std::wstring>``.
*unspecified* ``version(std::string const & version_)``
    Create a version directive that will set the response's version to the given
    parameter. In this case the type of the version is an ``std::string``.

    Note that this version includes the full ``"HTTP/"`` string.
*unspecified* ``version(std::wstring const & version_)``
    Create a version directive that will set the response's version to the given
    parameter. In this case the type of the version is an ``std::wstring``.

    Note that this version includes the full ``"HTTP/"`` string.
*unspecified* ``version(boost::shared_future<std::string> const & version_)``
    Create a version directive that will set the response's version to the given
    parameter. In this case the type of the version is an ``boost::shared_future<std::string>``.

    Note that this version includes the full ``"HTTP/"`` string.
*unspecified* ``version(boost::shared_future<std::wstring> const & version_)``
    Create a version directive that will set the response's version to the given
    parameter. In this case the type of the version is an ``boost::shared_future<std::wstring>``.

    Note that this version includes the full ``"HTTP/"`` string.
*unspecified* ``status_message(std::string const & status_message_)``
    Create a status_message directive that will set the response's status_message to the given
    parameter. In this case the type of the status_message is an ``std::string``.

    Note that this status_message includes the full ``"HTTP/"`` string.
*unspecified* ``status_message(std::wstring const & status_message_)``
    Create a status_message directive that will set the response's status_message to the given
    parameter. In this case the type of the status_message is an ``std::wstring``.

    Note that this status_message includes the full ``"HTTP/"`` string.
*unspecified* ``status_message(boost::shared_future<std::string> const & status_message_)``
    Create a status_message directive that will set the response's status_message to the given
    parameter. In this case the type of the status_message is an ``boost::shared_future<std::string>``.

    Note that this status_message includes the full ``"HTTP/"`` string.
*unspecified* ``status_message(boost::shared_future<std::wstring> const & status_message_)``
    Create a status_message directive that will set the response's status_message to the given
    parameter. In this case the type of the status_message is an ``boost::shared_future<std::wstring>``.

    Note that this status_message includes the full ``"HTTP/"`` string.
*unspecified* ``status(boost::uint16_t status_)``
    Create a status directive that will set the response's status to the given
    parameter. In this case the type of ``status_`` is ``boost::uint16_t``.
*unspecified* ``status(boost::shared_future<boost::uint16_t> const & status_)``
    Create a status directive that will set the response's status to the given
    parameter. In this case the type of ``status_`` is ``boost::shared_future<boost::uint16_t>``.

Modifiers
---------

This section details the provided modifiers that are provided by
:mod:`cpp-netlib`.

``template <class Tag> inline void source(basic_response<Tag> & response, typename string<Tag>::type const & source_)``
    Modifies the source of the given ``response``. The type of ``source_`` is
    dependent on the ``Tag`` specialization of ``basic_response``.
``template <class Tag> inline void source(basic_response<Tag> & response, boost::shared_future<typename string<Tag>::type> const & source_)``
    Modifies the source of the given ``response``. The type of ``source_`` is
    dependent on the ``Tag`` specialization of ``basic_response``.
``template <class Tag> inline void destination(basic_response<Tag> & response, typename string<Tag>::type const & destination_)``
    Modifies the destination of the given ``response``. The type of ``destination_`` is
    dependent on the ``Tag`` specialization of ``basic_response``.
``template <class Tag> inline void destination(basic_response<Tag> & response, boost::shared_future<typename string<Tag>::type> const & destination_)``
    Modifies the destination of the given ``response``. The type of ``destination_`` is
    dependent on the ``Tag`` specialization of ``basic_response``.
``template <class Tag> inline void add_header(basic_response<Tag> & response, typename string<Tag>::type const & name, typename string<Tag>::type const & value)``
    Adds a header to the given ``response``. The type of the ``name`` and
    ``value`` parameters are dependent on the ``Tag`` specialization of
    ``basic_response``.
``template <class Tag> inline void remove_header(basic_response<Tag> & response, typename string<Tag>::type const & name)``
    Removes a header from the given ``response``. The type of the ``name``
    parameter is dependent on the ``Tag`` specialization of ``basic_response``.
``template <class Tag> inline void headers(basic_response<Tag> & response, typename headers_container<basic_response<Tag> >::type const & headers_)``
    Sets the whole headers contained in ``response`` as the given parameter
    ``headers_``.
``template <class Tag> inline void headers(basic_response<Tag> & response, boost::shared_future<typename headers_container<basic_response<Tag> >::type> const & headers_)``
    Sets the whole headers contained in ``response`` as the given parameter
    ``headers_``.
``template <class Tag> inline void clear_headers(basic_response<Tag> & response)``
    Removes all headers from the given ``response``.
``template <class Tag> inline void body(basic_response<Tag> & response, typename string<Tag>::type const & body_)``
    Modifies the body of the given ``response``. The type of ``body_`` is
    dependent on the ``Tag`` specialization of ``basic_response``.
``template <class Tag> inline void body(basic_response<Tag> & response, boost::shared_future<typename string<Tag>::type> const & body_)``
    Modifies the body of the given ``response``. The type of ``body_`` is
    dependent on the ``Tag`` specialization of ``basic_response``.
``template <class Tag> inline void version(basic_response<Tag> & response, typename traits::version<basic_response<Tag> >::type const & version_)``
    Modifies the version of the given ``response``. The type of ``version_`` is
    dependent on the ``Tag`` specialization of ``basic_response``.
``template <class Tag> inline void status(basic_response<Tag> & response, typename traits::status<basic_response<Tag> >::type const & status_)``
    Modifies the status of the given ``response``. The type of ``status_`` is
    dependent on the ``Tag`` specialization of ``basic_response``.
``template <class Tag> inline void status_message(basic_response<Tag> & response, typename traits::status_message<basic_response<Tag> >::type const & status_message_)``
    Modifies the status message of the given ``response``. The type of ``status_message_`` is
    dependent on the ``Tag`` specialization of ``basic_response``.

Wrappers
--------

This section details the provided response wrappers that come with
:mod:`cpp-netlib`. Wrappers are used to convert a message into a different type,
usually providing accessor operations to retrieve just part of the message. This
section assumes that the following using namespace directives are in
effect:

.. code-block:: c++

    using namespace boost::network;
    using namespace boost::network::http;

``template <class Tag>`` *unspecified* ``source(basic_response<Tag> const & response)``
    Returns a wrapper convertible to ``typename string<Tag>::type`` that
    provides the source of a given response.
``template <class Tag>`` *unspecified* ``destination(basic_response<Tag> const & response)``
    Returns a wrapper convertible to ``typename string<Tag>::type`` that
    provides the destination of a given response.
``template <class Tag>`` *unspecified* ``headers(basic_response<Tag> const & response)``
    Returns a wrapper convertible to ``typename headers_range<basic_response<Tag>
    >::type`` or ``typename basic_response<Tag>::headers_container_type`` that
    provides the headers of a given response.
``template <class Tag>`` *unspecified* ``body(basic_response<Tag> const & response)``
    Returns a wrapper convertible to ``typename string<Tag>::type`` that
    provides the body of a given response.
``template <class Tag>`` *unspecified* ``version(basic_response<Tag> const & response)``
    Returns a wrapper convertible to ``typename string<Tag>::type`` that
    provides the version of the given response.
``template <class Tag>`` *unspecified* ``status(basic_response<Tag> const & response)``
    Returns a wrapper convertible to ``typename boost::uint16_t`` that
    provides the status of the given response.
``template <class Tag>`` *unspecified* ``status_message(basic_response<Tag> const & response)``
    Returns a wrapper convertible to ``typename string<Tag>::type`` that
    provides the status message of the given response.

HTTP Server API
===============

General
-------

:mod:`cpp-netlib` includes and implements and asynchronous HTTP server
implementation that you can use and embed in your own applications. The HTTP
Server implementation:

  * **Cannot be copied.** This means you may have to store instances of the HTTP
    Server in dynamic memory if you intend to use them as function parameters or
    pass them around in smart pointers of by reference.
  * **Assume that requests made are independent of each other.** None of the
    HTTP Server implementations support request pipelining (yet) so a single
    connection only deals with a single request.
  * **The Handler instance is invoked asynchronously**. This means the I/O
    thread used to handle network-related events are free to handle only the
    I/O related events. This enables the server to scale better as to the
    number of concurrent connections it can handle.
  * **The Handler is able to schedule asynchronous actions on the thread pool
    associated with the server.** This allows handlers to perform multiple
    asynchronous computations that later on perform writes to the connection.
  * **The Handler is able to control the (asynchronous) writes to and reads
    from the HTTP connection.** Because the connection is available to the
    Handler, that means it can write out chunks of data at a time or stream
    data through the connection continuously.

The Handler concept for the HTTP Server is described by the following table:

---------------

**Legend:**

H
    The Handler type.
h
    An instance of H.
Req
    A type that models the Request Concept.
ConnectionPtr
    A type that models the Connection Pointer Concept.
req
    An instance of Req.
conn
    An instance of ConncetionPtr.

+------------------+-------------+--------------------------------------------+
| Construct        | Return Type | Description                                |
+==================+=============+============================================+
| ``h(req, conn)`` | ``void``    | Handle the request; conn is a shared       |
|                  |             | pointer which exposes functions for        |
|                  |             | writing to and reading from the connection.|
+------------------+-------------+--------------------------------------------+

---------------

The HTTP Server is meant to allow for better scalability in terms of the number
of concurrent connections and for performing asynchronous actions within the
handlers.  The HTTP Server implementation is available from a single
user-facing template named ``server``. This template takes in a single template
parameter which is the type of the Handler to be called once a request has been
parsed from a connection.

An instance of Handler is taken as a reference to the constructor of the server
instance.

.. warning:: The HTTP Server implementation does not perform any
   synchronization on the calls to the Handler invocation. This means if your
   handler contains or maintains internal state, you are responsible for
   implementing your own synchronization on accesses to the internal state of
   the Handler.

The general pattern for using the ``server`` template is shown below:

.. code-block:: c++

    struct handler;
    typedef boost::network::http::server<handler> http_server;

    struct handler {
        void operator()(
            http_server::request const & req,
            http_server::connection_ptr connection
        ) {
            // handle the request here, and use the connection to
            // either read more data or write data out to the client
        }
    };

API Documentation
-----------------

The following sections assume that the following file has been included:

.. code-block:: c++

    #include <boost/network/include/http/server.hpp>
    #include <boost/network/utils/thread_pool.hpp>

And that the following typedef's have been put in place:

.. code-block:: c++

    struct handler_type;
    typedef boost::network::http::server<handler_type> http_server;

    struct handler_type {
        void operator()(http_server::request const & request,
                        http_server::connection_ptr connection) {
            // do something here
        }
    };

Constructor
~~~~~~~~~~~

``explicit http_server(options)``
    Construct an HTTP server instance passing in a ``server_options<Tag,
    Handler>`` instance.

Server Options
~~~~~~~~~~~~~~

.. doxygenstruct:: boost::network::http::server_options
   :project: cppnetlib
   :members:

Public Members
~~~~~~~~~~~~~~

.. doxygenstruct:: boost::network::http::server
   :project: cppnetlib
   :members:
   :undoc-members:

Connection Object
~~~~~~~~~~~~~~~~~

.. doxygenstruct:: boost::network::http::async_connection
   :project: cppnetlib
   :members:

Adding SSL support to the HTTP Server
-------------------------------------

In order to setup SSL support for an Asynchronous Server, it is best to start from
a regular Asynchronous Server (see above). Once this server is setup, SSL can be
enabled by adding a Boost.Asio.Ssl.Context_ to the options. The settings that can be
used are defined in the link.

.. code-block:: c++

    // Initialize SSL context
    std::shared_ptr<asio::ssl::context> ctx =
        std::make_shared<asio::ssl::context>(asio::ssl::context::sslv23);
    ctx->set_options(
                asio::ssl::context::default_workarounds
                | asio::ssl::context::no_sslv3
                | asio::ssl::context::single_dh_use);
    
    // Set keys
    ctx->set_password_callback(password_callback);
    ctx->use_certificate_chain_file("server.pem");
    ctx->use_private_key_file("server.pem", asio::ssl::context::pem);
    ctx->use_tmp_dh_file("dh512.pem");
    
    handler_type handler;
    http_server::options options(handler);
    options.thread_pool(std::make_shared<boost::network::utils::thread_pool>(2));
    http_server server(options.address("127.0.0.1").port("8442").context(ctx));

    std::string password_callback(std::size_t max_length, asio::ssl::context_base::password_purpose purpose) {
        return std::string("test");
    }
    
.. _Boost.Range: http://www.boost.org/libs/range
.. _Boost.Function: http://www.boost.org/libs/function
.. _Boost.Asio.SSL.Context: http://www.boost.org/doc/libs/1_55_0/doc/html/boost_asio/reference/ssl__context.html
#            Copyright (c) Dean Michael Berris 2010.
# Distributed under the Boost Software License, Version 1.0.
#    (See accompanying file LICENSE_1_0.txt or copy at
#          http://www.boost.org/LICENSE_1_0.txt)

include_directories(${CPP-NETLIB_SOURCE_DIR})
include_directories(${CPP-NETLIB_SOURCE_DIR}/deps/cxxopts/src)
if (OPENSSL_FOUND)
  include_directories(${OPENSSL_INCLUDE_DIR})
endif (OPENSSL_FOUND)

add_executable(http_client http_client.cpp)
add_executable(simple_wget simple_wget.cpp)
add_executable(atom_reader atom/atom.cpp atom/main.cpp)
add_executable(rss_reader rss/rss.cpp rss/main.cpp)
add_executable(hello_world_server http/hello_world_server.cpp)
add_executable(hello_world_client http/hello_world_client.cpp)
add_executable(hello_world_async_server_with_work_queue http/hello_world_async_server_with_work_queue.cpp)
add_executable(trivial_google trivial_google.cpp)

if (UNIX)
  add_executable(fileserver http/fileserver.cpp)
endif (UNIX)
add_dependencies(http_client network-uri cppnetlib-client-connections)
add_dependencies(simple_wget network-uri cppnetlib-client-connections)
add_dependencies(atom_reader network-uri cppnetlib-client-connections)
add_dependencies(rss_reader network-uri cppnetlib-client-connections)
add_dependencies(trivial_google network-uri cppnetlib-client-connections)

target_link_libraries(http_client
    ${Boost_LIBRARIES}
    ${CMAKE_THREAD_LIBS_INIT}
    network-uri
    cppnetlib-client-connections)

target_link_libraries(simple_wget
    ${Boost_LIBRARIES}
    ${CMAKE_THREAD_LIBS_INIT}
    network-uri
    cppnetlib-client-connections)

target_link_libraries(atom_reader
    ${Boost_LIBRARIES}
    ${CMAKE_THREAD_LIBS_INIT}
    network-uri
    cppnetlib-client-connections)

target_link_libraries(rss_reader
    ${Boost_LIBRARIES}
    ${CMAKE_THREAD_LIBS_INIT}
    network-uri
    cppnetlib-client-connections)

target_link_libraries(trivial_google
    ${Boost_LIBRARIES}
    ${CMAKE_THREAD_LIBS_INIT}
    network-uri
    cppnetlib-client-connections)

target_link_libraries(hello_world_server
    ${Boost_LIBRARIES}
    ${CMAKE_THREAD_LIBS_INIT}
    cppnetlib-server-parsers)

target_link_libraries(hello_world_client
    ${Boost_LIBRARIES}
    ${CMAKE_THREAD_LIBS_INIT}
    network-uri
    cppnetlib-client-connections)

target_link_libraries(hello_world_async_server_with_work_queue
    ${Boost_LIBRARIES}
    ${CMAKE_THREAD_LIBS_INIT}
    network-uri
    cppnetlib-client-connections
    cppnetlib-server-parsers)

if (OPENSSL_FOUND)
    add_executable(ssl_server http/ssl/ssl_server.cpp)
    add_dependencies(ssl_server network-uri cppnetlib-client-connections)
    target_link_libraries(ssl_server
        ${Boost_LIBRARIES}
        ${CMAKE_THREAD_LIBS_INIT}
        cppnetlib-server-parsers
        network-uri
        cppnetlib-client-connections)
endif (OPENSSL_FOUND)


if (OPENSSL_FOUND)
  target_link_libraries(http_client ${OPENSSL_LIBRARIES})
  target_link_libraries(simple_wget ${OPENSSL_LIBRARIES})
  target_link_libraries(atom_reader ${OPENSSL_LIBRARIES})
  target_link_libraries(rss_reader ${OPENSSL_LIBRARIES})
  target_link_libraries(hello_world_server ${OPENSSL_LIBRARIES})
  target_link_libraries(hello_world_client ${OPENSSL_LIBRARIES})
  target_link_libraries(hello_world_async_server_with_work_queue ${OPENSSL_LIBRARIES})
  target_link_libraries(ssl_server ${OPENSSL_LIBRARIES})
  target_link_libraries(trivial_google ${OPENSSL_LIBRARIES})
endif (OPENSSL_FOUND)

if (${CMAKE_CXX_COMPILER_ID} MATCHES GNU AND ${CMAKE_SYSTEM_NAME} MATCHES "Windows")
  target_link_libraries(http_client ws2_32)
  target_link_libraries(simple_wget ws2_32)
  target_link_libraries(atom_reader ws2_32)
  target_link_libraries(rss_reader ws2_32)
  target_link_libraries(hello_world_server ws2_32 wsock32)
  target_link_libraries(hello_world_client ws2_32)
  target_link_libraries(hello_world_async_server_with_work_queue ws2_32 wsock32)
  target_link_libraries(ssl_server ws2_32 wsock32)
  target_link_libraries(trivial_google ws2_32)
endif()

if (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
  target_link_libraries(http_client rt)
  target_link_libraries(simple_wget rt)
  target_link_libraries(atom_reader rt)
  target_link_libraries(rss_reader rt)
  target_link_libraries(hello_world_server rt)
  target_link_libraries(hello_world_client rt)
  target_link_libraries(hello_world_async_server_with_work_queue rt)
  target_link_libraries(trivial_google rt)
  if (OPENSSL_FOUND)
    target_link_libraries(ssl_server rt)
  endif (OPENSSL_FOUND)
endif()

if (UNIX)
  target_link_libraries(fileserver
    ${Boost_LIBRARIES}
    ${CMAKE_THREAD_LIBS_INIT}
    cppnetlib-server-parsers)
  if (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    target_link_libraries(fileserver rt)
  endif()
  if (OPENSSL_FOUND)
    target_link_libraries(fileserver ${OPENSSL_LIBRARIES})
  endif(OPENSSL_FOUND)
endif (UNIX)

set_target_properties(http_client PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/example)
set_target_properties(simple_wget PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/example)
set_target_properties(atom_reader PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/example)
set_target_properties(rss_reader PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/example)
set_target_properties(trivial_google PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/example)
set_target_properties(hello_world_server PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/example)
set_target_properties(hello_world_client PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/example)
set_target_properties(hello_world_async_server_with_work_queue PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/example)
if (OPENSSL_FOUND)
  set_target_properties(ssl_server PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/example)
endif (OPENSSL_FOUND)

if (UNIX)
  set_target_properties(fileserver PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/example)
endif (UNIX)
Use of this software is granted under one of the following two licenses,
to be chosen freely by the user.

1. Boost Software License - Version 1.0 - August 17th, 2003
===============================================================================

Copyright (c) 2006, 2007 Marcin Kalicinski

Permission is hereby granted, free of charge, to any person or organization
obtaining a copy of the software and accompanying documentation covered by
this license (the "Software") to use, reproduce, display, distribute,
execute, and transmit the Software, and to prepare derivative works of the
Software, and to permit third-parties to whom the Software is furnished to
do so, all subject to the following:

The copyright notices in the Software and this entire statement, including
the above license grant, this restriction and the following disclaimer,
must be included in all copies of the Software, in whole or in part, and
all derivative works of the Software, unless such copies or derivative
works are solely in the form of machine-executable object code generated by
a source language processor.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE, TITLE AND NON-INFRINGEMENT. IN NO EVENT
SHALL THE COPYRIGHT HOLDERS OR ANYONE DISTRIBUTING THE SOFTWARE BE LIABLE
FOR ANY DAMAGES OR OTHER LIABILITY, WHETHER IN CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
DEALINGS IN THE SOFTWARE.

2. The MIT License
===============================================================================

Copyright (c) 2006, 2007 Marcin Kalicinski

Permission is hereby granted, free of charge, to any person obtaining a copy 
of this software and associated documentation files (the "Software"), to deal 
in the Software without restriction, including without limitation the rights 
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies 
of the Software, and to permit persons to whom the Software is furnished to do so, 
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all 
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR 
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, 
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL 
THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER 
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, 
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS 
IN THE SOFTWARE.
# Copyright 2013 Google, Inc.
# Copyright 2010 Dean Michael Berris <dberris@google.com>
# Distributed under the Boost Software License, Version 1.0.
# (See accompanying file LICENSE_1_0.txt or copy at
# http://www.boost.org/LICENSE_1_0.txt)

# Commenting this out until it's ready for prime-time later on.
# include_directories(${CPP-NETLIB_SOURCE_DIR})
# set(CMAKE_BUILD_TYPE Release)
# if (Boost_FOUND)
#   add_executable(cpp-netlib-utils_base64_experiment utils_base64_experiment.cpp)
#   target_link_libraries(cpp-netlib-utils_base64_experiment ${Boost_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT})
#   if (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
#     target_link_libraries(cpp-netlib-utils_base64_experiment rt)
#   endif()
#   set_target_properties(cpp-netlib-utils_base64_experiment
#                         PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/tests)
# endif()
Benchmark results from GCC 4.6.4 without any optimization (no switches):

  Executing base64_stateless_test:
    Encoding 16 MB buffer took 4.81s.
  Executing base64_stateful_buffer_test:
    Encoding 16 MB buffer took 4.93s.
    Encoding 256 x 64 KB buffers took 4.92s.
  Executing base64_stateful_transform_test:
    Encoding 16 MB buffer took 5.32s.
    Encoding 256 x 64 KB buffers took 5.25s.
  Executing base64_stateful_iterator_test:
    Encoding 16 MB buffer took 7.03s.
    Encoding 256 x 64 KB buffers took 7.02s.
  Executing base64_standalone_test:
    Encoding 16 MB buffer took 0.93s.
    Encoding 256 x 64 KB buffers took 1.01s.
  Executing base64_standalone_io_test:
    Encoding 16 MB buffer took 2.31s.
    Encoding 256 x 64 KB buffers took 2.32s.

Benchmark results from GCC 4.6.4 with the -O3 optimization; the processed
data were 10 times bigger than for the test run without any optimization:

  Executing base64_stateless_test:
    Encoding 160 MB buffer took 3.42s.
  Executing base64_stateful_buffer_test:
    Encoding 160 MB buffer took 3.69s.
    Encoding 1280 x 320 KB buffers took 9.43s.
  Executing base64_stateful_transform_test:
    Encoding 160 MB buffer took 4.71s.
    Encoding 1280 x 320 KB buffers took 12.27s.
  Executing base64_stateful_iterator_test:
    Encoding 160 MB buffer took 4.65s.
    Encoding 1280 x 320 KB buffers took 11.92s.
  Executing base64_standalone_test:
    Encoding 160 MB buffer took 1.46s.
    Encoding 1280 x 320 KB buffers took 4.09s.
  Executing base64_standalone_io_test:
    Encoding 160 MB buffer took 3.93s.
    Encoding 1280 x 320 KB buffers took 10.18s.

Testing the base64_stateless was done for the sake of completeness just to
test the pure boost implementation only; state is needed for chunked encoding.

The three different base64_stateful_xxx implementations are comparable;
the base64_stateful_iterator may have spent more time in copy constructors,
because the state is owned lower - by the transformed iterator adaptor.
The iostream interface brings noticeable overhead, especially if the
encoding state (stored in the internal extensible array of the output stream)
is used extensively.

The boost transforming iterators are not enough to implement BASE64 encoding
of a chunked input.  Taking the additional code into consideration, the amount
of code for the non-boost base64_standalone implementation is not so different
and offers better performance.
# Copyright (c) Glyn Matthews 2011.
# Copyright 2011 Dean Michael Berris (dberris@google.com)
# Copyright 2011 Google, Inc.
# Distributed under the Boost Software License, Version 1.0.
#    (See accompanying file LICENSE_1_0.txt or copy at
#          http://www.boost.org/LICENSE_1_0.txt)


include_directories(${CPP-NETLIB_SOURCE_DIR})

file(GLOB_RECURSE CPP-NETLIB_HEADERS
    "${CPP-NETLIB_SOURCE_DIR}/boost/" "*.hpp")

set(CPP-NETLIB_HTTP_SERVER_SRCS server_request_parsers_impl.cpp)
add_library(cppnetlib-server-parsers ${CPP-NETLIB_HTTP_SERVER_SRCS})
set_target_properties(cppnetlib-server-parsers
    PROPERTIES VERSION ${CPPNETLIB_VERSION_STRING}
    SOVERSION ${CPPNETLIB_VERSION_MAJOR}
    PUBLIC_HEADER "${CPP-NETLIB_HEADERS}")
install(TARGETS cppnetlib-server-parsers
    EXPORT cppnetlibTargets
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_FULL_INCLUDEDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_FULL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_FULL_LIBDIR})

set(CPP-NETLIB_HTTP_CLIENT_SRCS client.cpp)
add_library(cppnetlib-client-connections ${CPP-NETLIB_HTTP_CLIENT_SRCS})
set_target_properties(cppnetlib-client-connections
    PROPERTIES VERSION ${CPPNETLIB_VERSION_STRING}
    SOVERSION ${CPPNETLIB_VERSION_MAJOR}
    PUBLIC_HEADER "${CPP-NETLIB_HEADERS}")
target_link_libraries(cppnetlib-client-connections ${Boost_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT})
if (OPENSSL_FOUND)
    target_link_libraries(cppnetlib-client-connections ${OPENSSL_LIBRARIES})
    if (CPP-NETLIB_STATIC_OPENSSL)
      if (NOT MSVC AND NOT MINGW AND NOT ${CMAKE_SYSTEM_NAME} MATCHES "FreeBSD") # dynlinker functions are built into libc on FreeBSD
        target_link_libraries(cppnetlib-client-connections "-ldl")
      endif()
    endif()
endif ()
install(TARGETS cppnetlib-client-connections
    EXPORT cppnetlibTargets
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_FULL_INCLUDEDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_FULL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_FULL_LIBDIR})
# Copyright (c) Dean Michael Berris 2010.
# Copyright 2015 Google, Inc.
# Distributed under the Boost Software License, Version 1.0.
# (See accompanying file LICENSE_1_0.txt or copy at
# http://www.boost.org/LICENSE_1_0.txt)

include_directories(${CPP-NETLIB_SOURCE_DIR} ${gtest_SOURCE_DIR}/include)

# add_subdirectory(uri)
add_subdirectory(http)

if (Boost_FOUND)
    set(TESTS utils_thread_pool
	# utils_base64_test -- turn on when ready.
        )
    foreach (test ${TESTS})
      if (${CMAKE_CXX_COMPILER_ID} MATCHES GNU)
	set_source_files_properties(${test}.cpp
	  PROPERTIES COMPILE_FLAGS "-Wall")
      endif()
      add_executable(cpp-netlib-${test} ${test}.cpp)
      add_dependencies(cpp-netlib-${test} network-uri gtest_main)
      target_link_libraries(cpp-netlib-${test} ${Boost_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT} network-uri gtest_main)
      if (OPENSSL_FOUND)
	target_link_libraries(cpp-netlib-${test} ${OPENSSL_LIBRARIES})
      endif()
      if (${CMAKE_CXX_COMPILER_ID} MATCHES GNU AND ${CMAKE_SYSTEM_NAME} MATCHES "Windows")
	target_link_libraries(cpp-netlib-${test} ws2_32 wsock32)
      endif()
      if (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
	target_link_libraries(cpp-netlib-${test} rt)
      endif()
      set_target_properties(cpp-netlib-${test}
	  PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/tests)
      add_test(cpp-netlib-${test}
	  ${CPP-NETLIB_BINARY_DIR}/tests/cpp-netlib-${test})
    endforeach (test)

    # Also copy the server directory to the root of the build directory.
    file(COPY server DESTINATION ${CPP-NETLIB_BINARY_DIR}/libs/network/test/)
endif()

# Copyright 2010 Dean Michael Berris.
# Distributed under the Boost Software License, Version 1.0.
# (See accompanying file LICENSE_1_0.txt or copy at
# http://www.boost.org/LICENSE_1_0.txt)

include_directories(${CPP-NETLIB_SOURCE_DIR})

if (OPENSSL_FOUND)
    include_directories( ${OPENSSL_INCLUDE_DIR} )
    add_definitions(-DBOOST_NETWORK_ENABLE_HTTPS)
endif()

if (Boost_FOUND)
    add_subdirectory(client)

    set(TESTS response_incremental_parser_test request_incremental_parser_test
      request_linearize_test)
    foreach ( test ${TESTS} )
        add_executable(cpp-netlib-http-${test} ${test}.cpp)
        add_dependencies(cpp-netlib-http-${test} gtest_main
            network-uri)
        target_link_libraries(cpp-netlib-http-${test}
            ${Boost_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT} gtest_main
            network-uri)
	if (${CMAKE_CXX_COMPILER_ID} MATCHES GNU AND ${CMAKE_SYSTEM_NAME} MATCHES "Windows")
          target_link_libraries(cpp-netlib-http-${test} ws2_32)
        endif()
	if (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
	  target_link_libraries(cpp-netlib-http-${test} rt)
	endif()
        set_target_properties(cpp-netlib-http-${test}
            PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/tests)
        add_test(cpp-netlib-http-${test}
            ${CPP-NETLIB_BINARY_DIR}/tests/cpp-netlib-http-${test})
    endforeach (test)
    set(TESTS
      client_constructor_test
      client_get_test
      client_get_different_port_test
      # client_get_timeout_test
      client_get_ready_test
      client_get_streaming_test)
    foreach ( test ${TESTS} )
        add_executable(cpp-netlib-http-${test} ${test}.cpp)
        add_dependencies(cpp-netlib-http-${test} network-uri
	  cppnetlib-client-connections gtest_main)
        target_link_libraries(cpp-netlib-http-${test}
	  ${Boost_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT} network-uri gtest_main cppnetlib-client-connections)
        if (OPENSSL_FOUND)
            target_link_libraries(cpp-netlib-http-${test} ${OPENSSL_LIBRARIES})
        endif()
	if (${CMAKE_CXX_COMPILER_ID} MATCHES GNU AND ${CMAKE_SYSTEM_NAME} MATCHES "Windows")
          target_link_libraries(cpp-netlib-http-${test} ws2_32)
        endif()
	if (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
	  target_link_libraries(cpp-netlib-http-${test} rt)
	endif()
        set_target_properties(cpp-netlib-http-${test}
            PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/tests)
        add_test(cpp-netlib-http-${test}
            ${CPP-NETLIB_BINARY_DIR}/tests/cpp-netlib-http-${test})
    endforeach (test)

    set(SERVER_API_TESTS server_constructor_test
       server_header_parser_test)
    foreach (test ${SERVER_API_TESTS})
        add_executable(cpp-netlib-http-${test} ${test}.cpp)
        add_dependencies(cpp-netlib-http-${test} cppnetlib-server-parsers)
	target_link_libraries(cpp-netlib-http-${test}
	  ${Boost_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT} cppnetlib-server-parsers gtest_main)
        if (OPENSSL_FOUND)
            target_link_libraries(cpp-netlib-http-${test} ${OPENSSL_LIBRARIES})
        endif()
	if (${CMAKE_CXX_COMPILER_ID} MATCHES GNU AND ${CMAKE_SYSTEM_NAME} MATCHES "Windows")
          target_link_libraries(cpp-netlib-http-${test} ws2_32 wsock32)
        endif()
	if (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
	  target_link_libraries(cpp-netlib-http-${test} rt)
	endif()
        set_target_properties(cpp-netlib-http-${test}
            PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/tests)
        add_test(cpp-netlib-http-${test}
            ${CPP-NETLIB_BINARY_DIR}/tests/cpp-netlib-http-${test})
    endforeach (test)

    # Add the server start/stop concurrency test
    add_executable(cpp-netlib-http-server_async_run_stop_concurrency
      server_async_run_stop_concurrency.cpp)
    add_dependencies(cpp-netlib-http-server_async_run_stop_concurrency
      cppnetlib-server-parsers)
    target_link_libraries(cpp-netlib-http-server_async_run_stop_concurrency
      ${Boost_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT} cppnetlib-server-parsers)
    if (OPENSSL_FOUND)
      target_link_libraries(cpp-netlib-http-server_async_run_stop_concurrency
	${OPENSSL_LIBRARIES})
    endif()
    if (${CMAKE_CXX_COMPILER_ID} MATCHES GNU
       	AND ${CMAKE_SYSTEM_NAME} MATCHES "Windows")
      target_link_libraries(cpp-netlib-http-server_async_run_stop_concurrency
	ws2_32 wsock32)
    endif()
    if (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
      target_link_libraries(cpp-netlib-http-server_async_run_stop_concurrency rt)
    endif()
    set_target_properties(cpp-netlib-http-server_async_run_stop_concurrency
      PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/tests)
    add_test(cpp-netlib-http-server_async_run_stop_concurrency
      ${CPP-NETLIB_BINARY_DIR}/tests/cpp-netlib-http-server_async_run_stop_concurrency)
endif()
# Copyright 2016 Glyn Matthews.
# Distributed under the Boost Software License, Version 1.0.
# (See accompanying file LICENSE_1_0.txt or copy at
# http://www.boost.org/LICENSE_1_0.txt)


set(
  TESTS
  request_test
  response_test
  )

foreach(test ${TESTS})
  set(test_name cpp-netlib-http-client-${test})

  add_executable(${test_name} ${test}.cpp)
  add_dependencies(${test_name} network-uri gtest_main)
  target_link_libraries(${test_name}
    ${CMAKE_THREAD_LIBS_INIT} ${Boost_LIBRARIES} network-uri gtest_main)
  set_target_properties(${test_name}
    PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CPP-NETLIB_BINARY_DIR}/tests)
  add_test(${test_name}
    ${CPP-NETLIB_BINARY_DIR}/tests/${test_name})

  if (OPENSSL_FOUND)
    target_link_libraries(${test_name} ${OPENSSL_LIBRARIES})
  endif()

endforeach(test)
