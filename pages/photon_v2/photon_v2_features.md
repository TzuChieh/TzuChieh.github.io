---
title: Features Overview
keywords: 
last_updated: August 11, 2020
summary: "A quick overview of the features supported by Photon in each version."
sidebar: photon_v2_sidebar
permalink: photon_v2_features.html
---

## Version 2.0.0

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
