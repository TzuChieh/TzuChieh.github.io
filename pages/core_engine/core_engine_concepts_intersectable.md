---
title: Intersectable
keywords: 
last_updated: September 29, 2018
summary: "Representing elements on which intersection tests can be performed."
sidebar: core_engine_sidebar
permalink: core_engine_concepts_intersectable.html
---

To construct a scene, we must populate it with some *objects*. Imagining you are beside a table with a mug on it, how would you describe the shape of those two objects? Specifically, how to represent them digitally in a computer? One way to do this is to model them using many triangles or quads. Take a triangle for example, in a renderer like Photon, merely store the three vertices of it is not enough: we need to support opearations on the stored data for it to be useful.

The most common operation is **ray intersection test**. We need to know whether a given ray is intersecting a triangle for the rest of the system to work. Remember that we can also model the table and mug using other shapes such as quads, they should support the same operation set as triangles. Photon supports many kinds of *object* that can be **intersected** by rays, such as just-mentioned triangles and quads, and they are named after this capability: **Intersectable**.

Generally, an intersectable object does not support ray intersection tests only, they should support the following operations in order to be a full-featured **intersectable**

* ray intersection test

  Able to detect whether a given ray hits the intersectable.

* report geometric properties where the ray hit

  Calculates properties such as the coordinates of hit, the normal vector of hit point, surface parameterization, and partial derivatives if possible.

* AABB calculation

  Able to calculate an Axis-Aligned Bounding Box of itself.

Please refer to source code for more details. \[[Source Code](https://github.com/TzuChieh/Photon-v2/blob/master/Engine/Source/Core/Intersectable/Intersectable.h)\]