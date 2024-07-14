---
title: Introduction
keywords: 
last_updated: September 26, 2018
summary: "Gemetries define shapes in a scene."
sidebar: photon_v2_sidebar
permalink: photon_v2_geometry_introduction.html
---

{% include warning.html content="Documentation deprecated. Please visit the [project website](https://tzuchieh.github.io/Photon-v2-site/engine_docs/v2.0.0-beta/Photon/html/index.html) for up-to-date content." %}

If there is a ball in the scene, we can create a sphere geometry to represent it; if there is a piece of paper on the table, we can use a rectangle geometry to model it. Geometries are the barebone of a scene: materials, lights, physical motions... are all built on top of geometries, they are basically the heart of a virtual world. We show some common types of geometries in the following sections to give you a rough idea how geometries are like in Photon renderer.

## Rectangle, Triangle, and Sphere

These are common basic shapes to have in a renderer. They are useful for defining the shape of light sources or for further tessellation:

{% include image_gallery.html file="photon_v2/rectangle_geometry.png" alt="" caption="A rectangle." width="90%" %}

{% include image_gallery.html file="photon_v2/triangle_geometry.png" alt="" caption="A triangle. Complex shapes are often built with triangles." width="90%" %}

{% include image_gallery.html file="photon_v2/sphere_geometry.png" alt="" caption="A sphere. Useful from small light sources to a large dome." width="90%" %}

## Triangle Mesh

Games, modeling programs, and other applications typically use triangle mesh to represent arbitrary 3-D shapes. It is basically a collection of triangles grouping in a way that approximate some shapes. Below is a famous model called *Suzanne*.

{% include image_gallery.html file="photon_v2/triangle_mesh_geometry.png" alt="" caption="A triangle mesh." width="90%" %}

## Cuboid

It is quite useful to have a generalized cube at hand. Unlike cubes, a cuboid allows variable extents. Cuboids are axis-aligned bounding boxes (AABB) in their local space.

{% include image_gallery.html file="photon_v2/cuboid_geometry.png" alt="" caption="A Cuboid (in fact a cube in this image)." width="90%" %}

A bonus to have cuboids is that voxel games like Minecraft can be rendered easily. Here is a work-in-progress render of a Minecraft level parser that tries to translate in-game data into SDL:

{% include image_gallery.html file="photon_v2/textured_mc.png" alt="" caption="Test render of a Minecraft level parser." width="90%" %}

## Miscellaneous

We support also some interesting geometries such as wave and fractals. A wave is basically a cuboid with its top surface being tessellated according to a superposition of 2-D sine and cosine functions. These special geometries are sometimes useful for modeling a scene.

{% include image_gallery.html file="photon_v2/water_dragon_color_light.png" alt="" caption="A triangle mesh submerged inside a wave geometry." width="90%" %}

{% include image_gallery.html file="photon_v2/menger_sponge.png" alt="" caption="A fractal geometry (Menger sponge)." width="90%" %}
