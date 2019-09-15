---
title: Photon Scene Description Language
keywords: 
last_updated: September 15, 2019
summary: "Full documentation of PSDL."
sidebar: photon_v2_sidebar
permalink: photon_v2_sdl_documentation.html
---
# Photon Scene Description Language

## Actor

* Category: `actor`
* Type: `actor`

Represents an entity in the scene. Every entity that participates in a scene is an actor.

## Dome Actor

* Category: `actor`
* Type: `dome`

A large energy emitting source encompassing the whole scene.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| env-map | `string` | Resource identifier for a HDRI describing the energy distribution. |

> Operation **translate**:

Moves the actor away from the original location with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| factor | `vector3` | The amount to move in each axis. |

> Operation **rotate**:

Rotates the actor along an axis with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| axis | `vector3` | The axis for rotation. |
| degree | `real` | The amount of the rotation. |
| factor | `quaternion` | Specifying the rotation with a quaternion directly. |

> Operation **scale**:

Enlarges or shrinks the actor with some specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| factor | `vector3` | The amount to scale in each axis. |

## Light Actor

* Category: `actor`
* Type: `light`

An actor that represents a light in the scene.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| light-source | `light-source` | The source of the energy. |

> Operation **translate**:

Moves the actor away from the original location with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| factor | `vector3` | The amount to move in each axis. |

> Operation **rotate**:

Rotates the actor along an axis with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| axis | `vector3` | The axis for rotation. |
| degree | `real` | The amount of the rotation. |
| factor | `quaternion` | Specifying the rotation with a quaternion directly. |

> Operation **scale**:

Enlarges or shrinks the actor with some specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| factor | `vector3` | The amount to scale in each axis. |

## Model Actor

* Category: `actor`
* Type: `model`

An actor that has a certain 3-D shape in the scene.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| geometry | `geometry` | A geometry that represent this actor's shape. |
| material | `material` | A material that describes this actor's surface appearance. |

> Operation **translate**:

Moves the actor away from the original location with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| factor | `vector3` | The amount to move in each axis. |

> Operation **rotate**:

Rotates the actor along an axis with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| axis | `vector3` | The axis for rotation. |
| degree | `real` | The amount of the rotation. |
| factor | `quaternion` | Specifying the rotation with a quaternion directly. |

> Operation **scale**:

Enlarges or shrinks the actor with some specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| factor | `vector3` | The amount to scale in each axis. |

## Phantom Model Actor

* Category: `actor`
* Type: `phantom-model`

An actor that itself will not appear in the scene, but its cooked result can be referenced by others.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| name | `string` | Phantom's name. |
| geometry | `geometry` | A geometry that represent this actor's shape. |
| material | `material` | A material that describes this actor's surface appearance. |

> Operation **translate**:

Moves the actor away from the original location with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| factor | `vector3` | The amount to move in each axis. |

> Operation **rotate**:

Rotates the actor along an axis with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| axis | `vector3` | The axis for rotation. |
| degree | `real` | The amount of the rotation. |
| factor | `quaternion` | Specifying the rotation with a quaternion directly. |

> Operation **scale**:

Enlarges or shrinks the actor with some specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| factor | `vector3` | The amount to scale in each axis. |

## Transformed Instance

* Category: `actor`
* Type: `transformed-instance`

An actor that applies a transformation effect on a phantom.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| name | `string` | Target phantom's name. |

> Operation **translate**:

Moves the actor away from the original location with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| factor | `vector3` | The amount to move in each axis. |

> Operation **rotate**:

Rotates the actor along an axis with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| axis | `vector3` | The axis for rotation. |
| degree | `real` | The amount of the rotation. |
| factor | `quaternion` | Specifying the rotation with a quaternion directly. |

> Operation **scale**:

Enlarges or shrinks the actor with some specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| factor | `vector3` | The amount to scale in each axis. |

## Physical Actor

* Category: `actor`
* Type: `physical`

An actor that is visible and can be transformed.

> Operation **translate**:

Moves the actor away from the original location with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| factor | `vector3` | The amount to move in each axis. |

> Operation **rotate**:

Rotates the actor along an axis with a specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| axis | `vector3` | The axis for rotation. |
| degree | `real` | The amount of the rotation. |
| factor | `quaternion` | Specifying the rotation with a quaternion directly. |

> Operation **scale**:

Enlarges or shrinks the actor with some specified amount.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| factor | `vector3` | The amount to scale in each axis. |

## Cuboid

* Category: `geometry`
* Type: `cuboid`

A shape that is similar to cube but may contain rectangular faces. It is centered around origin.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| min-vertex | `vector3` | Vertex in the (---) octant. |
| max-vertex | `vector3` | Vertex in the (+++) octant. |
| px-face-uv | `quaternion` | UV coordinates of the +x face (+y as upward), in (min-u, min-v, max-u, max-v). |
| nx-face-uv | `quaternion` | UV coordinates of the -x face (+y as upward), in (min-u, min-v, max-u, max-v). |
| pz-face-uv | `quaternion` | UV coordinates of the +z face (+y as upward), in (min-u, min-v, max-u, max-v). |
| nz-face-uv | `quaternion` | UV coordinates of the -z face (+y as upward), in (min-u, min-v, max-u, max-v). |
| py-face-uv | `quaternion` | UV coordinates of the +y face (-z as upward), in (min-u, min-v, max-u, max-v). |
| ny-face-uv | `quaternion` | UV coordinates of the -y face (+z as upward), in (min-u, min-v, max-u, max-v). |

## Empty

* Category: `geometry`
* Type: `empty`

It is just an empty geometry. Nothing is there.

> Creation:

(no input)

## Geometry

* Category: `geometry`
* Type: `geometry`

Defining the shape of scene elements.

## Geometry Soup

* Category: `geometry`
* Type: `geometry-soup`

A collection of geometry.

> Creation:

(no input)

> Operation **add**:

Adds a geometry to the soup.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| geometry | `geometry` | The geometry to be added. |

> Operation **add-transformed**:

Applies transformations on a geometry then add it to the soup.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| geometry | `geometry` | The geometry to be added. |
| translation | `vector3` | Offset amount. |
| rotation-axis | `vector3` | Axis of rotation. |
| rotation-degrees | `real` | Amount of rotation along the rotation axis in degrees. |
| scale | `vector3` | Magnify/minify factor to be applied on the geometry. |

## Rectangle

* Category: `geometry`
* Type: `rectangle`

A rectangular shape on xy-plane. It is centered around origin.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| width | `real` | Width of the rectangle. |
| height | `real` | Height of the rectangle. |
| texcoord-scale | `real` | A scaling factor that scales the default-generated texture coordinates. |

## Sphere

* Category: `geometry`
* Type: `sphere`

A perfectly round shape centering around origin.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| radius | `real` | Size of the sphere. |

## Triangle Mesh

* Category: `geometry`
* Type: `triangle-mesh`

A cluster of triangles forming a singe shape in 3-D space.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| positions | `vector3-array` | Vertices of all triangles. Every three vector3s in the array represents a single triangle. The vertices are expected to be given in counterclockwise order. |
| texture-coordinates | `vector3-array` | Similar to positions, except that the array stores texture coordinates for each triangle. |
| normals | `vector3-array` | Similar to positions, except that the array stores normal vectors for each triangle. |

## Constant Image

* Category: `image`
* Type: `constant`

An image that stores constant value. It can be a single real, a vector or a spectrum.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| value-type | `string` | Specifying what the stored constant represents. "raw": the value will be used directly without any conversion; "emr-linear-srgb": the value represents energy magnitudes in linear-SRGB; "ecf-linear-srgb": the value represents energy conserving coefficients in linear-SRGB. |
| value | `real` | A single constant value. |
| value | `vector3` | Vectorized constant value with three elements. |

## Image

* Category: `image`
* Type: `image`

A block of data.

## LDR Picture Image

* Category: `image`
* Type: `ldr-picture`

Low dynamic range images.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| image | `string` | Resource identifier for a LDR image file. |

## Picture Image

* Category: `image`
* Type: `picture`

This kind of image is similar to ordinary color image formats.

## Real Math Image

* Category: `image`
* Type: `real-math`

This image applies mathematical modifications on other images.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| math-op | `string` | The mathematical operation used. "multiply": multiplying a value to the target; "add": add a value to the target. |
| value | `real` | The value that is going to be applied to the target. How it will be applied depends on the math-op specified. |
| operand | `image` | The target image that is going to be operated on. |

## Area Source

* Category: `light-source`
* Type: `area`

This type of light source has a finite area. Energy is allowed to emit as long as the emitting source is within the area.

## Dome Source

* Category: `light-source`
* Type: `dome`

A large energy emitting source encompassing the whole scene.

> Creation:

(no input)

## Light Source

* Category: `light-source`
* Type: `light-source`

The source of all energy emitting entity in the scene.

## Model Source

* Category: `light-source`
* Type: `model`

A light source that emits energy from the surface of a geometry. A surface material model can also be given to describe its surface appearance.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| geometry | `geometry` | A geometry that defines the surface energy is going to emit from. |
| material | `material` | A material that describes this source's surface appearance. |
| emitted-radiance | `image` | An image that describes the emitted radiance across the surface. |
| emitted-radiance | `vector3` | Specify a constant emitted radiance across the surface in linear-SRGB. |
| emit-mode | `string` | Selects the side where the energy is allowed to emit. It can be "front" or "back". |

## Point Source

* Category: `light-source`
* Type: `point`

Power emitting source from a small but not infinitesimal region. Resembling a small light bulb.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| linear-srgb | `vector3` | The color of this light source in linear-SRGB. |
| watts | `real` | Energy emitted by this light source. |

## Rectangle Source

* Category: `light-source`
* Type: `rectangle`

This type of light emits energy from a rectangular shape. Note that energy is only allowed to emit from one side of the rectangle, not both sides.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| width | `real` | The width of the rectangle. |
| height | `real` | The height of the rectangle. |
| linear-srgb | `vector3` | The color of this light source in linear-SRGB. |
| watts | `real` | Energy emitted by this light source. |

## Sphere Source

* Category: `light-source`
* Type: `sphere`

This type of light emits energy from a spherical shape.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| radius | `real` | The radius of the sphere. |
| linear-srgb | `vector3` | The color of this light source in linear-SRGB. |
| watts | `real` | Energy emitted by this light source. |

## Abraded Opaque

* Category: `material`
* Type: `abraded-opaque`

Able to model surfaces ranging from nearly specular to extremely rough appearances.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| microsurface | `microsurface-info` | Describes the appearance model of surface microstructure. |
| fresnel | `conductive-interface-info` | Fresnel model for the surface microstructure. |
| distribution-model | `string` | Possible value are "trowbridge-reitz" (or equivalently "ggx", for both isotropic and anisotropic surface appearances), and "beckmann" (isotropic only). |
| roughness | `real` | Isotropic surface roughness in [0, 1], the material will appear to be smoother with smaller roughness value. |
| roughness-u | `real` | Similar to the roughness parameter, but is used for anisotropic surface appearances. This value controls the U component of surface roughness. |
| roughness-v | `real` | Similar to the roughness parameter, but is used for anisotropic surface appearances. This value controls the V component of surface roughness. |
| mapping | `string` | Method for transforming roughness value into an internal parameter "alpha". Possible values are "squared", "pbrt-v3", and "equaled". |
| fresnel-model | `string` | Controls the Fresnel model used. Possible values are "exact" and "schlick". |
| f0 | `vector3` | Surface reflectance on normal incidence. This value is expected to be given in linear-SRGB space. When this parameter is used, the underlying Fresnel model will be an approximated one (schlick) which is pretty popular in real-time graphics. |

## Abraded Translucent

* Category: `material`
* Type: `abraded-translucent`

Able to model translucent surfaces with variable roughnesses. Such as frosted glass.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| microsurface | `microsurface-info` | Describes the appearance model of surface microstructure. |
| fresnel | `dielectric-interface-info` | Fresnel model for the surface microstructure. |
| distribution-model | `string` | Possible value are "trowbridge-reitz" (or equivalently "ggx", for both isotropic and anisotropic surface appearances), and "beckmann" (isotropic only). |
| roughness | `real` | Isotropic surface roughness in [0, 1], the material will appear to be smoother with smaller roughness value. |
| roughness-u | `real` | Similar to the roughness parameter, but is used for anisotropic surface appearances. This value controls the U component of surface roughness. |
| roughness-v | `real` | Similar to the roughness parameter, but is used for anisotropic surface appearances. This value controls the V component of surface roughness. |
| mapping | `string` | Method for transforming roughness value into an internal parameter "alpha". Possible values are "squared", "pbrt-v3", and "equaled". |
| fresnel-model | `string` | Controls the Fresnel model used. Possible values are "exact" and "schlick". |
| ior-outer | `real` | The index of refraction outside of this material. |
| ior-inner | `real` | The index of refraction inside of this material. |

## Binary Mixed Surface

* Category: `material`
* Type: `binary-mixed-surface`

Mixing two surface materials in various ways.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| mode | `string` | Specifying how two materials are mixed. The only mode supported now is "lerp". |
| factor | `real` | A number in [0, 1] controlling the contribution from each material. |
| factor | `image` | An image controlling the contribution from each material. |
| material-0 | `material` | The material that participates the mixing process. |
| material-1 | `material` | The material that participates the mixing process. |

## Full Material

* Category: `material`
* Type: `full`

A material model that combines surface and volume properties.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| surface | `material` | A surface material. |
| interior | `material` | A volume material describing the inside of the surface. |
| exterior | `material` | A volume material describing the outside of the surface. |

## Ideal Substance

* Category: `material`
* Type: `ideal-substance`

Models a perfectly smooth surface with various physical properties.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| type | `string` | Specifying the physical behavior of the surface. Available types are "dielectric-reflector", "metallic-reflector", "transmitter", "absorber", and "dielectric". |
| ior-outer | `real` | The index of refraction outside of this material. |
| ior-inner | `real` | The index of refraction inside of this material. |
| f0-rgb | `vector3` | Surface reflectance on normal incidence. This value is expected to be given in linear-SRGB. When this parameter is used, the underlying Fresnel model will be an approximated one which is pretty popular in real-time graphics. |
| reflection-scale | `vector3` | A scaling factor for reflected energy. Note that this is only for artistic control and is not physically correct. This value is expected to be given in linear-SRGB. |
| transmission-scale | `vector3` | A scaling factor for transmitted energy. Note that this is only for artistic control and is not physically correct. This value is expected to be given in linear-SRGB. |

## Layered Surface

* Category: `material`
* Type: `layered-surface`

A material model for surfaces with matte look, such as chalk and moon.

> Creation:

(no input)

> Operation **add**:

Appends a layer to the bottom of the existing layers.

(no input)

> Operation **set**:

Creates a new surface layer and set it to a specified layer index. If there are N layers, the top one will have index 0 and the bottom one will have index N-1.

| Inputs | Types | Descriptions |
| --- | --- | --- |
| index | `integer` | The target layer index. |
| roughness | `real` | Isotropic surface roughness in [0, 1], the material will appear to be smoother with smaller roughness value. |
| ior-n | `vector3` | The real part of the layer's index of refraction in linear-SRGB. |
| ior-k | `vector3` | The imaginary part of the layer's index of refraction in linear-SRGB. |
| ior-n | `real` | The real part of the layer's index of refraction as a raw constant. |
| ior-k | `real` | The imaginary part of the layer's index of refraction as a raw constant. |
| depth | `real` | Thickness of the layer. |
| g | `real` | The g variable in Henyey-Greenstein phase function. |
| sigma-a | `real` | The volume absorption coefficient. |
| sigma-s | `real` | The volume scattering coefficient. |

## Material

* Category: `material`
* Type: `material`

Defines and models the appearance of scene elements.

## Matte Opaque

* Category: `material`
* Type: `matte-opaque`

A material model for surfaces with matte look, such as chalk and moon.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| albedo | `real` | A constant albedo in linear SRGB. |
| albedo | `vector3` | An albedo value in linear SRGB. |
| albedo | `image` | An image that will be used for describing albedo. |
| sigma-degrees | `real` | Roughness in standard deviation of surface orientation. |

## Camera

* Category: `camera`
* Type: `camera`

A camera for observing the scene.

## Perspective Camera

* Category: `camera`
* Type: `perspective`

For cameras that have perspective effect.

## Pinhole Camera

* Category: `camera`
* Type: `pinhole`

This type of camera is simply composed of a hole (which serves as its lens system) and a film. Images captured by this camera is similar to how a normal human perceives the world but with several simplifications.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| fov-degree | `real` | Field of view of this camera in degrees. |
| film-width-mm | `real` | Width of the film used by this camera in millimeters. |
| film-offset-mm | `real` | Distance from the film to the camera's lens. |
| position | `vector3` | Position of the camera. |
| rotation | `quaternion` | The orientation of the camera. |
| direction | `vector3` | Direction that this camera is looking at. |
| up-axis | `vector3` | The direction that this camera consider as upward. |
| yaw-degrees | `real` | Rotation of the camera around +y axis in [0, 360]. |
| pitch-degrees | `real` | The camera's declination from the horizon in [-90, 90]. |

## Thin Lens Camera

* Category: `camera`
* Type: `thin-lens`

As its name suggests, the lens system in this camera is assumed to be a single lens with negligible thickness. The biggest advantage of it is that depth of field effects are possible under this model.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| lens-radius-mm | `real` | Radius of the lens in millimeters. |
| focal-distance-mm | `real` | The distance in millimeters that the camera is focusing on. |
| fov-degree | `real` | Field of view of this camera in degrees. |
| film-width-mm | `real` | Width of the film used by this camera in millimeters. |
| film-offset-mm | `real` | Distance from the film to the camera's lens. |
| position | `vector3` | Position of the camera. |
| rotation | `quaternion` | The orientation of the camera. |
| direction | `vector3` | Direction that this camera is looking at. |
| up-axis | `vector3` | The direction that this camera consider as upward. |
| yaw-degrees | `real` | Rotation of the camera around +y axis in [0, 360]. |
| pitch-degrees | `real` | The camera's declination from the horizon in [-90, 90]. |

## Renderer

* Category: `renderer`
* Type: `renderer`

The main engine component for producing images.

## Attribute Renderer

* Category: `renderer`
* Type: `attribute`

This renderer produces various type of attributes which can be useful for compositing. The attributes are also known as AOVs (arbitrary output variables).

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| attribute | `string` | The attribute to render. |
| width | `integer` | Width of the film in pixels. |
| height | `integer` | Height of the film in pixels. |
| rect-x | `integer` | X coordinate of the lower-left corner of the film cropping window. |
| rect-y | `integer` | Y coordinate of the lower-left corner of the film cropping window. |
| rect-w | `integer` | Width of the film cropping window. |
| rect-h | `integer` | Height of the film cropping window. |

## Photon Map Renderer

* Category: `renderer`
* Type: `pm`

This renderer renders images by utilizing a precomputed photon map. Like all caching based methods, this render technique is biased; rendered result converges to ground truth in the limit.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| mode | `string` | Photon mapping mode. "vanilla": directly compute energy values from photon map, no fancy tricks applied; "progressive": progressively refine the rendered results; "stochastic-progressive": stochastic sampling technique is utilized for energy value computation. |
| num-photons | `integer` | Number of photons used. For progressive techniques, this value is for single pass. |
| radius | `real` | Contributing radius for each photon. For progressive techniques, this value is for setting up initial radius. |
| num-passes | `integer` | Number of passes performed by progressive techniques. |
| num-samples-per-pixel | `integer` | Number of samples per pixel. Higher values can resolve image aliasing, but can consume large amounts of memory. |
| width | `integer` | Width of the film in pixels. |
| height | `integer` | Height of the film in pixels. |
| rect-x | `integer` | X coordinate of the lower-left corner of the film cropping window. |
| rect-y | `integer` | Y coordinate of the lower-left corner of the film cropping window. |
| rect-w | `integer` | Width of the film cropping window. |
| rect-h | `integer` | Height of the film cropping window. |

## Adaptive Sampling Renderer

* Category: `renderer`
* Type: `adaptive-sampling`

This renderer renders images by path sampling techniques, but the samples will be concentrated on noisy regions. Normally, this renderer has better utilization of computational power.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| filter-name | `string` | The type of filter used by the film. "box": box filter, fairly sharp but can have obvious aliasing around edges; "gaussian": Gaussian filter, gives smooth results; "mitchell-netravali" or "mn": Mitchell-Netravali filter, smooth but remains sharp around edges; "blackman-harris" or "bh": Blackman-Harris filter, a good compromise between smoothness and sharpness. |
| estimator | `string` | The energy estimating component used by the renderer. "bvpt": backward path tracing; "bneept": backward path tracing with next event estimation. |
| width | `integer` | Width of the film in pixels. |
| height | `integer` | Height of the film in pixels. |
| rect-x | `integer` | X coordinate of the lower-left corner of the film cropping window. |
| rect-y | `integer` | Y coordinate of the lower-left corner of the film cropping window. |
| rect-w | `integer` | Width of the film cropping window. |
| rect-h | `integer` | Height of the film cropping window. |

## Equal Sampling Renderer

* Category: `renderer`
* Type: `equal-sampling`

This renderer renders images by path sampling techniques and distributes them equally. Typically, this means the rendering technique used is unbiased, and the the image converges as a whole.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| scheduler | `string` | Scheduler for rendering, affect the order of rendered regions. Possible values: bulk, stripe, grid, tile, spiral, spiral-grid. |
| block-width | `integer` | Desired width for render scheduling. |
| block-height | `integer` | Desired height for render scheduling. |
| filter-name | `string` | The type of filter used by the film. "box": box filter, fairly sharp but can have obvious aliasing around edges; "gaussian": Gaussian filter, gives smooth results; "mitchell-netravali" or "mn": Mitchell-Netravali filter, smooth but remains sharp around edges; "blackman-harris" or "bh": Blackman-Harris filter, a good compromise between smoothness and sharpness. |
| estimator | `string` | The energy estimating component used by the renderer. "bvpt": backward path tracing; "bneept": backward path tracing with next event estimation. |
| width | `integer` | Width of the film in pixels. |
| height | `integer` | Height of the film in pixels. |
| rect-x | `integer` | X coordinate of the lower-left corner of the film cropping window. |
| rect-y | `integer` | Y coordinate of the lower-left corner of the film cropping window. |
| rect-w | `integer` | Width of the film cropping window. |
| rect-h | `integer` | Height of the film cropping window. |

## Sampling Renderer

* Category: `renderer`
* Type: `sampling`



## Sample Generator

* Category: `sample-generator`
* Type: `sample-generator`

Engine component for generating sample values.

## Stratified Sample Generator

* Category: `sample-generator`
* Type: `stratified`

Generating samples based on engine provided dimensional hints.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| sample-amount | `integer` | Controls the number of sample batches that will be generated. |

## Uniform Random Sample Generator

* Category: `sample-generator`
* Type: `uniform-random`

Generating samples in a completely random fashion.

> Creation:

| Inputs | Types | Descriptions |
| --- | --- | --- |
| sample-amount | `integer` | Controls the number of sample batches that will be generated. |

## Data Structure: `conductive-interface-info`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| fresnel-model | `string` | Controls the Fresnel model used. Possible values are "exact" and "schlick". |
| f0 | `vector3` | Surface reflectance on normal incidence. This value is expected to be given in linear-SRGB space. When this parameter is used, the underlying Fresnel model will be an approximated one (schlick) which is pretty popular in real-time graphics. |

## Data Structure: `dielectric-interface-info`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| fresnel-model | `string` | Controls the Fresnel model used. Possible values are "exact" and "schlick". |
| ior-outer | `real` | The index of refraction outside of this material. |
| ior-inner | `real` | The index of refraction inside of this material. |

## Data Structure: `microsurface-info`

| Inputs | Types | Descriptions |
| --- | --- | --- |
| distribution-model | `string` | Possible value are "trowbridge-reitz" (or equivalently "ggx", for both isotropic and anisotropic surface appearances), and "beckmann" (isotropic only). |
| roughness | `real` | Isotropic surface roughness in [0, 1], the material will appear to be smoother with smaller roughness value. |
| roughness-u | `real` | Similar to the roughness parameter, but is used for anisotropic surface appearances. This value controls the U component of surface roughness. |
| roughness-v | `real` | Similar to the roughness parameter, but is used for anisotropic surface appearances. This value controls the V component of surface roughness. |
| mapping | `string` | Method for transforming roughness value into an internal parameter "alpha". Possible values are "squared", "pbrt-v3", and "equaled". |

