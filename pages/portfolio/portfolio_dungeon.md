---
title: "Dungeon: Lost Cognition"
keywords: 
tags: 
toc: true
sidebar: portfolio_sidebar
permalink: portfolio_dungeon.html
summary: 
last_updated: August 17, 2020
---

## Introduction

### Technical Showreel

<iframe width="560" height="315" src="https://www.youtube.com/embed/yieawWJ31pw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### About the Project

Photon-v2 is a physically based render engine. The engine tries to generate photorealistic images by leveraging contemporary ray tracing techniques and sticks to physical formulae as close as possible. Its core is written in modern C++ (C++17) and provides a C API for easy integration. The renderer also comes with a Java based studio program for managing render tasks, and a CLI program for server usages. With a custom scene description language, it is possible to automatically generate APIs for scene management in many languages (currently supports Java and Python; markdown for documentation). Notably, the renderer's integration with Blender includes shader nodes, scene exporting and rendering, making the creation and adjustments of complex scenes possible. Photon currently supports Windows, Linux and macOS.

## More on the Project

* The project has been thoroughly documented in its [dedicated website](photon_v2_what_is_photon.html).
* This is an open-source project. Full [source code](https://github.com/TzuChieh/Photon-v2) available.

## History

Initially, it was a side project where I experiment with some global illumination techniques for my game engine (called Tokzin), and both of them were written in Java. It had occurred to me that Java, although easy to code and sometimes outperforms compiled (to machine code) languages thanks to its JIT system, the restricted accessibilities to system memory makes it hard to implement some of the low level optimizations. In 2016, I decided to rewrite the rendering engine in C++ for better performance, and ported most of the code from the original Java codebase. It is worth noting that the C++ version was more than 20% faster rendering the Crytek Sponza scene than its Java counterpart out of the box. At that time, I bumped Photon’s version number into 2.0.
