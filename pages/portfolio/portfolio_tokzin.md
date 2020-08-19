---
title: "Tokzin Game Engine"
keywords: 
tags: 
toc: true
sidebar: portfolio_sidebar
permalink: portfolio_tokzin.html
summary: 
last_updated: August 16, 2020
---

## Introduction

Tokzin is a game engine that features physically based rendering. It supports both forward and deferred render mode and uses OpenGL internally. A great deal of real-time rendering algorithms has been added into the core of the engine. Other than that, audio is implemented via OpenAL and a third-party physics simulator (Bullet) is integrated into the engine. Tokzin was written in Java and took approximately 3 years to develop.

## List of Main Features

* Physically based materials (Cook-Torrance, metalness workflow)
* Forward & Deferred render pipeline
* Soft Shadow
  * Percentage Closer Filtering (PCF)
  * Variance Shadow Map (VSM)
* Normal compression (Crytek's G-buffer compression algorithm)
* Image based lighting
  * Specular roughness mipmaps
  * Diffuse map based on spherical harmonics
* Screen Space Ambient Occlusion (SSAO)
* Fast Approximate Anti-Aliasing (FXAA)
* Dynamic lights
  * directional light
  * point light
  * spot light
  * line light
* Lens Flare
* Volumetric Light Shafts (godrays)
* Volumetric Fog
* Frustum Culling (based on octree)
* Texture mapping
  * Normal mapping
  * Relief mapping
  * Parallax occlusion mapping
  * Specular (roughness) mapping
  * Environment mapping
* High Dynamic Range (HDR) rendering
* Specular occlusion (Frostbite's method)
* Billboards
* OpenGL state sorting (optimization)
* Custom GUI (based on OpenGL)
* Physics engine integration (Bullet)
* Audio (based on OpenAL)

## Video Documentations

<iframe width="560" height="315" src="https://www.youtube.com/embed/_DPdp7NqzSE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ObDJ3mYE4zQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Tr_2b5EwDGw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/QkiLlWiZJrE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

You can find more videos about Tokzin [here](https://www.youtube.com/playlist?list=PLTb8yNz82VDXlove7p_BXdwRHxHXBrMxv).

## Images

{% include image_gallery.html file="portfolio/tokzin_custom_test_site.jpg" alt="" caption="Custom algorithm test site" width="90%" %}

{% include image_gallery.html file="portfolio/tokzin_utah_teapot.jpg" alt="" caption="Various Utah teapot with different PBR materials" width="90%" %}

{% include image_gallery.html file="portfolio/tokzin_mat_test.jpg" alt="" caption="Using Mitsuba material ball for development" width="90%" %}

{% include image_gallery.html file="portfolio/tokzin_sponza.jpg" alt="" caption="Filling the famous Sponza scene with random objects" width="90%" %}
