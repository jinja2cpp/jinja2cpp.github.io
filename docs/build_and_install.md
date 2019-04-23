---
layout: default
title: Build and Install
nav_order: 4
---


# Supported compilers
Compilation of Jinja2Cpp tested on the following compilers (with C++14 enabled feature):
- Linux gcc 5.0
- Linux gcc 6.0
- Linux gcc 7.0
- Linux clang 5.0
- Microsoft Visual Studio 2015 x86, x64
- Microsoft Visual Studio 2017 x86, x64

# Build and install
Jinja2Cpp has five external dependencies: boost library (at least version 1.55) and several header-only dependecies from nonstd project(expected-lite, variant-lite, value-ptr-lite, optional-lite). Because of types from boost are used inside library, you should compile both your projects and Jinja2Cpp library with similar compiler settings. Otherwise ABI could be broken.

In order to compile Jinja2Cpp you need:

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

## Additional CMake build flags
You can define (via -D command line CMake option) the following build flags:

* **JINJA2CPP_BUILD_TESTS** (default TRUE) - to build or not to Jinja2Cpp tests.
* **JINJA2CPP_STRICT_WARNINGS** (default TRUE) - Enable strict mode compile-warnings(-Wall -Werror and etc).
* **JINJA2CPP_BUILD_SHARED** (default OFF) - Specify Jinja2Cpp library library link type.
* **MSVC_RUNTIME_TYPE** (default /MD) - MSVC runtime type to link with (if you use Microsoft Visual Studio compiler).
* **BOOST_ROOT** - Path to the prebuilt boost installation

# Link with you projects
Jinja2Cpp is shipped with cmake finder script. So you can:

1. Include Jinja2Cpp cmake scripts to the project:
```cmake
list (APPEND CMAKE_MODULE_PATH ${JINJA2CPP_INSTALL_DIR}/cmake)
```

2. Use regular 'find' script:
```cmake
find_package(Jinja2Cpp)
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
4. Build with C++17 standard enabled
In case of C++17 standard enabled for your project you should define `variant_CONFIG_SELECT_VARIANT=variant_VARIANT_NONSTD` macro in the build settings.

