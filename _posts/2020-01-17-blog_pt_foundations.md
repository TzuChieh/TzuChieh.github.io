---
title:  "Path Tracing Foundations: A Mathematical Overview"
published: true
toc: true
permalink: blog_pt_foundations.html
summary: "Understanding path tracing from equations."
tags: [sharing]
---

## Introduction

Rendering is a broad term describing a collection of image synthesis techniques that takes geometrical descriptions and material properties of a 3-D scene as input, and outputs a 2-D image of that scene from a specific point of view. In layman's terms, it is like taking a photograph, except the scene and the camera are both computer simulated. The rendering equation (or light transport equation, LTE) proposed by Kajiya[^1] is as follows:

$$
\begin{equation}
    L_{o}\left(p, w_{o}\right)=L_{e}\left(p, w_{o}\right)+\int L_{i}\left(p, w_{i}\right) f\left(p, w_{i}, w_{o}\right) \cos \theta_{i} d w_{i},
\end{equation}
$$

Where $$ L_{o} $$ is the outgoing radiance along direction $$ w_{o} $$ originated at point $$ p $$, and $$ L_{e} $$ is the emitted radiance. Followed is an infamous integral which is extremely hard to solve since the whole LTE is a recursive equation. The integration involves integrating over all incoming radiance multiplied by a special quantity $$ f\left(p, w_{i}, w_{o}\right) $$ commonly known as BSDF (bi-directional scattering distribution function). Recursively expand the LTE and using $$ p $$ plus an arrow to represent both position and direction, we get

### Footnotes

[^1]: J. T. Kajiya, "The rendering equation". SIGGRAPH 1986. 