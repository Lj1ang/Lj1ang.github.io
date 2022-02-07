---
title: "cmake"
date: 2022-02-06T22:57:02+08:00
slug: ""
description: ""
keywords: []
draft: false
tags: []
math: false
toc: ture
---

# CH1

## 1.1

```cmake
    cmake_minimum_required(VERSION 3.5 FATAL_ERROR)
    project(recipe-01 LANGUAGES CXX)
    add_executable(hello-world hello-world.cpp)
```

- The second line declares the name of the project (recipe-01) and thesupported language ( CXX stands for C++)
- to create a new target: the executable hello-world
- Save the file in the same directory as the source file hello-world.cpp .
- Remember that it can only be named CMakeLists.txt .

--------------------------------

CLI

```CLI
$ mkdir -p build
$ cd build
$ cmake ..
$ cmake --build .
```

&ensp; or

```CKI
$ cmake -H. -Bbuild
```

---------------------------------------

CMake does not enforce a specific name or a
specific location for the build directory.

```CLI
$mkdir -p /tmp/someplace
$cd /tmp/someplace
$cmake /path/to/source
$cmake --build .
```

```CLI
$ cmake --build . --target help
```

reveals that CMake generates more targets than those strictly needed for building
the executable itself.

```CLI
$ cmake --help
```

At the bottom, you will find the list of available generators.

## 1.2 Switch generators for the same project

http://www.aosabook.org/en/posa/ninja.html

```CLI
$ mkdir -p build
$ cd build
$ cmake -G Ninja ..
```

```CLI
$ cmake --build .
```

&ensp; build.ninja and rules.ninja : Contain all the build statements and build rules
for Ninja.(build 构建)

&ensp;cmake_install.cmake : CMake script handling install rules and which is used at
install time.(install 安装)

## 1.3 Building and linking static and shared libraries

Add two lines as follow:

```cmake
add_library(message
            STATIC
            Message.hpp
            Message.cpp
    )
target_link_libraries(hello-world message)
```

run the same command in CLI as before  

-----------------------------

**How it works?**  

```add_library(message STATIC Message.hpp Message.cpp)```

- compiling the specified sources into a library
- The first argument to add_library is the name of the target.The same
  name can be used throughout CMakeLists.txt to refer to the library.
- The library extension is determined based on the second argument, STATIC or SHARED , and the operating system.  

------------------------

**Second Arguements**    

- `STATIC`Archives of object files 
  for use when linking other targets
- `SHARED`libraries that can be
  linked dynamically and loaded at runtime. DSO(dynamic shared object)
- `OBJECT` neithor archiving intto static lib nor being shared 
- `MODULE` DSOs(DOS组)  

>- `IMPORTED`
>- `INTERFACE`
>- `ALIAS` 

-------------------------


```target_link_libraries(hello-world message)```not linked to any other target within the project, but may be loaded dynamically later on

- Links the library into the executable.
- **We thus ensure that the message library is
  always built before we attempt to link it to the hello-world executable.**
  The build dir will contain the `libmessage.a` static library

-----------------

**Obtain static library and shared library**

```cmake
cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

project(recipe-03 LANGUAGES CXX)

add_library(message-objs
    OBJECT
        Message.hpp
        Message.cpp
    )

# this is only needed for older compilers
# but doesn't hurt either to have it
set_target_properties(message-objs
    PROPERTIES
        POSITION_INDEPENDENT_CODE 1
    )

add_library(message-shared
    SHARED
        $<TARGET_OBJECTS:message-objs>
    )

add_library(message-static
    STATIC
        $<TARGET_OBJECTS:message-objs>
    )

add_executable(hello-world hello-world.cpp)

target_link_libraries(hello-world message-static)
```

Generate the two libraries with the same name `message` instead of 
`message-static` and `message-shared`

```cmake
add_library(message-shared
SHARED
$<TARGET_OBJECTS:message-objs>
)
set_target_properties(message-shared
PROPERTIES
OUTPUT_NAME "message"
)
add_library(message-static
STATIC
$<TARGET_OBJECTS:message-objs>
)
set_target_properties(message-static
PROPERTIES
OUTPUT_NAME "message"
)
```

Controlling compilation with conditionals

How to do it
