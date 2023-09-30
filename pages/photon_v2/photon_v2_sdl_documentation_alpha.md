---
title: Photon Scene Description Language (alpha)
keywords: 
last_updated: August 15, 2021
summary: "Full documentation of PSDL."
sidebar: photon_v2_sidebar
permalink: photon_v2_sdl_documentation_alpha.html
---
# Photon Scene Description Language

## Geometry

* Category: `Geometry`
* Type: `Geometry`
* Note: **blueprint only**

Defining the shape of scene elements.



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


## Material

* Category: `Material`
* Type: `Material`
* Note: **blueprint only**

Defines and models the appearance of scene elements.



## Surface Material

* Category: `Material`
* Type: `Surface Material`
* Note: **blueprint only**, based on **Material**

*(no description)*



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
| f0 | `spectrum` | Surface reflectance on normal incidence. This value is expected to be given in linear-SRGB space. When this parameter is used, the underlying Fresnel model will be an approximated one (schlick) which is pretty popular in real-time graphics. |
| ior-outer | `real` | The index of refraction outside of this interface. |
| ior-inner-n | `spectrum` | The complex index of refraction (real part) inside of this interface. |
| ior-inner-k | `spectrum` | The complex index of refraction (imaginary part) inside of this interface. |
| microsurface | `enum` | Type of the microsurface of the material. |
| roughness-to-alpha | `enum` | Type of the mapping to transform roughness into alpha value. |
| roughness | `real` | Isotropic surface roughness in [0, 1], the material will appear to be smoother with smaller roughness value. |
| roughness-v | `real` | Similar to the `roughness` parameter, but is used for anisotropic surface appearances. This value controls the V component of surface roughness. If this value is provided, the `roughness` parameter is interpreted as the U component of surface roughness. |


## Light Source

* Category: `Light Source`
* Type: `Light Source`
* Note: **blueprint only**

The source of all energy emitting entity in the scene.



## Area Light Source

* Category: `Light Source`
* Type: `Area`
* Note: **blueprint only**, based on **Light Source**

This type of light source has a finite area. Energy is allowed toemit as long as the emitting source is within the area.



## Spherical Light Source

* Category: `Light Source`
* Type: `Sphere`
* Note: **concrete**, based on **Area Light Source**

This type of light emits energy from a spherical shape.

> Creation: `light-source(sphere)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| radius | `real` | The radius of the sphere. |


## Rectangular Light Source

* Category: `Light Source`
* Type: `Rectangle`
* Note: **concrete**, based on **Area Light Source**

This type of light emits energy from a rectangular shape.Note that energyis only allowed to emit from one side of the rectangle, not both sides.

> Creation: `light-source(rectangle)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| width | `real` | The width of the rectangle. |
| height | `real` | The height of the rectangle. |


## Observer

* Category: `Observer`
* Type: `Observer`
* Note: **blueprint only**

A tool for observing the incoming energy of the scene.



## Oriented Raster Observer

* Category: `Observer`
* Type: `Oriented Raster`
* Note: **blueprint only**, based on **Observer**

Observers that work by projecting incoming energy in certain ways. Projective observers face the -z axis (+y up) and reside on (0, 0, 0) by default.



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
| sensor-offset-mm | `real` | Distance between sensor and light entry. Can be overridden if FoV is provided. |
| fov-degrees | `real` | Field of view of this observer in degrees. If provided, it will be used to adjust sensor offset such that the desired FoV is reached. |


## Sample Source

* Category: `Sample Source`
* Type: `Sample Source`
* Note: **blueprint only**

Engine component for generating sample values.



## Runtime Sample Source

* Category: `Sample Source`
* Type: `Runtime`
* Note: **blueprint only**, based on **Sample Source**

Sample sources that generate samples during render engine execution time.



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



## Frame Visualizer

* Category: `Visualizer`
* Type: `Frame`
* Note: **blueprint only**, based on **Visualizer**

A visualizer that produces frames, a typical example is an image.



## Path Tracing Visualizer

* Category: `Visualizer`
* Type: `Path Tracing`
* Note: **concrete**, based on **Frame Visualizer**

Render frames with common path tracing methods.

> Creation: `visualizer(path-tracing)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| scheduler | `enum` | Scheduler for rendering, affect the order of rendered regions. |
| estimator | `enum` | Scheduler for rendering, affect the order of rendered regions. |
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


## Actor

* Category: `Actor`
* Type: `Actor`
* Note: **blueprint only**

Represents an entity in the scene. Every entity that participates in a scene is an actor.



## Physical Actor

* Category: `Actor`
* Type: `Physical`
* Note: **blueprint only**, based on **Actor**

An actor that is visible and can be transformed.


> Operation: `translate`

Moves the actor away from the original location with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| amount | `vector3` | The amount to move on each axis. |

> Operation: `rotate`

Rotates the actor along an axis with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| axis | `vector3` | The axis for rotation. |
| degrees | `real` | The amount of the rotation, in degrees. |
| rotation | `quaternion` | Specify the rotation with a quaternion directly. |

> Operation: `scale`

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


## Light Actor

* Category: `Actor`
* Type: `Light`
* Note: **concrete**, based on **Physical Actor**

An actor that represents a light in the scene.

> Creation: `actor(light)`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| source | `light-source` | The source of the energy. |



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
| `box` | Fairly sharp, fast to evaluate, but can have obvious aliasing around edges. |
| `gaussian` | Gives smooth results, slower to evaluate and can sometimes result in blurry images. |
| `mn` | Smooth but remains sharp around edges. |
| `bh` | A good compromise between smoothness and sharpness. |

## Color Space

Marks color space information of input values.

| Entries | Descriptions |
| --- | --- |
| *(empty)* | *(no description)* |
| `LSRGB` | *(no description)* |
| `SRGB` | *(no description)* |
| `SPD` | *(no description)* |


