---
title: What is Photon
keywords: 
last_updated: September 25, 2018
summary: "A quick overview of all non-trivial features Photon currently has."
sidebar: features_sidebar
permalink: features_overview.html
---

* **Rendering**
  * Backward Path Tracing
  * Backward Path Tracing with Next Event Estimation
  * Photon Mapping
  * Progressive Photon Mapping
  * Stochastic Progressive Photon Mapping
  * RGB and Spectral Rendering
  * AOV Rendering (normal)
  * Random and Stratified Sampling

* **Imaging and Film**
  * Pinhole and Thin Lens Cameras
  * Film Filtering
    * (box, Gaussian, Mitchell-Netravali, Blackman-Harris)
  * Tone-mapping (Jim Hejl and Richard Burgess-Dawson)

* **Material**
  * Lambertian Diffuse
  * Microfacet-based Opaque Model
    * isotropic-GGX distribution
    * anisotropic-GGX distribution
  * Microfacet-based Translucent Model
    * isotropic-GGX distribution
  * Ideal Reflector, Transmitter and Absorber
  * Spectral Complex IoR
  * Layered Surface Material (Belcour's model)
  * Lerped BSDF
  * Schlick and Exact Fresnel Models

* **Geometry**
  * Triangle, Rectangle, Sphere, Cuboid, Triangle Mesh
  * Simple 2-D Wave, Fractal
  * Instancing
  * Acceleration Structures
    * BVH
    * kD-tree (point, indexed, referenced)
  * Linearly Interpolated Motion

* **Light**
  * Point Light, Area Light (sphere, rectangle)
  * Geometric Light
  * HDR Environment Map
    * with importance sampling
  * IES Light Profiles

* **Texture**
  * Texturing with Ordinary File Formats (.jpg, .png, etc)
  * Mathematical Modifiers (add, multiply)

* **Misc.**
  * Blender Addon for Scene Creation
  * Easy-to-write Custom Scene Description Language
  * GUI for Rendering and Scene Management
  * CLI for Server Usages
  * Loading and Rendering Minecraft Maps
  * Hierarchical Scene Graph

For corresponding references, please see the [source code](https://github.com/TzuChieh/Photon-v2).
