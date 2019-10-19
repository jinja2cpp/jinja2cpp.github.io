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
- Linux gcc 5.0 - 9
- Linux clang 5.0 - 8
- MacOS X-Code 9 - 11
- Microsoft Visual Studio 2015-2019 x86, x64

## Dependencies
Jinja2C++ has several external dependencies:
-  `boost` library (at least version 1.65) 
-  `nonstd::expected-lite` [https://github.com/martinmoene/expected-lite](https://github.com/martinmoene/expected-lite)
-  `nonstd::variant-lite` [https://github.com/martinmoene/variant-lite](https://github.com/martinmoene/variant-lite)
-  `nonstd::optional-lite` [https://github.com/martinmoene/optional-lite](https://github.com/martinmoene/optional-lite)
-  `nonstd::string-view-lite` [https://github.com/martinmoene/string-view-lite](https://github.com/martinmoene/string-view-lite)
-  `fmtlib::fmt` [https://github.com/fmtlib/fmt](https://github.com/fmtlib/fmt)
For testing purposes:
-  `rapidjson` [https://github.com/Tencent/rapidjson](https://github.com/Tencent/rapidjson)
-  `nlohmannjson` [https://github.com/nlohmann/json](https://github.com/nlohmann/json)

## Build and install

### The simplest case
In simplest case, if you don't want to understand Jinja2C++ build script internals, you can follow these easy steps. Jinja2C++ library is shipped with all dependencies as a submodules and can use them. So, you have to:

1. Install CMake build system (at least version 3.5)
2. Clone jinja2cpp repository and update submodules:
```
> git clone https://github.com/jinja2cpp/Jinja2Cpp.git
> cd Jinja2Cpp
> git submodule -q update --init
```
3. Create build directory:
```
> mkdir .build
```
4. Run CMake and build the library:
```
> cd .build
> cmake .. -DCMAKE_INSTALL_PREFIX=<path to install folder> -DJINJA2_DEPS_MODE=internal
> cmake --build . --target install
```
"Path to install folder" here is a path to the folder where you want to install Jinja2Cpp lib. `JINJA2_DEPS_MODE` define with `internal` value creates the build script which will take external dependencies from the submodules.
5. Build library:
```
> cmake --build . 
```
6. Install library (if necessary):
```
> cmake --build . 
```

### Use with conan.io dependency manager
Jinja2C++ can be used as conan.io package. In this case you should do the following steps:

1. Install conan.io according to the documentation ( https://docs.conan.io/en/latest/installation.html )
2. Register the following remote conan.io repositories:
    - https://api.bintray.com/conan/martinmoene/nonstd-lite
    - https://api.bintray.com/conan/bincrafters/public-conan
    - https://api.bintray.com/conan/flexferrum/conan-packages
    
    The sample command is: `conan remote add martin https://api.bintray.com/conan/martinmoene/nonstd-lite`    
3. Add reference to Jinja2C++ package (`jinja2cpp/0.9.1@Manu343726/testing`) to your conanfile.txt, conanfile.py or CMakeLists.txt. For instance, with usage of `conan-cmake` integration it could be written this way:

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

### Dependency management

Different projects require follow different ways for dependencies management. In some cases it's enough to build Jinja2C++ with the internal dependencies only. In other cases it could be necessary that Jinja2C++ use the externally-provided libraries (for instance, boost). To handle this cases Jinja2C++ supports several external dependencies management modes. This modes control via `JINJA2CPP_DEPS_MODE` variable.

#### 'internal' mode

In this mode Jinja2C++ will take all necessary dependencies (both for library build and tests build) from the submodules. This mode suitable when your project has no other dependencies or these dependencies aren't shared with Jinja2C++ deps. `cmake` invocation for this mode is quite simple:
```
> cmake <path_to_jinja2cpp_root> -DCMAKE_BUILD_TYPE=Release -DJINJA2CPP_DEPS_MODE=internal
```

This mode is default for the upstream (`master`) branch. But for releases branch you need to specify this mode manually.

Sample projects for this mode can be found here: [https://github.com/jinja2cpp/examples-build/tree/master/subproject/internal](https://github.com/jinja2cpp/examples-build/tree/master/subproject/internal) and here: [https://github.com/jinja2cpp/examples-build/tree/master/external/internal](https://github.com/jinja2cpp/examples-build/tree/master/external/internal).

#### 'external-boost' mode

The `boost` library is wildly used (except of other Jinja2C++ dependencies), so it's possible to build Jinja2C++ with only `boost` provided as an external dependencies. In this case Jinja2C++ will take `boost` from the outside of the project tree, but all other dependencies will be taken from the submodules. Jinja2C++ build system tries to find boost with the standard `find_package` approach, so, it's necessary for this mode that path to the `boost` is provided with the standard ways (such as `BOOST_ROOT` environment variable). `cmake` invocation for this mode is also quite simple:
```
> cmake <path_to_jinja2cpp_root> -DCMAKE_BUILD_TYPE=Release -DJINJA2CPP_DEPS_MODE=external-boost
```

Sample projects for this mode can be found here: [https://github.com/jinja2cpp/examples-build/tree/master/subproject/external_boost](https://github.com/jinja2cpp/examples-build/tree/master/subproject/external_boost) and here: [https://github.com/jinja2cpp/examples-build/tree/master/external/external_boost](https://github.com/jinja2cpp/examples-build/tree/master/external/external_boost).

#### 'external'

In this mode all Jinja2C++ build system tries to find all necessary dependencies outside the project tree. Path to the projects should be provided via `CMAKE_PREFIX_PATH` variable. This mode is suitable when you want to handle all external libs for your project manually and separately. `cmake` invocation for this mode is also quite simple:
```
cmake <path_to_jinja2cpp_root> -DCMAKE_BUILD_TYPE=Release -DJINJA2CPP_BUILD_TESTS=OFF -DJINJA2CPP_DEPS_MODE=external -DCMAKE_PREFIX_PATH="thirdparty/expected-lite;thirdparty/variant-lite;thirdparty/optional-lite;thirdparty/string-view-lite;thirdparty/fmt
```
This mode is default for the releases branches in order to make archives with Jinja2C++ sources compilable by default.

Sample projects for this mode can be found here: [https://github.com/jinja2cpp/examples-build/tree/master/subproject/external](https://github.com/jinja2cpp/examples-build/tree/master/subproject/external) and here: [https://github.com/jinja2cpp/examples-build/tree/master/external/external](https://github.com/jinja2cpp/examples-build/tree/master/external/external).

### Additional CMake build flags
You can define (via -D command line CMake option) the following build flags:

-  **JINJA2CPP_BUILD_TESTS** (default TRUE) - to build or not to Jinja2C++ tests.
-  **JINJA2CPP_STRICT_WARNINGS** (default TRUE) - Enable strict mode compile-warnings(-Wall -Werror and etc).
-  **MSVC_RUNTIME_TYPE** (default /MD) - MSVC runtime type to link with (if you use Microsoft Visual Studio compiler).

## Link with you projects
Jinja2C++ is a CMake project and follow the standard ways of the CMake project `find` script implementation. So, you can either include Jinja2C++ as a subproject of your project. In this case you should link against `jinja2cpp` target. All necessary settings are already associated with this target. For instance:
```cmake
cmake_minimum_required (VERSION 3.0.0 FATAL_ERROR)
project (Jinja2CppBuildTest CXX)

set (TARGET_NAME jinja2cpp_build_test)

set (JINJA2CPP_DEPS_MODE internal CACHE STRING "" FORCE)

add_subdirectory (${JINJA2CPP_DIR} ${CMAKE_CURRENT_BINARY_DIR}/thirdparty/jinja2cpp)

add_executable (${TARGET_NAME} main.cpp)

target_link_libraries (${TARGET_NAME} jinja2cpp)
set_target_properties (${TARGET_NAME} PROPERTIES
            CXX_STANDARD 14
            CXX_STANDARD_REQUIRED ON)
```

Sample project for this build type you can find here: [https://github.com/jinja2cpp/examples-build/tree/master/subproject/internal](https://github.com/jinja2cpp/examples-build/tree/master/subproject/internal)

Or you can build Jinja2C++ library separately, install it and the find it via `find_package` cmake function. In this case:
1. You should build Jinja2C++ with `CMAKE_INSTALL_PREFIX` variable defined and then install it:
```shell script
cmake thirdparty/Jinja2Cpp -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=../.jinja2cpp-install -DJINJA2CPP_BUILD_TESTS=OFF
cmake --build . --target install
```
2. You should provide path to the Jinja2C++ library directory to the `cmake` invocation of your project:
```shell script
cmake .. -DCMAKE_BUILD_TYPE=Release -Djinja2cpp_DIR=../.jinja2cpp-install/lib/jinja2cpp
```
3. In the CMake script of your project you should find Jinja2C++ with the `find_package` invocation:
```cmake
cmake_minimum_required (VERSION 3.0.0 FATAL_ERROR)
project (Jinja2CppBuildTest CXX)
                
set (TARGET_NAME jinja2cpp_build_test)
set (CMAKE_PREFIX_PATH ${CMAKE_PREFIX_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/.jinja2cpp-install)

find_package(jinja2cpp REQUIRED)

add_executable (${TARGET_NAME} main.cpp)

target_link_libraries (${TARGET_NAME} jinja2cpp)
set_target_properties (${TARGET_NAME} PROPERTIES
            CXX_STANDARD 14
            CXX_STANDARD_REQUIRED ON)
```


## Build with C++17 standard enabled
In case of C++17 standard enabled for your project you should define `variant_CONFIG_SELECT_VARIANT=variant_VARIANT_NONSTD` macro in the build settings.

