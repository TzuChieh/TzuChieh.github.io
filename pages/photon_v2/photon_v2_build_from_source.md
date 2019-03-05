---
title: Build from Source
keywords: 
last_updated: January 20, 2019
summary: 
sidebar: photon_v2_sidebar
permalink: photon_v2_build_from_source.html
---

## Prerequisites

Photon uses CMake as its main build system, and the toolkits you need are as follows:

* CMake 3.5.2+ (recommended)
* Python 3 (recommended)
* C++17 compliant compiler (necessary)

If you want to build editor, you will also need:

* JDK 1.8+ and Maven

*Note that the working directory is assumed to be the project root (in the folder that you cloned) if not stated , and please use `./build/` as build folder for now since build scripts are more or less hard-coded to use this path, currently.*

## Step 1: Run the Setup Script
Run the setup script (depending on your system, choose either `./setup.bat` or `./setup.sh`), this will download pre-compiled libraries and resources into "./build".

## Step 2: Compile

For Windows, just use CMake-GUI to generate project files for your favorite IDE.

For Linux and macOS, run the following commands:

* `cd ./build/`
* `cmake -DCMAKE_BUILD_TYPE=release ../`
* `make`

## Step 3: Have Fun

The compiled binaries will be in the `./build/bin/` folder.

## Appendix A: Available CMake Options

Several options are available for fine-tuning the built binaries. To specify a CMake option named `SOME_OPTION` with value `SOME_VALUE`, you should add it as an additional argument in the form

```shell
cmake -DSOME_OPTION=SOME_VALUE (other arguments...)
```

and substitute `SOME_OPTION` and `SOME_VALUE` with the options listed below.

*(do not forget the -D prefix)*

| Options          | Values        | Effects  |
| -------------    | ------------- | ----- |
| CMAKE_BUILD_TYPE | release | When set, build binaries with optimizations enabled; otherwise no optimization is done. |
| BUILD_ENGINE_TEST | ON (default: OFF)     | Build unit tests. They should be executed from the build folder. |
| BUILD_EDITOR_JNI | ON (default: OFF)     | Build JNI for Photon Studio. |

You can also obtain a complete list of options with descriptions by running `cmake -LAH` in the project root.