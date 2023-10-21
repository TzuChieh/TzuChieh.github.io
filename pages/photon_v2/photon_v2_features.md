---
title: Features Overview
keywords: 
last_updated: August 11, 2020
summary: "A quick overview of the features supported by Photon in each version."
sidebar: photon_v2_sidebar
permalink: photon_v2_features.html
---

## Version 2.0.0-beta

* **Rendering**
  * **Backward Unidirectional Path Tracing**
  * **Backward Unidirectional Path Tracing with Next Event Estimation**
  * **Photon Mapping**
  * **Progressive Photon Mapping**
  * **Stochastic Progressive Photon Mapping**
  * **RGB and Spectral Rendering**
  * **AOV Rendering (normal, sample time, sample count)**
  * **Sample Generation**  
    Supports random, stratified, and Halton. In addition to the original Halton, fixed & per-digit scramble are also supported.
  * **Image Rendering**
    * Bulk, Tile, Stripe, Grid, and Spiral Modes
    * Adaptive Sampling

* **Imaging and Film**
  * **Cameras**  
    Supports pinhole, thin Lens, 360 cameras.
  * **Radiant Flux Sensor**  
    General rectangular sensors for radiant flux measurement (e.g., for solar panel efficiency analysis).
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
  * *Experimental: Thin-film*

* **Geometry**
  * **Triangle, Rectangle, Sphere, Cuboid, Triangle Mesh**
  * **Indexed Mesh**  
  Triangle and quad mesh (experimental). Arbitrary number of bit for indices. Various vertex attribute formats from half float to octahedral compression.
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
  * **Accurate black-body radiators**

* **Texture**
  * **Nearest and Bilinear Filtering**
  * **Procedural Generators**
    * constants and checkerboard
  * **Procedural Operators**
    * mathematical modifiers: add, multiply
  * **General Pixel Channel Swizzling**

* **Misc.**
  * **Blender Addon for Scene Creation**  
  With scene manipulation, material construction (node graph), and render preview.
  * **Easy-to-write Custom Scene Description Language**  
  Modular and extensible grammar.
  * **Studio Program for Rendering and Scene Management**  
  In previous version, studio was in Java. From beta and later, all functionalities are moving into UI written fully in C++ to better support the upcoming editor upgrade.
  * **CLI for Server Usage**
  * **Loading and Rendering Minecraft Maps (experimental)**
  * **Hierarchical Scene Graph**
  * **Automatically Generate SDL Interface and Documentation**  
  Currently supports Python, Java.

## Version 2.0.0-alpha

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

Full [source code](https://github.com/TzuChieh/Photon-v2) available.
