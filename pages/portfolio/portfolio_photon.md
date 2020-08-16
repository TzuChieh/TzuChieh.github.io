---
title: "Photon Renderer"
keywords: 
tags: 
toc: true
sidebar: portfolio_sidebar
permalink: portfolio_photon.html
summary: 
last_updated: August 16, 2020
---

## Introduction

Photon is a simple Monte-Carlo path tracer made out of my personal interest in computer graphics. The engine served as a playground as I learned and tried to implement new graphics stuff. The core of the renderer is written in Java, and supports path tracing primarily. Its acceleration structure is a kD-tree with optimal SAH splits (when filled with triangle mesh). The material system is based on Cook-Torrance BSDF, which is famous for its physics-based derivation and modulable surface roughness.

## List of Main Features

* Primitive intersection test
  * Ray-sphere intersection
  * Ray-triangle intersection
* Anti-aliasing samples
* kD-tree with optimal SAH splits
* Physically based materials
  * Lambertian diffuse
  * Cook-Torrance microfacet model (both BRDF & BTDF variants)
  * Supports MERL BRDF database
* Texture for material & emission
* Fully support .obj model (with .mtl loading)
* Dynamic camera control during rendering (WASD-style movement)

## Images

{% include image_gallery.html file="portfolio/photon_teaser.jpg" alt="" caption="Crytek Sponza" width="100%" %}

{% include image_gallery.html file="portfolio/photon_stanford.jpg" alt="" caption="Golden Stanford Dragon" width="100%" %}

{% include image_gallery.html file="portfolio/photon_material_matrix.jpg" alt="" caption="Classic Material Matrix" width="100%" %}

{% include image_gallery.html file="portfolio/photon_transparent_bunny.jpg" alt="" caption="Transparent Stanford Bunny" width="100%" %}

## More on the Project

* This is an open-source project. Full [source code](https://github.com/TzuChieh/Photon) available.
