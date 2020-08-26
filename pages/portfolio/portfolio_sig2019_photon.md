---
title: "Photon: A Modular, Research-Oriented Rendering System"
keywords: 
tags: 
toc: true
sidebar: portfolio_sidebar
permalink: portfolio_sig2019_photon.html
summary: A poster presented in ACM SIGGRAPH 2019.
last_updated: August 16, 2020
---

{% include image_gallery.html file="portfolio/teaser_wt.jpeg" alt="" caption="Several visualization techniques implemented using the building blocks provided by our system. In the center, the buddha features
Belcour’s BSDF model [Belcour 2018]; while the glass brick (left) induces caustics that can be rendered efficiently using particle tracing methods." width="100%" %}

## Introduction

Authors: [Tzu-Chieh Chang](https://tzuchieh.github.io/index.html), [Ming Ouhyoung](https://www.csie.ntu.edu.tw/~ming/)

To develop a graphics project with ease and confidence, the reliability and extensibility of the underlying framework are essential. While there are existing options, e.g., pbrt-v3 and Mitsuba, they either focus on education or not being updated for a long time. We would like to present an alternative solution named Photon.
Photon is an open-source and cross-platform1 rendering system that, in its core, is designed with modularity and research in mind. The goal of our system is to provide a set of building blocks to facilitate the implementation of new rendering algorithms, as well as a unified foundation for comparing the performance
of different methods. In addition, our system comes with both CLI and GUI applications, and the later is particularly useful for interactive visualization of the rendering progress. A Blender add-on is also available for content creation and can export 3-D assets to our scene description format. In this article, we first propose a tri-layer software architecture that encapsulates common graphics concepts as independent modules, while maintaining the ability to fine-tune the behavior of each submodule. Secondly, we demonstrate the flexibility of the architecture by implementing several rendering algorithms, then showcasing some useful features. Finally, we conclude with a general comparison between similar systems and planned features for
future releases.

## Downloads and Links

* [Abstract](images/portfolio/sig2019_photon_abstract.pdf) (13.3 MB)
* [Poster](images/portfolio/sig2019_photon_poster.pdf) (828 KB)
* [Link to ACM Digital Library](https://dl.acm.org/doi/10.1145/3306214.3338586)
* This is an open-source project. Full [source code](https://github.com/TzuChieh/Photon-v2) available.
