---
title: "Photon-v2 Renderer"
keywords: 
tags: 
toc: true
sidebar: portfolio_sidebar
permalink: portfolio_photon_v2.html
summary: 
last_updated: August 16, 2020
---

## Technical Showreel

<iframe width="560" height="315" src="https://www.youtube.com/embed/yieawWJ31pw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## About the Project

Photon-v2 is a physically based render engine. The engine tries to generate photorealistic images by leveraging contemporary ray tracing techniques and sticks to physical formulae as close as possible. Its core is written in modern C++ (C++17) and provides a C API for easy integration. The renderer also comes with a Java based studio program for managing render tasks, and a CLI program for server usages. With a custom scene description language, it is possible to automatically generate APIs for scene management in many languages (currently supports Java and Python; markdown for documentation). Notably, the renderer's integration with Blender includes shader nodes, scene exporting and rendering, making the creation and adjustments of complex scenes possible. Photon currently supports Windows, Linux and macOS.

## List of Main Features

* **Rendering**
  * **Backward Unidirectional Path Tracing**
  * **Backward Unidirectional Path Tracing with Next Event Estimation**
  * **Photon Mapping**
  * **Progressive Photon Mapping**
  * **Stochastic Progressive Photon Mapping**
  * **RGB and Spectral Rendering**
  * **AOV Rendering (normal, sample time, sample count)**
  * **Sample Generation**  
    Supports random, stratified, and Halton
  * **Image Rendering**
    * Bulk, Tile, Grid and Spiral Modes
    * Adaptive Sampling

* **Imaging and Film**
  * **Cameras**  
    Supports pinhole, thin Lens, 360 cameras.
  * **Radiant Flux Sensor**
  * **Film Filtering**
    * box, Gaussian, Mitchell-Netravali, Blackman-Harris
  * **Tone-mapping**
    * naive Reinhard
    * Jim Hejl and Richard Burgess-Dawson mapping
  * **Various IO Formats**
    * LDR: .png, .jpg, .bmp, .tga
    * HDR: .hdr, .exr, .pfm

* **Material**
  * **Lambertian Diffuse**
  * **Microfacet-based Opaque Model**
    * isotropic-GGX distribution
    * anisotropic-GGX distribution
  * **Microfacet-based Translucent Model**
    * isotropic-GGX distribution
  * **Idealized Surface**
    * absorber, reflector, transmitter
    * dielectric with controllable reflectance and transmittance
  * **Spectral Complex IoR**
  * **Layered Surface Material (Belcour's model)**
  * **Blending Arbitrary BSDFs**
  * **Schlick and Exact Fresnel Models**

* **Geometry**
  * **Triangle, Rectangle, Sphere, Cuboid, Triangle Mesh**
  * **Simple 2-D Wave, Fractal**
  * **Instancing**
  * **Acceleration Structures**
    * BVH
    * kD-tree (point, indexed, referenced)
  * **Linear Motions**

* **Light**
  * **Point Light, Area Light (sphere, rectangle)**
  * **Geometric Light**
  * **HDR Environment Map**
    * with importance sampling
  * **IES Light Profiles**
  * **Preetham Sky Model**

* **Texture**
  * **Nearest and Bilinear Filtering**
  * **Procedural Generators**
    * constants and checkerboard
  * **Procedural Operators**
    * mathematical modifiers: add, multiply

* **Misc.**
  * **Blender Addon for Scene Creation**
  * **Easy-to-write Custom Scene Description Language**
  * **Studio Program for Rendering and Scene Management**
  * **CLI for Server Usage**
  * **Loading and Rendering Minecraft Maps (experimental)**
  * **Hierarchical Scene Graph**
  * **Automatically Generate SDL Interface (currently supports Python, Java)**

## Rendered Images

{% include image_gallery.html file="gallery/Mercedes ML63 AMG.jpg" alt="" caption="Mercedes ML63 AMG (car model by LYES94; all models are from BlendSwap, adapted for use with Photon-v2 renderer)" width="100%" %}

{% include image_gallery.html file="gallery/bathroom_(based on Salle de bain by nacimus).jpg" alt="" caption="Cozy Bathroom (based on \"Salle de bain\" by nacimus)" width="100%" %}

{% include image_gallery.html file="gallery/054_chess (based on _Transparent Chess For Cycle_ by yayel59).jpg" alt="" caption="Metallic Chess (based on \"Transparent Chess For Cycle\" by yayel59)" width="100%" %}

## A Brief History

Initially, it was a side project where I experiment with some global illumination techniques for my game engine (called Tokzin), and both of them were written in Java. It had occurred to me that Java, although easy to code and sometimes outperforms compiled (to machine code) languages thanks to its JIT system, the restricted accessibilities to system memory makes it hard to implement some of the low level optimizations. In 2016, I decided to rewrite the rendering engine in C++ for better performance, and ported most of the code from the original Java codebase. It is worth noting that the C++ version was more than 20% faster rendering the Crytek Sponza scene than its Java counterpart out of the box. At that time, I bumped Photon’s version number into 2.0 after a complete refactor of the core architecture.

## More on the Project

* The project has been thoroughly documented in its [dedicated website](photon_v2_what_is_photon.html).
* This is an open-source project. Full [source code](https://github.com/TzuChieh/Photon-v2) available.
