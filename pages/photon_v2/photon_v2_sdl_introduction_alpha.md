---
title: Scene Description Language (alpha)
keywords: 
last_updated: September 15, 2019
summary: "Introducing the basics about scene description in Photon."
sidebar: photon_v2_sidebar
permalink: photon_v2_sdl_introduction_alpha.html
---

{% include warning.html content="Documentation deprecated. Please visit the [project website](https://tzuchieh.github.io/Photon-v2-site/engine_docs/v2.0.0-beta/Photon/html/index.html) for up-to-date content." %}

# Introduction

Here, you will learn about the scene description language used in Photon (sometimes we call it PSDL for convenience, which stands for **P**hoton **S**cene **D**escription **L**anguage). It is a special format created for storing scene data as well as controlling the behavior of the render engine. Currently we have Python and Java APIs for users to programmatically build scene descriptions, and a documentation for engine features exposed as PSDL can be found [here](photon_v2_sdl_documentation.html).

## Language Basics

A hello-world scene rendered by Photon looks like this

{% include image_gallery.html file="photon_v2/sdl_hello_world_scene.jpg" alt="" caption="Rendered hello-world scene" width="60%" %}

This image can be generated by feeding the following descriptions into Photon:

```csharp
## camera(pinhole) [real fov-degree 30] [vector3 position "0 6 40"] [vector3 direction "0 0 -1"] [vector3 up-axis "0 1 0"]
## sample-generator(stratified) [integer sample-amount 10]
## renderer(equal-sampling) [integer width 512][integer height 512][string filter-name gaussian][string estimator bneept]

-> geometry(rectangle) @plane [real width 15] [real height 15]
-> geometry(sphere)    @ball  [real radius 2.5]

-> material(matte-opaque) @white [vector3 albedo "0.9 0.9 0.9"]

-> actor(model) @ground [geometry geometry @plane] [material material @white]
-> actor(model) rotate(@ground) [vector3 axis "1 0 0"] [real degree -90]
-> actor(model) scale(@ground) [vector3 factor "10 10 10"]

-> actor(model) @object [geometry geometry @ball]  [material material @white]
-> actor(model) translate(@object) [vector3 factor "0 2.5 0"]

-> light-source(rectangle) @areaSource [vector3 linear-srgb "1 1 0.8"] [real watts 400] [real width 2] [real height 2]
-> actor(light) @topLight [light-source light-source @areaSource]
-> actor(light) translate(@topLight) [vector3 factor "0 10 0"]
-> actor(light) rotate(@topLight) [vector3 axis "1 0 0"] [real degree 90]
```

{% include note.html content="More example scenes can be found in the \"scenes\" folder in the GitHub repository." %}

The scene description can be stored into a text file (.p2 filename extension) and loaded by Photon for rendering. PSDL is a command-like system and the commands can be roughly categorized into 2 parts: **core** and **world**. Commands are normally structured in the following way (without the angle brackets):

`<command-prefix>` `<type-category>`(`<type-name>`) `<name>` `<clauses>`

where `<command-prefix>` is the part that you can distinguish between core and world categories.

> Core commands start with prefix `##`. For example, to create a pinhole camera, we write:

```csharp
## camera(pinhole) [real fov-degree 30] [vector3 position "0 0 0"] [vector3 direction "0 0 -1"]
```

> World commands start with prefix `->`. To create a unit-sized rectangle, we may write:

```csharp
-> geometry(rectangle) @plane [real width 1] [real height 1]
```

Note that in most cases, core commands do not have the `<name>` part.

> To disable a command or write some comment, simply put two slashes before the line:

```csharp
// These commands are being disabled
//## camera(pinhole) [real fov-degree 30] [vector3 position "0 0 0"] [vector3 direction "0 0 -1"]
//-> geometry(rectangle) @plane [real width 1] [real height 1]
```

{% include important.html content="You must start a command with either \"##\" or \"->\", and at least a white space after them." %}

In the next sections, we will focus on the remaining structures of PSDL commands.

## Type Category

`<command-prefix>` **`<type-category>`**(`<type-name>`) `<name>` `<clauses>`

Describes the category to which current command belongs, e.g., the command that creates a camera states that its category is **camera** in its type category section.

## Type Name

`<command-prefix>` `<type-category>`(**`<type-name>`**) `<name>` `<clauses>`

Type names generally **add details** to the type category. Again, in the example of creating a camera, we know that we are now creating a **pinhole** camera from the command fragment `camera(pinhole)`.

## Data Name

`<command-prefix>` `<type-category>`(`<type-name>`) **`<name>`** `<clauses>`

```csharp
// Data names in PSDL must start with "@". In this example, we created a sphere named "@ball".
-> geometry(sphere) @ball [real radius 2]
```

A command usually represents an element from the scene. As you may notice from the examples, core commands typically associate with singleton objects for a scene, e.g., camera, film, or sampler. Giving singleton objects a name seems to be redundant, so this section should remain empty for core commands. For world commands, we can assign them a name here.

## Clauses

`<command-prefix>` `<type-category>`(`<type-name>`) `<name>` **`<clauses>`**

**Clause** is a structure that stores parameters for a command. It has the following form:

`[<type-category> <parameter-name> <values>]`

It is worth pointing out that a `<parameter-name>` does not need to start with `@`. The `<values>` section can have many forms such as numerical values (you have already seen that), arrays, and even stand-alone data files (we call them **PSDL Resource Identifier**). Details of this section will be introduced in later part of the guide.

TODO: reference & struct types

{% include note.html content="You can place multiple clauses one after another in case of multiple parameters are required." %}

```csharp
// By writing these, we can have a ball and a ground in the scene!
-> geometry(sphere)    @ball   [real radius 0.5]
-> geometry(rectangle) @ground [real width 100] [real height 100]
```

With PSDL, you can create almost all kinds of objects the rendering system has to offer. In later sections, we will see that it is also possible to perform actions via PSDL.

{% include tip.html content="Go back and check the hello-world scene description again. You should be able to understand most of the lines now." %}

## Operations

TODO: introduce PSDL executors

## Appendix

 [Full documentation of PSDL commands](photon_v2_sdl_documentation.html).
