---
title: Photon Scene Description Language
keywords: 
last_updated: September 30, 2023
summary: "Full documentation of PSDL."
sidebar: photon_v2_sidebar
permalink: photon_v2_sdl_documentation.html
---

{% include warning.html content="Documentation deprecated. Please visit the [project website](https://tzuchieh.github.io/Photon-v2-site/engine_docs/v2.0.0-beta/Photon/html/index.html) for up-to-date content." %}

# Photon Scene Description Language

## Geometry

* Category: `Geometry`
* Type: `Geometry`
* Note: **blueprint only**

Defining the shape of scene elements.

*(no input)*


## Spherical Geometry

* Category: `Geometry`
* Type: `Sphere`
* Note: **concrete**, based on **Geometry**

A perfectly round shape centering around origin.

> Creation: `geometry(sphere)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| radius | `real` | Size of the sphere. |


## Rectangular Geometry

* Category: `Geometry`
* Type: `Rectangle`
* Note: **concrete**, based on **Geometry**

A rectangular shape on xy-plane. It is centered around origin.

> Creation: `geometry(rectangle)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| width | `real` | Width of the rectangle. |
| height | `real` | Height of the rectangle. |
| texcoord-scale | `real` | A scaling factor that scales the default-generated texture coordinates. |


## Triangle Geometry

* Category: `Geometry`
* Type: `Triangle`
* Note: **concrete**, based on **Geometry**

A single triangle-shaped surface. Please note that using this type of triangle for triangle mesh may induce significant overhead (in terms of memory usage). This is meant for very simple shapes or debug usages.

> Creation: `geometry(triangle)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| v-A | `vector3` | The first vertex coordinates of the triangle. |
| v-B | `vector3` | The second vertex coordinates of the triangle, in CCW. |
| v-C | `vector3` | The third vertex coordinates of the triangle, in CCW. |
| uvw-A | `vector3` | Texture coordinates of the first vertex. |
| uvw-B | `vector3` | Texture coordinates of the first vertex. |
| uvw-C | `vector3` | Texture coordinates of the first vertex. |
| n-A | `vector3` | Normal vector of the first vertex. |
| n-B | `vector3` | Normal vector of the second vertex. |
| n-C | `vector3` | Normal vector of the third vertex. |


## Triangle Mesh

* Category: `Geometry`
* Type: `Triangle Mesh`
* Note: **concrete**, based on **Geometry**

A cluster of triangles forming a singe shape in 3-D space.

> Creation: `geometry(triangle-mesh)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| positions | `vector3-array` | Vertex coordinates of all triangles. Every three vector3s in the array represents a single triangle. The vertices are expected to be given in counterclockwise order. |
| texture-coordinates | `vector3-array` | Similar to positions, except that the array stores texture coordinates for each triangle. |
| normals | `vector3-array` | Similar to positions, except that the array stores normal vectors for each triangle. |


## Menger Sponge Geometry

* Category: `Geometry`
* Type: `Menger Sponge`
* Note: **concrete**, based on **Geometry**

A fractal geometry.

> Creation: `geometry(menger-sponge)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| iterations | `integer` | Number of iterations on the fractal surface detail. |


## Geometry Soup

* Category: `Geometry`
* Type: `Geometry Soup`
* Note: **concrete**, based on **Geometry**

A collection of random geometries.

> Creation: `geometry(geometry-soup)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| geometries | `geometry-array` | Array of references to the geometries in the soup. |


## PLY Polygon Mesh

* Category: `Geometry`
* Type: `Ply`
* Note: **concrete**, based on **Geometry**

Polygon mesh stored as a .ply file.

> Creation: `geometry(ply)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| ply-file | `PRI` | The .ply file that stores the polygon mesh. |


## Material

* Category: `Material`
* Type: `Material`
* Note: **blueprint only**

Defines and models the appearance of scene elements.

*(no input)*


## Surface Material

* Category: `Material`
* Type: `Surface Material`
* Note: **blueprint only**, based on **Material**

*(no description)*

*(no input)*


## Matte Opaque Material

* Category: `Material`
* Type: `Matte Opaque`
* Note: **concrete**, based on **Surface Material**

A material model for surfaces with matte look, such as chalk and moon.

> Creation: `material(matte-opaque)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| albedo | `image` | An image or constant color that will be used for describing albedo. |
| sigma-degrees | `image` | Roughness in standard deviation of surface orientation (unit: degrees). |


## Abraded Opaque Material

* Category: `Material`
* Type: `Abraded Opaque`
* Note: **concrete**, based on **Surface Material**

Able to model surfaces ranging from nearly specular to extremely rough appearances.

> Creation: `material(abraded-opaque)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| fresnel | `enum` | Type of the Fresnel for the conductive interface. |
| f0 | `spectrum` | Surface reflectance on normal incidence. This value is expected to be given in linear-sRGB space. When this parameter is used, the underlying Fresnel model will be an approximated one (schlick) which is pretty popular in real-time graphics. Also note that F0 already includes the information of ior-outer. |
| ior-outer | `real` | The index of refraction outside of this interface. |
| ior-inner-n | `spectrum` | The complex index of refraction (real part) inside of this interface. |
| ior-inner-k | `spectrum` | The complex index of refraction (imaginary part) inside of this interface. |
| microsurface | `enum` | Type of the microsurface of the material. |
| roughness-to-alpha | `enum` | Type of the mapping to transform roughness into alpha value. |
| roughness | `real` | Isotropic surface roughness in [0, 1], the material will appear to be smoother with smaller roughness value. |
| roughness-v | `real` | Similar to the `roughness` parameter, but is used for anisotropic surface appearances. This value controls the V component of surface roughness. If this value is provided, the `roughness` parameter is interpreted as the U component of surface roughness. |


## Abraded Translucent Material

* Category: `Material`
* Type: `Abraded Translucent`
* Note: **concrete**, based on **Surface Material**

Able to model translucent surfaces with variable roughnesses. Such as frosted glass.

> Creation: `material(abraded-translucent)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| fresnel | `enum` | Type of the Fresnel for the dielectric interface. |
| ior-outer | `real` | The index of refraction outside of this interface. |
| ior-inner | `real` | The index of refraction inside of this interface. |
| microsurface | `enum` | Type of the microsurface of the material. |
| roughness-to-alpha | `enum` | Type of the mapping to transform roughness into alpha value. |
| roughness | `real` | Isotropic surface roughness in [0, 1], the material will appear to be smoother with smaller roughness value. |
| roughness-v | `real` | Similar to the `roughness` parameter, but is used for anisotropic surface appearances. This value controls the V component of surface roughness. If this value is provided, the `roughness` parameter is interpreted as the U component of surface roughness. |


## Full Material

* Category: `Material`
* Type: `Full`
* Note: **concrete**, based on **Material**

A material model that combines surface and volume properties.

> Creation: `material(full)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| surface | `material` | A surface material. |
| interior | `material` | A volume material describing the inside of the surface. |
| exterior | `material` | A volume material describing the outside of the surface. |


## Ideal Substance Material

* Category: `Material`
* Type: `Ideal Substance`
* Note: **concrete**, based on **Surface Material**

Models a perfectly smooth surface with various physical properties.

> Creation: `material(ideal-substance)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| substance | `enum` | Specifying the physical property/behavior of the surface. |
| fresnel | `enum` | Type of the Fresnel for the interface. |
| ior-outer | `real` | The index of refraction outside the surface. |
| ior-inner | `real` | The index of refraction inside the surface. |
| f0 | `spectrum` | Surface reflectance on normal incidence. This value is expected to be given in linear-sRGB space. When this parameter is used, the underlying Fresnel model will be an approximated one (schlick) which is pretty popular in real-time graphics. |
| reflection-scale | `spectrum` | A scaling factor for reflected energy. Note that this property is only for artistic control and is not physically correct. |
| transmission-scale | `spectrum` | A scaling factor for transmitted energy. Note that this property is only for artistic control and is not physically correct. |
| ior-inner-n | `spectrum` | The complex index of refraction (real part) inside the metallic interface. |
| ior-inner-k | `spectrum` | The complex index of refraction (imaginary part) inside the metallic interface. |


## Binary Mixed Surface

* Category: `Material`
* Type: `Binary Mixed Surface`
* Note: **concrete**, based on **Surface Material**

Mixing two surface materials in various ways.

> Creation: `material(binary-mixed-surface)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| mode | `enum` | Specify how two materials are mixed. |
| material-0 | `material` | The first material that participates the mixing process. |
| material-1 | `material` | The second material that participates the mixing process. |
| factor | `image` | Factor that controls the contribution from each material. |


## Image

* Category: `Image`
* Type: `Image`
* Note: **blueprint only**

A block of data.

*(no input)*


## Constant Image

* Category: `Image`
* Type: `Constant`
* Note: **concrete**, based on **Image**

An image that stores constant value. It can be a single scalar, a vector or a color.

> Creation: `image(constant)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| value | `real-array` | A series of values to populate the const image. |
| color-space | `enum` | Associated color space of the constant. |


## Base of Raster Image

* Category: `Image`
* Type: `Raster Base`
* Note: **blueprint only**, based on **Image**

Common information for raster-based images.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| sample-mode | `enum` | Sample mode of the raster image. |
| wrap-mode | `enum` | Wrap mode of the raster image. |
| vertical-wrap-mode | `enum` | Wrap mode of the raster image in the vertical direction. If this field is specified, the <wrap-mode> field is treated as the horizontal wrap mode. |


## Raster File Image

* Category: `Image`
* Type: `Raster File`
* Note: **concrete**, based on **Base of Raster Image**

Raster-based image file (most common image file formats belongs to this category).

> Creation: `image(raster-file)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| image-file | `PRI` | The image file. |


## Math Image

* Category: `Image`
* Type: `Math`
* Note: **concrete**, based on **Image**

This image applies mathematical modifications on other images, such as addition and multiplication.

> Creation: `image(math)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| math-image-op | `enum` | The mathematical operation used. |
| operand | `image` | The target image that is going to be operated on. |
| scalar-input | `real` | A scalar input for the specified mathematical operation. |
| input-0 | `image` | First input for the specified mathematical operation. |
| input-1 | `image` | Second input for the specified mathematical operation. |


## Black-body Radiation Image

* Category: `Image`
* Type: `Black Body`
* Note: **concrete**, based on **Image**

An image outputs the value of black-body radiation.

> Creation: `image(black-body)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| temperature-k | `real` | Temperature (in Kelvin) that the black-body radiates on. |
| is-spectral-radiance | `bool` | false (default): The energy unit is in radiance; true: The energy unit is in spectral radiance. If "energy" value is specified, this option will have no effect (the user is then responsible for specifying "energy" value in their desired unit). |
| energy | `real` | If specified, the resulting radiation will be adjusted (scaled) to the target energy level; otherwise, the true energy level at the temperature will be used. |
| color-space | `enum` | The tristimulus color space to use when using the image as a numeric texture. The default is to use the current tristimulus space, and linear-sRGB when the engine is in spectral mode. |


## Observer

* Category: `Observer`
* Type: `Observer`
* Note: **blueprint only**

A tool for observing the incoming energy of the scene.

*(no input)*


## Oriented Raster Observer

* Category: `Observer`
* Type: `Oriented Raster`
* Note: **blueprint only**, based on **Observer**

Observers that work by projecting incoming energy in certain ways. Projective observers face the -z axis (+y up) and reside on (0, 0, 0) by default.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| position | `vector3` | Position of the observer. |
| yaw-pitch-row-degrees | `vector3` | Direction that this observer is looking at in yaw pitch form. yaw: Rotation around +y axis in [-180, 180]; pitch: Declination from the horizon in [-90, 90]; row: Rotation around +z axis in [-180, 180]. |
| direction | `vector3` | Direction vector that this observer is looking at. No need to be normalized. |
| up-axis | `vector3` | The direction vector that this observer consider as upward. No need to be normalized. |


## Single-Lens Observer

* Category: `Observer`
* Type: `Single Lens`
* Note: **concrete**, based on **Oriented Raster Observer**

As its name suggests, the lens system in this observer is assumed to have just a single lens. The biggest advantage of it is that depth of field effects are possible under this model. In case of the lens radius is zero, the lens system will be reduced to a pinhole. Images captured by this observer is similar to how a normal human perceives the world but with several simplifications.

> Creation: `observer(single-lens)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| lens-radius-mm | `real` | Radius of the lens in millimeters. |
| focal-distance-mm | `real` | The distance in millimeters that the observer is focusing on. |
| sensor-width-mm | `real` | Width of the sensor used by this observer in millimeters. |
| sensor-offset-mm | `real` | Distance between sensor and light entry (more commonly known as focal length). Will be overridden if FoV is provided. |
| fov-degrees | `real` | Field of view of this observer in degrees. If provided, it will be used to adjust sensor offset such that the desired FoV is reached. |


## Sample Source

* Category: `Sample Source`
* Type: `Sample Source`
* Note: **blueprint only**

Engine component for generating sample values.

*(no input)*


## Runtime Sample Source

* Category: `Sample Source`
* Type: `Runtime`
* Note: **blueprint only**, based on **Sample Source**

Sample sources that generate samples during render engine execution time.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| samples | `integer` | Number of samples that will be generated. This is the number of samples that each data unit (such as a single pixel) will receive, on average. |


## Uniform Random Sample Source

* Category: `Sample Source`
* Type: `Uniform Random`
* Note: **concrete**, based on **Runtime Sample Source**

Generating samples in a completely random fashion.

> Creation: `sample-source(uniform-random)`

*(no input)*


## Stratified Sample Source

* Category: `Sample Source`
* Type: `Stratified`
* Note: **concrete**, based on **Runtime Sample Source**

Generating samples based on engine provided dimensional hints.

> Creation: `sample-source(stratified)`

*(no input)*


## Halton Sample Source

* Category: `Sample Source`
* Type: `Halton`
* Note: **concrete**, based on **Runtime Sample Source**

Generating samples based on the Halton sequence. The samples generated are somewhat deterministic and can lead to visible patterns if the number of samples is too low.

> Creation: `sample-source(halton)`

*(no input)*


## Visualizer

* Category: `Visualizer`
* Type: `Visualizer`
* Note: **blueprint only**

The main engine component for producing visual content.

*(no input)*


## Frame Visualizer

* Category: `Visualizer`
* Type: `Frame`
* Note: **blueprint only**, based on **Visualizer**

A visualizer that produces frames, a typical example is an image.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| rect-x | `integer` | X coordinate of the lower-left corner of the film cropping window. |
| rect-y | `integer` | Y coordinate of the lower-left corner of the film cropping window. |
| rect-w | `integer` | Width of the film cropping window. |
| rect-h | `integer` | Height of the film cropping window. |


## Path Tracing Visualizer

* Category: `Visualizer`
* Type: `Path Tracing`
* Note: **concrete**, based on **Frame Visualizer**

Render frames with common path tracing methods.

> Creation: `visualizer(path-tracing)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| scheduler | `enum` | Scheduler for rendering, affect the order of rendered regions. |
| estimator | `enum` | The energy estimating component used by the renderer. |
| sample-filter | `enum` | Sample filter for the film sampling process. |


## Option

* Category: `Option`
* Type: `Option`
* Note: **concrete**

Options that control engine runtime behavior.

> Creation: `option(option)`

*(no input)*


## Render Session

* Category: `Option`
* Type: `Render Session`
* Note: **blueprint only**, based on **Option**

Settings for how to perform a render operation.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| session-name | `string` | Name of this render session. |
| num-workers | `integer` | Number of worker threads for the rendering operation. |


## Single Frame Render Session

* Category: `Option`
* Type: `Single Frame Render Session`
* Note: **concrete**, based on **Render Session**

Information regarding the rendering process of a single frame.

> Creation: `option(single-frame-render-session)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| frame-size | `vector2` | Width and height of the frame in pixels. |
| visualizer | `string` | Name of the visualizer resource to use. |
| observer | `string` | Name of the observer resource to use. |
| sample-source | `string` | Name of the sample source resource to use. |
| top-level-accelerator | `enum` | Acceleration structure used on the top level geometries. |


## Object

* Category: `Object`
* Type: `Object`
* Note: **blueprint only**

General object that may refer to any type.

*(no input)*


## Actor

* Category: `Actor`
* Type: `Actor`
* Note: **blueprint only**

Represents an entity in the scene. Every entity that participates in a scene is an actor.

*(no input)*


## Physical Actor

* Category: `Actor`
* Type: `Physical`
* Note: **blueprint only**, based on **Actor**

An actor that is visible and can be transformed.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| position | `vector3` | Position of the entity. |
| rotation | `quaternion` | Rotation of the entity |
| scale | `vector3` | Scale of the entity. |

> Operation: `translate`, callable on `actor(physical)` and its derivations

Moves the actor away from the original location with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| amount | `vector3` | The amount to move on each axis. |

> Operation: `rotate`, callable on `actor(physical)` and its derivations

Rotates the actor along an axis with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| axis | `vector3` | The axis for rotation. |
| degrees | `real` | The amount of the rotation, in degrees. |
| rotation | `quaternion` | Specify the rotation with a quaternion directly. |

> Operation: `scale`, callable on `actor(physical)` and its derivations

Enlarges or shrinks the actor with some specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| amount | `vector3` | The amount to scale on each axis. |


## Model Actor

* Category: `Actor`
* Type: `Model`
* Note: **concrete**, based on **Physical Actor**

An actor that has a certain 3-D shape in the scene.

> Creation: `actor(model)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| geometry | `geometry` | A geometry that represent this actor's shape. |
| material | `material` | A material that describes this actor's surface appearance. |
| motion | `motion` | Movement of this actor. |


## Dome Actor

* Category: `Actor`
* Type: `Dome`
* Note: **blueprint only**, based on **Physical Actor**

A large energy emitting source encompassing the whole scene.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| energy-scale | `real` | A non-physical scale factor for artistic purpose. |


## Image Dome Actor

* Category: `Actor`
* Type: `Image Dome`
* Note: **concrete**, based on **Dome Actor**

Using a background image to represent the energy emitted from far away.

> Creation: `actor(image-dome)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| image-file | `PRI` | An image describing the energy distribution. |


## Preetham Dome Actor

* Category: `Actor`
* Type: `Preetham Dome`
* Note: **concrete**, based on **Dome Actor**

Using Preetham model to generate absolute energy from sky.

> Creation: `actor(preetham-dome)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| turbidity | `real` | Turbidity of the atmosphere. |
| standard-time-24h | `real` | Standard time in 24H. |
| standard-meridian-degrees | `real` | Standard meridian in degrees. |
| site-latitude-degrees | `real` | Site latitude in [-90, 90] degrees ("+" implies N and "-" implies S). |
| site-longitude-degrees | `real` | Site longitude in [0, 360] degrees (with prime meridian being 0) |
| julian-date | `integer` | The day of the year as an integer in the range [1, 366]. |
| sun-phi-theta-degrees | `vector2` | Directly specify sun position in the sky in spherical coordinates. Note that this option may not be physically correct since not every position in the sky is possible for the sun given a location on Earth. |


## Light Actor

* Category: `Actor`
* Type: `Light`
* Note: **blueprint only**, based on **Physical Actor**

The source of all energy emitting entity in the scene.

*(no input)*


## Geometric Light Actor

* Category: `Actor`
* Type: `Geometric Light`
* Note: **blueprint only**, based on **Light Actor**

Energy emitters that come with a physical geometry.

*(no input)*


## Area Light Actor

* Category: `Actor`
* Type: `Area Light`
* Note: **blueprint only**, based on **Geometric Light Actor**

This type of light source has a finite area. Energy is allowed to emit as long as the emitting source is within the area.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| color | `spectrum` | The color of this light source. |
| watts | `real` | Energy emitted by this light source, in watts. |


## Model Light Actor

* Category: `Actor`
* Type: `Model Light`
* Note: **concrete**, based on **Geometric Light Actor**

A light source that emits energy from the surface of a geometry. A surface material model can also be given to describe its surface appearance.

> Creation: `actor(model-light)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| geometry | `geometry` | A geometry that defines the surface energy is going to emit from. |
| material | `material` | A material that describes this source's surface appearance. |
| emitted-radiance | `image` | An image that describes the emitted radiance across the surface. |
| back-face-emit | `bool` | Whether the energy should emit from the back face of the geometry. |


## Point Light Actor

* Category: `Actor`
* Type: `Point Light`
* Note: **concrete**, based on **Area Light Actor**

Power emitting source from a small but not infinitesimal region. Resembling a small light bulb.

> Creation: `actor(point-light)`

*(no input)*


## Rectangular Light Actor

* Category: `Actor`
* Type: `Rectangle Light`
* Note: **concrete**, based on **Area Light Actor**

This type of light emits energy from a rectangular shape.Note that energyis only allowed to emit from one side of the rectangle, not both sides.

> Creation: `actor(rectangle-light)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| width | `real` | The width of the rectangle. |
| height | `real` | The height of the rectangle. |


## Spherical Light Actor

* Category: `Actor`
* Type: `Sphere Light`
* Note: **concrete**, based on **Area Light Actor**

This type of light emits energy from a spherical shape.

> Creation: `actor(sphere-light)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| radius | `real` | The radius of the sphere. |


## IES-Attenuated Light Actor

* Category: `Actor`
* Type: `Ies Attenuated Light`
* Note: **concrete**, based on **Light Actor**

Attenuating energy emitting strength of a light with an IES profile.

> Creation: `actor(ies-attenuated-light)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| source | `actor` | The light source that will be attenuated. |
| ies-file | `PRI` | The IES file. |



## Accelerator

Denotes acceleration structure types.

| Entries | Descriptions |
| --- | --- |
| *(empty)* | *(no description)* |
| `brute-force` | *(no description)* |
| `bvh` | *(no description)* |
| `kd-tree` | *(no description)* |
| `indexed-kd-tree` | *(no description)* |

## Estimator

Type of energy estimation algorithms.

| Entries | Descriptions |
| --- | --- |
| *(empty)* | *(no description)* |
| `bvpt` | Backward path tracing. |
| `bneept` | Backward path tracing with next event estimation. |
| `bvptdl` | Backward path tracing, evaluate direct lighting only (single bounce) |

## Sample Filter

The type of filter used during the sampling process.

| Entries | Descriptions |
| --- | --- |
| *(empty)* | *(no description)* |
| `box` | The box filter. Fairly sharp, fast to evaluate, but can have obvious aliasing around edges. |
| `gaussian` | The Gaussian filter. Gives smooth results, slower to evaluate and can sometimes result in blurry images. |
| `mn` | The Mitchell-Netravali filter. Smooth but remains sharp around edges. |
| `bh` | The Blackman-Harris filter. A good compromise between smoothness and sharpness. |

## Sample Mode

Controls how the image will be sampled.

| Entries | Descriptions |
| --- | --- |
| *(empty)* | *(no description)* |
| `nearest` | *(no description)* |
| `bilinear` | *(no description)* |
| `trilinear` | *(no description)* |

## Wrap Mode

Controls how the image will be sampled when texture coordinates is not within the range [0, 1].

| Entries | Descriptions |
| --- | --- |
| *(empty)* | *(no description)* |
| `repeat` | *(no description)* |
| `clamp-to-edge` | *(no description)* |
| `flipped-clamp-to-edge` | *(no description)* |

## Color Space

Marks color space information of input values.

| Entries | Descriptions |
| --- | --- |
| *(empty)* | *(no description)* |
| `LSRGB` | *(no description)* |
| `SRGB` | *(no description)* |
| `ACES` | *(no description)* |
| `SPD` | *(no description)* |

## Color Usage

Marks color usage information of input values.

| Entries | Descriptions |
| --- | --- |
| *(empty)* | *(no description)* |
| `RAW` | *(no description)* |
| `EMR` | *(no description)* |
| `ECF` | *(no description)* |

## Math Image Op

The mathematical operation used on images.

| Entries | Descriptions |
| --- | --- |
| `ADD` | *(no description)* |
| `MUL` | *(no description)* |

## Interface Fresnel

Controls the Fresnel model used.

| Entries | Descriptions |
| --- | --- |
| *(empty)* | *(no description)* |
| `schlick` | An approximative model developed by Schlick. |
| `exact` | The full-form Fresnel formula. |

## Roughness To Alpha

How roughness value will be mapped to alpha, a value that controls surface normal distribution function.

| Entries | Descriptions |
| --- | --- |
| *(empty)* | *(no description)* |
| `equaled` | Directly assign roughness value as-is to alpha. |
| `squared` | Mapping for a perceptually linear roughness. According to a course note in SIGGRAPH 2014: Moving Frostbite to Physically Based Rendering 3.0, P.68, they concluded that a squared mapping gives slightly better distribution of the profiles (blur amount) among all mip levels in the case of pre-integrated diffuse IBL maps. |
| `pbrt-v3` | The mapping used in PBRT-v3. |

## Ideal Substance

Type of the physical behavior of a perfectly smooth surface.

| Entries | Descriptions |
| --- | --- |
| `absorber` | *(no description)* |
| `dielectric-reflector` | *(no description)* |
| `metallic-reflector` | *(no description)* |
| `transmitter` | *(no description)* |
| `dielectric` | *(no description)* |

## Surface Material Mix Mode

Specify how surface materials are mixed.

| Entries | Descriptions |
| --- | --- |
| `lerp` | *(no description)* |


