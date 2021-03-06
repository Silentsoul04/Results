cmake_minimum_required(VERSION 3.1)
project(FlexibleReflection)
set(CMAKE_CXX_STANDARD 11)
add_executable(FlexibleReflection Main.cpp Primitives.cpp Reflect.h)
MIT License

Copyright (c) 2018 Jeff Preshing

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
This project presents a small, flexible runtime reflection system using C++11 language features.

For more information, see the blog series ["A Flexible Reflection System in C++"](http://preshing.com/20180116/a-primitive-reflection-system-in-cpp-part-1).

## Build Instructions

[CMake](https://cmake.org/) is required. Quick start:

    $ git clone https://github.com/preshing/FlexibleReflection
    $ cd FlexibleReflection
    $ mkdir build
    $ cd build
    $ cmake ..

For detailed build instructions, see ["How to Build a CMake-Based Project"](http://preshing.com/20170511/how-to-build-a-cmake-based-project).
