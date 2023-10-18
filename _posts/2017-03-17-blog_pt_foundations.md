---
title:  "Path Tracing Foundations: A Mathematical Overview"
published: true
toc: true
permalink: blog_pt_foundations.html
summary: "Understanding path tracing from equations."
tags: [sharing]
---

{% include mathjax.html %}

## Introduction

Rendering is a broad term describing a collection of image synthesis techniques that takes geometrical descriptions and material properties of a 3-D scene as input, and outputs a 2-D image of that scene from a specific point of view. In layman's terms, it is like taking a photograph, except the scene and the camera are both computer simulated. The rendering equation (or light transport equation, LTE) proposed by Kajiya[^1] is as follows:

$$
\begin{equation}
    L_{o}\left(p, w_{o}\right)=L_{e}\left(p, w_{o}\right)+\int L_{i}\left(p, w_{i}\right) f\left(p, w_{i}, w_{o}\right) \cos \theta_{i} d w_{i},
\end{equation}
$$

Where $$ L_{o} $$ is the outgoing radiance along direction $$ w_{o} $$ originated at point $$ p $$, and $$ L_{e} $$ is the emitted radiance. Followed is an infamous integral which is extremely hard to solve since the whole LTE is a recursive equation. The integration involves integrating over all incoming radiance multiplied by a special quantity $$ f\left(p, w_{i}, w_{o}\right) $$ commonly known as BSDF (bi-directional scattering distribution function). Recursively expand the LTE and using $$ p $$ plus an arrow to represent both position and direction, we get

$$
\begin{equation}
\begin{split}
    L_{o} & \left(p_{1} \rightarrow p_{0}\right) = L_{e}\left(p_{1} \rightarrow p_{0}\right) \\
    & + \int L_{e}\left(p_{2} \rightarrow p_{1}\right) f\left(p_{2} \rightarrow p_{1} \rightarrow p_{0}\right) \cos \left(\theta_{1}\right) d w_{1} \\
    & + \int \int L_{e}\left(p_{3} \rightarrow p_{2}\right) f\left(p_{3} \rightarrow p_{2} \rightarrow p_{1}\right) \cos \left(\theta_{2}\right) f\left(p_{2} \rightarrow p_{1} \rightarrow p_{0}\right) \cos \left(\theta_{1}\right) d w_{2} d w_{1} \\
    & + \cdots
\end{split}
\end{equation}
$$

which is clearly an infinite-dimensional integral that is really unlikely to have an analytical solution. Techniques like Bi-directional Path Tracing (BDPT), Metropolis Light Transport (MLT), Photon Mapping, Vertex Connection and Merging (VCM) are already proven to be quite effective in solving the LTE, but any of them can be hard to done right without previous experiences. The most basic form of path tracing and be further categorized into 4 different kinds of integration/rendering techniques. I have implemented all of them from scratch as the fundamental building block for advanced techniques (as well as to verify the results of other techniques). Implemented techniques including

### Vanilla Path Tracing

Tracing rays starting at the camera; rays reflect and refract and collect intersection information until an emitter is found. This is the most frequently seen algorithm from online tutorial or elementary rendering courses. This method is unbiased, consistent, but can be slow to converge in most cases.

### Backward Light Tracing

Similar to the aforementioned one, this algorithm is unbiased and consistent. By splitting radiance contribution into direct and indirect parts, we can directly sample the light at each intersection point. Obviously this technique is especially suitable for scenes with small light sources. Sometimes this technique is also called "path tracing with next event estimation".

### MIS'ed Path Tracing

Vanilla Path Tracing (VPT) and Backward Light Tracing (BLT) both have their weaknesses. The former one is good at handling specular surfaces and large light sources, while the later one is good at handling diffusive surfaces and small light sources. Can we combine them in an unbiased & consistent way? Veach's legendary doctoral thesis[^2] proposed a method called Multiple Importance Sampling (MIS) came to the rescue.

### Light (Particle) Tracing

This method is also unbiased and consistent and can be tricky to implement. Using Veach's naming convention: $$ s $$ stands for path vertices staring from the emitter, $$ t $$ for path vertices starting from the camera, light tracing is essentially a $$ s=n $$, $$ t=1 $$ sampling technique of Bi-directional Path Tracing. Interestingly, although many documents mentioned Light Tracing (LT), neither a detailed algorithm description nor a publicly available implementation can be easily found. To my knowledge, my implementation is the second open source Light Tracing integrator.

The following paragraphs will describe how each technique is implemented.

## Pre-requirements

Since I'm implementing these rendering techniques from scratch, the architecture of the renderer must be carefully designed. Inspired by PBRT version 2 and 3[^3], Mitsuba[^4], LuxRender[^5], and Tungsten[^6], I chose the powerful C++ as the main programming language for this project. I later combined the cosine term in the LTE with BSDF into an abstract base class called BSDFcos, each implementation must provide an evaluation, an importance sampling and a method for PDF querying. I implemented the classic Lambertian diffuse BRDF, and microfacet based BSDF materials. Unfortunately the paper by Walter et al.[^7] contains several errata and the most deadly one to me is that he forgot to provide a suitable mapping function from roughness to GGX alpha (luckily PBRT-v3 provided such mapping equation but did not mention how it was derived). My choice of acceleration structure is k-D tree with SAH based subdivision strategy. In the system I designed, camera and emitter implementations must provide several sampling methods which are essential for the integration techniques I have implemented.

## Vanilla Path Tracing

Recursively expand the LTE like how it is done in the introduction section, we got a general representation for the $$ n $$th integral:

$$
\begin{equation}
    T \left(n\right) = \int {\cdots \atop n} \int L_{p}\left(p_{n+1} \rightarrow p_{n}\right)
    \cdot \prod_{i=1}^{n}\Big[f\left(p_{i+1} \rightarrow p_{i} \rightarrow p_{i-1}\right) \cos \left(\theta_{i}\right)\Big] d \omega_1 d \omega_2 \cdots d \omega_n
\end{equation}
$$

Now we can write the LTE with infinite number of expansions as:

$$
\begin{equation}
    L_{o} \left(p_{1} \rightarrow p_{0}\right) = L_{e} \left(p_{1} \rightarrow p_{0}\right)
    + \sum_{n=1}^{\infty} T \left(n\right)
\end{equation}
$$

Quite an elegant form, isn’t it? If you are interested in a more in-depth explanation, be sure to pay a visit to Jiayin Cao's blog[^8] where I learned much of the basic concepts from. Apart from the direct (zero bounce) illumination term $$ L_{e} \left(p_{1} \rightarrow p_{0}\right) $$, each term in the summation represents an integral over $$ n $$ dimensional space. In order to get a reasonable converging rate, Monte-Carlo based integration method is used. Notice that there is no need to generate each path from scratch: by using Russian-Roulette (RR) path terminating technique, if a path terminates at camera vertex $$ t = i $$, one can evaluate the integrand of $$ T \left(1\right) $$, $$ T \left(2\right) $$, $$ \cdots $$ to $$ T \left(i - 1\right) $$. Source code is in "Source/Core/Integrator/BackwardPathTracing.cpp". The correctness of this integration method is verified since some rendered results have been compared to my Java-based renderer which was previously compared to PBRT-v2 and had no differences at all. Following is a rendered image of a simple Cornell Box scene using this technique:

{% include image_custom.html file="blog/2017-03-17-blog_pt_foundations/ref L 16000 simple.png" alt="vanilla path tracing result" caption="" width="80%" %}

### Footnotes

[^1]: J. T. Kajiya, "The rendering equation". SIGGRAPH 1986. 
[^2]: E. Veach, "robust monte carlo methods for light transport simulation," 1997.
[^3]: Matt Pharr, Wenzel Jakob, Greg Humphreys, "Physically Based Rendering 3rd Edition".
[^4]: W. Jakob, "Mitsuba Renderer (http://www.mitsuba-renderer.org/)".
[^5]: LuxRender (http://www.luxrender.net/).
[^6]: B. Bitterli, "Tungsten Renderer (https://benedikt-bitterli.me/tungsten.html)". 
[^7]: B. Walter, "Microfacet Models for Refraction through Rough Surfaces".
[^8]: A Graphics Guy’s Note (https://agraphicsguy.wordpress.com/).