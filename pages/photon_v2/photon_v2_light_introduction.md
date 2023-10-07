---
title: Introduction
keywords: 
last_updated: September 26, 2018
summary: "Energy sources in the matrix."
sidebar: photon_v2_sidebar
permalink: photon_v2_light_introduction.html
---

Photon provides several kinds of light sources, and insists on using physically based units for input arguments. The reason is three-fold:

* Photon is physically based, using physically based inputs is natural and more accurate.
* Users can expect consistent renderings between different versions of the software with identical inputs.
* It is easier to verify the results with real world measurements.

The following sections give a brief overview on the types of light sources implemented in Photon.

## Area and Model Light

Photon currently supports three kinds of area light, which are rectangle, sphere and point. People may be surprised that in Photon, point lights belongs to area light. The rationale behind this is that traditional point light introduces an additional singularity in the rendering equation, and we already have quite a lot of them in the system, e.g., pinhole camera and mirror reflection/transmission (and traditional point lights are not physically possible anyway). Each singularity may need special routines or conditionals to handle properly, and to make them working nicely altogether can be pretty hard (at least for me). The idea is to make point lights have a finite volume, typically a sphere with a 1- to 3-cm radius resembling the size of common light bulbs. Maxwell Renderer (http://www.nextlimit.com/maxwell/) has a similar design decision (though I am not sure whether the reason behind it is the same). Below is a series of area light sources, all of them emit 5W of energy (and thus should be of roughly the same brightness):

{% include image_gallery.html file="photon_v2/light_white_5W_point.png" alt="" caption="5W point light (note that our point light has a finite volume)." width="70%" %}

{% include image_gallery.html file="photon_v2/light_white_5W_rectangle_10cm.png" alt="" caption="5W rectangle light (10x10cm)." width="70%" %}

{% include image_gallery.html file="photon_v2/light_white_5W_sphere_10cm.png" alt="" caption="5W sphere light (5cm radius)." width="70%" %}

Model light is a variant of area light. While area light need to have constant emission profile, model light lifted this limitation and allow using variable emission profile (such as textures) on arbitrary geometry:

{% include image_gallery.html file="photon_v2/light_model_source.png" alt="" caption="Textured model light (Utah teapot)." width="70%" %}

## Dome

A powerful method of lighting is image based techniques, also known as environment map or HDRI lighting. The main idea is to assume energy come from far regions can be tabulated with direction vectors as entries. Lighting up a scene with HDRIs is usually the fastest and the most effective way of achieving natural-looking results. In photon we call this type of light source as *dome*. Visit https://hdrihaven.com/ for a nice collection of HDR environment maps.

{% include image_gallery.html file="photon_v2/light_hdri_chess_demo.png" alt="" caption="A scene lit with a dome source." width="70%" %}

{% include image_gallery.html file="photon_v2/light_hdri_for_chess.png" alt="" caption="The dome source in latitude-longitude format (captured by Greg Zaal)." width="70%" %}

## IES Light Profile

An IES light profile stores the distribution of emitted energy of a light fixture. The majority of the dataset are provided by lighting manufacturers, which is useful for interior design (architecture visualization). Most commercial renderers are able to parse and render IES lights, and even some game engines support it. Photon does not treat IES light profiles as an energy distribution function, rather, they are interpreted as energy attenuating filters (energy values are normalized to [0, 1]). The reason of doing this is that user can freely modify the total energy a light emits; otherwise IES light profiles stores absolute energy values. On the other hand, it is always possible to extract the total energy from an IES data file then applying the attenuation to faithfully reproduce the light fixture in the renderer.

{% include image_gallery.html file="photon_v2/light_IES_style1.png" alt="" caption="A wide spread angle described by an IES data file." width="70%" %}

{% include image_gallery.html file="photon_v2/light_IES_style2.png" alt="" caption="A pretty narrow spread angle described by an IES data file." width="70%" %}

{% include image_gallery.html file="photon_v2/light_IES_style3.png" alt="" caption="An interesting IES light profile." width="70%" %}

{% include image_gallery.html file="photon_v2/light_IES_style4.png" alt="" caption="Another interesting IES light profile." width="70%" %}
