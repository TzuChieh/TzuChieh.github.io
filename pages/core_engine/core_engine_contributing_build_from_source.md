---
title: Build from Source
keywords: 
last_updated: January 20, 2019
summary: 
sidebar: core_engine_sidebar
permalink: core_engine_contributing_build_from_source.html
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