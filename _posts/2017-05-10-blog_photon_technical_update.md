---
title:  "Technical Update on Photon"
published: true
permalink: blog_photon_technical_update.html
summary: "An update (technical aspect) to Photon renderer."
tags: [sharing]
---

The majority of this post is from an old document that has never been released. Before starting, I would like to talk a bit more about why the [first version of Photon renderer](https://github.com/TzuChieh/Photon) is not developed anymore. 

Initially, it was a side project where I experiment with some global illumination techniques for my game engine (called Tokzin), and both of them were written in Java. It had occurred to me that Java, although easy to code and sometimes outperforms compiled languages[^1] thanks to its JIT system, the restricted accessibilities to system memory makes it hard to implement some of the low level optimizations. In 2016, I decided to rewrite the rendering engine in C++ for better performance, and ported most of the code from the original Java codebase. It is worth noting that the C++ version was more than 20% faster rendering the Crytek Sponza[^2] scene than its Java counterpart out of the box. At that time, I bumped Photon’s version number into 2.0 and has been adding features here and there since then.

$$
\begin{aligned}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{aligned}
$$

{% include image_custom.html file="blog/2017-01-31_blog_intro_photon/car.png" alt="image rendered by photon" caption="Lamborghini car model from TF3DM.com" width="90%" %}

[^1]: For compiled languages, I mean C/C++, Rust, Go, Fortran, etc. Although languages like Java and Python can be compiled into bytecode, I call them interpreted languages since they require a VM to execute the code.
[^2]: A scene modeled by Frank Meinl at Crytek.
