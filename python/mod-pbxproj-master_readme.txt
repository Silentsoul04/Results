# Contributing

Do you want to fix an issue yourself? Great! some house rules:

1. Provide a description of what problem you are solving, what case was not being taking into account
2. Provide unit tests for the case you have fixed. Pull request without unit test or PRs that decrease the coverage will not be approved until this changes.
3. Adhere to the coding style and conventions of the project, for instance, target_name is used to specify the target across all functions that use this parameter. Changes will be requested on PRs that don't follow this.
4. Write descriptive commit messages.
MIT License

Copyright (c) 2016 Ignacio Calderon aka kronenthaler

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
SOFTWARE.[![Build Status](https://travis-ci.org/kronenthaler/mod-pbxproj.svg?branch=master)](https://travis-ci.org/kronenthaler/mod-pbxproj) 
[![Coverage Status](https://coveralls.io/repos/github/kronenthaler/mod-pbxproj/badge.svg?branch=master&x=1)](https://coveralls.io/github/kronenthaler/mod-pbxproj?branch=master) 
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/70c14211ba704d2893f7b0f54bb04da7)](https://www.codacy.com/app/kronenthaler/mod-pbxproj?utm_source=github.com&utm_medium=referral&utm_content=kronenthaler/mod-pbxproj&utm_campaign=badger)
[![PyPI](https://img.shields.io/pypi/v/pbxproj.svg)](https://pypi.python.org/pypi/pbxproj)
[![License](https://img.shields.io/badge/license-MIT-blue.svg?x=1)](license.txt)
 
# pbxproj 

This module can read, modify, and write a .pbxproj file from an Xcode 4+ projects. The file is usually called project.pbxproj and can be found inside the .xcodeproj bundle. Because some task cannot be done by clicking on an UI or opening Xcode to do it for you, this python module lets you automate the modification process.

## How to use it
The typical tasks with an Xcode project are adding files to the project and setting some standard compilation flags.
It can be achieved with a simple snippet like this:

```python
from pbxproj import XcodeProject
# open the project
project = XcodeProject.load('myapp.xcodeproj/project.pbxproj')

# add a file to it, force=false to not add it if it's already in the project
project.add_file('MyClass.swift', force=False)

# set a Other Linker Flags
project.add_other_ldflags('-ObjC')

# save the project, otherwise your changes won't be picked up by Xcode
project.save()
```

That's it. More details about available API's visit the [wiki](https://github.com/kronenthaler/mod-pbxproj/wiki/).

## Why refactor?
The project has being rewritten entirely from version 1.3.1 to 2.0.0. This refactor had some goals in mind:

1. Make the project more maintainable. By breaking the monolithic file into separated packages and classes.
2. Add unit tests. The old implementation was not particularly testable. Tests will allow to make future changes with confidence that they won't break existing functionality.
3. Improve the code quality. The code has being cleaned, responsibilities clearly separated and ambiguous APIs removed.
4. Introduce new functionality in a clearer way. There were some functionality missing or half working. Some of this features were addresses by this refactor.
5. Make the output as compatible as possible with Xcode's expectations. 
6. Improve the fault tolerance. Whenever Xcode introduces new sections into its format things would've broken. Now, unknown sections are read and written back even if the project doesn't know about them.

For more information about what API's were deprecated or completely removed check [wiki](https://github.com/kronenthaler/mod-pbxproj/wiki/Deprecations).

## Installation
For installation instructions visit the [wiki](https://github.com/kronenthaler/mod-pbxproj/wiki/Installation)

## CLI
For instructions and commands available visit the [wiki](https://github.com/kronenthaler/mod-pbxproj/wiki/CLI)

## Documentation
For general documentation, visit the [wiki](https://github.com/kronenthaler/mod-pbxproj/wiki/).
For technical documentation, the public functions are documented and contains details about what is expected.

## Reporting bugs
Did you find a bug? Too bad, but we want to help you, we need you to:

* Provide as many details about the error you are having.
* If possible provide a sample project.pbxproj to reproduce the steps 
* If possible, try the sequence of steps on Xcode and provide the project.pbxproj generated by Xcode.

We cannot help you if your issue is a title: "it does not work". Or if there is no sequence of steps to reproduce the error. Those kind of issues will be ignored or closed automatically.

## Contributing
Do you want to fix an issue yourself? Great! some house rules:

* Provide a description of what problem you are solving, what case was not being taking into account
* Provide unit tests for the case you have fixed. Pull request without unit test or PRs that decrease the coverage will not be approved until this changes.
* Adhere to the coding style and conventions of the project, for instance, target_name is used to specify the target across all functions that use this parameter. Changes will be requested on PRs that don't follow this.
* Write descriptive commit messages.

## License
This project is licensed using MIT license.
