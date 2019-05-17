---
layout: default
title: Build and Install
nav_order: 4
---

# Build and install
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Supported compilers
Compilation of Jinja2C++ tested on the following compilers (with C++14 enabled feature):
- Linux gcc 5.0
- Linux gcc 6.0
- Linux gcc 7.0
- Linux clang 5.0
- Microsoft Visual Studio 2015 x86, x64
- Microsoft Visual Studio 2017 x86, x64

## Dependencies
Jinja2C++ has several external dependencies:
-  `boost` library (at least version 1.55) 
-  `nonstd::expected-lite` [https://github.com/martinmoene/expected-lite](https://github.com/martinmoene/expected-lite)
-  `nonstd::variant-lite` [https://github.com/martinmoene/variant-lite](https://github.com/martinmoene/variant-lite)
-  `nonstd::value-ptr-lite` [https://github.com/martinmoene/value-ptr-lite](https://github.com/martinmoene/value-ptr-lite)
-  `nonstd::optional-lite` [https://github.com/martinmoene/optional-lite](https://github.com/martinmoene/optional-lite)

## Build and install
In order to compile Jinja2C++ you need:

1. Install CMake build system (at least version 3.0)
2. Clone jinja2cpp repository and update submodules:
```
> git clone https://github.com/flexferrum/Jinja2Cpp.git
> git submodule -q update --init
```
3. Create build directory:
```
> cd Jinja2Cpp
> mkdir build
```
4. Run CMake and build the library:
```
> cd build
> cmake .. -DCMAKE_INSTALL_PREFIX=<path to install folder>
> cmake --build . --target all
```
"Path to install folder" here is a path to the folder where you want to install Jinja2Cpp lib.
5. Install library:
```
> cmake --build . --target install
```
6. Also you can run the tests:
```
> ctest -C Release
```

### Use with conan.io dependency manager
Jinja2Cpp can be used as conan.io package. In this case you should do the following steps:

1. Install conan.io according to the documentation ( https://docs.conan.io/en/latest/installation.html )
2. Register the following remote conan.io repositories:
    - https://api.bintray.com/conan/martinmoene/nonstd-lite
    - https://api.bintray.com/conan/bincrafters/public-conan
    - https://api.bintray.com/conan/manu343726/conan-packages
    
    The sample command is: `conan remote add martin https://api.bintray.com/conan/martinmoene/nonstd-lite`    
3. Add reference to Jinja2Cpp package (`jinja2cpp/0.9.1@Manu343726/testing`) to your conanfile.txt, conanfile.py or CMakeLists.txt. For instance, with usage of `conan-cmake` integration it could be written this way:

```cmake
include (../../cmake/conan.cmake)
if (NOT MSVC)
    set (CONAN_SETTINGS SETTINGS compiler.libcxx=libstdc++11)
endif ()

conan_cmake_run(REQUIRES 
                    jinja2cpp/0.9.1@Manu343726/testing
                    gtest/1.7.0@bincrafters/stable
                BASIC_SETUP
                ${CONAN_SETTINGS}
                OPTIONS 
                    jinja2cpp:shared=False
                    gtest:shared=False
                BUILD missing)
                
set (TARGET_NAME jinja2cpp_build_test)

add_executable (${TARGET_NAME} main.cpp)

target_link_libraries (${TARGET_NAME} ${CONAN_LIBS})
set_target_properties (${TARGET_NAME} PROPERTIES
            CXX_STANDARD 14
            CXX_STANDARD_REQUIRED ON)

```

### Additional CMake build flags
You can define (via -D command line CMake option) the following build flags:

-  **JINJA2CPP_BUILD_TESTS** (default TRUE) - to build or not to Jinja2Cpp tests.
-  **JINJA2CPP_STRICT_WARNINGS** (default TRUE) - Enable strict mode compile-warnings(-Wall -Werror and etc).
-  **JINJA2CPP_BUILD_SHARED** (default OFF) - Specify Jinja2Cpp library library link type.
-  **MSVC_RUNTIME_TYPE** (default /MD) - MSVC runtime type to link with (if you use Microsoft Visual Studio compiler).
-  **JINJA2CPP_DEPS_MODE** (default "internal") - modes for dependencies handling. Following values possible:
    -  `internal` In this mode Jinja2Cpp build script uses dependencies (include `boost`) shipped as subprojects. Nothing needs to be provided externally.
    -  `external-boost` In this mode Jinja2Cpp build script uses only `boost` as externally-provided dependency. All other dependencies taken from subprojects.
    -  `external` In this mode all dependencies should be provided externally. Paths to `boost`, `nonstd-*` libs etc. should be specified via standard CMake variables (like `CMAKE_PREFIX_PATH` or libname_DIR)
    -  `conan-build` Special mode for building Jinja2Cpp via conan recipe.
    
## Dependency management modes
TODO:

## Link with you projects
Jinja2Cpp is shipped with cmake finder script. So you can:

1. Include Jinja2Cpp cmake scripts to the project:
```cmake
list (APPEND CMAKE_MODULE_PATH ${JINJA2CPP_INSTALL_DIR}/cmake)
```
2. Use regular 'find' script:
```cmake
find_package(jinja2cpp)
```
3. Add found paths to the project settings:
```cmake
#...
include_directories(
    #...
    ${JINJA2CPP_INCLUDE_DIR}
    )

target_link_libraries(YourTarget
    #...
    ${JINJA2CPP_LIBRARY}
    )
#...
```
or just link with Jinja2Cpp target:
```cmake
#...
target_link_libraries(YourTarget
    #...
    Jinja2Cpp
    )
#...
```

## Build with C++17 standard enabled
In case of C++17 standard enabled for your project you should define `variant_CONFIG_SELECT_VARIANT=variant_VARIANT_NONSTD` macro in the build settings.

