---
title: "The current state of Photon"
published: true
toc: true
permalink: blog_current_state_of_photon.html
summary: "What has changed, what is new, and what to expect in the future."
tags: [graphics]
---

If you have not read the [previous post about Photon](blog_photon_technical_update.html), I highly recommend to have a look at it. Though that post dates back to 2019, it will give you a rough idea about the history of the project as well as its design. In case you are not familiar to Photon, it is a program that generates 3D images (like those 3D games), except that we spend more time on a single frame and try to compute physically correct lighting for the scene. Photon renderer is currently in version 2.0.0-alpha.

{% include image_custom.html file="blog/2023-10-10-blog_current_state_of_photon/bneept_halton_8192spp.png" alt="image teaser" caption="Light bulbs rendered by Photon (modeled by sadaj72, materials adapted for use in Photon)." width="100%" %}

## What has changed?

Photon has undergone several design overhaul over the past few years. The most exciting part from a user perspective would definitely be new features. Almost all aspects to a 3D renderer are updated--we now have new material models, new lighting system, new geometry processing stages, and architectural refactors on the main rendering infrastructure. An updated PSDL (Photon Scene Description Language) documentation can also be found [here](photon_v2_sdl_documentation.html).

Our scene description language has been redesigned. Previously, it was embedded in code (as XML comments) and requires a separate script written in Python to parse and generate (similar to Qt and Unreal in some way). Loading and saving resources forces the programmer to write C++ code that pretty much code-duplicate the interface specified in XML. That approach is flexible (we can write arbitrary logics in the I/O code), however the code duplication bothers me every time I add/remove SDL parameters. The new system is basically a full-fledged reflection system that not only tackles all code duplications, we no longer need to maintain a separate program to parse and extract SDL interface from C++ code. We demonstrate the improvement in coding experience by comparing an old SDL executor definition to the new one:

* The old SDL interface need XML based binding description
    ```xml
    <SDL_interface>
        <category>  actor       </category>
        <type_name> physical    </type_name>
        <extend>    actor.actor </extend>

        <name> Physical Actor </name>
        <description>
            An actor that is visible and can be transformed.
        </description>

        <command type="executor" name="translate">
            <description>
                Moves the actor away from the original location with a specified amount.
            </description>
            <input name="factor" type="vector3">
                <description>The amount to move in each axis.</description>
            </input>
        </command>
        <!-- more definitions... -->
    </SDL_interface>
    ```
    and corresponding C++ code (showing only the loading part)
    ```cpp
    ExitStatus PhysicalActor::ciTranslate(
        const std::shared_ptr<PhysicalActor>& targetResource,
        const InputPacket& packet)
    {
        InputPrototype translationInput;
        translationInput.addVector3("factor");

        if(packet.isPrototypeMatched(translationInput))
        {
            const Vector3R translation = packet.getVector3("factor");
            targetResource->translate(translation);
            return ExitStatus::SUCCESS();
        }
        else
        {
            return ExitStatus::BAD_INPUT("requiring a vector3 factor");
        }
    }
    ```
* Whereas the new SDL interface can do more by writing less
    ```cpp
    struct SdlTranslate
    {
        math::Vector3R amount;

        void operator () (PhysicalActor& actor) const
        {
            actor.translate(amount);
        }

        PH_DEFINE_SDL_FUNCTION(TSdlMethod<SdlTranslate, PhysicalActor>)
        {
            FunctionType func("translate");
            func.description("Moves the actor away from the original location with a specified amount.");

            TSdlVector3<OwnerType> amount("amount", &OwnerType::amount);
            amount.description("The amount to move on each axis.");
            amount.defaultTo({0, 0, 0});
            func.addParam(amount);

            return func;
        }
    };

    PH_DEFINE_SDL_CLASS(TSdlOwnerClass<PhysicalActor>)
	{
		ClassType clazz("physical");
		clazz.docName("Physical Actor");
		clazz.description("An actor that is visible and can be transformed.");
		clazz.baseOn<Actor>();

		clazz.addFunction<SdlTranslate>();
        // more definitions...
		return clazz;
	}
    ```

PSDL now has a more "programming language" like syntax:

```csharp
// This is how we create a rectangle shape now
geometry(rectangle) @wall = [real width 1] [real height 1];
```

There are some points to note:

* The new PSDL syntax divides a command to LHS and RHS parts by the assignment operator. We call the LHS part *command header* and RHS part *SDL data packet*.
* Command header now supports a larger set of types, and is extensible by inheriting from a set of classes.
* If possible, reference type can now be deduced automatically.
* SDL data packet, as its name suggests, carries data for the command. In the above example, it is basically an aggregate of SDL value clauses (see `SdlInlinePacketInterface`).
* To add custom data packet, simply inherit from `SdlDataPacketInterface` and provide the implementation required.

Thanks to the new SDL interface, Python bindings to PSDL can be more easily generated. Our Blender addon *Photon Blend* is now updated more often and render preview feature (F12) has been integrated so scenes can iterate faster:

{% include image_custom.html file="blog/2023-10-10-blog_current_state_of_photon/blender_preview.gif" alt="image preview" caption="Previewing intermediate render result in Blender is accomplished by transferring pixel data over sockets." width="100%" %}

Last but not least, the data cooking process is now more standardized and continued to evolve. I am slowly shaping the process to allow greater potential for parallelism. When finished, time-to-first-pixel performance should have visible improvement.

## What is new?

We now have a new C++ based GUI program for rendering. This time it is much more ambitious then the previous Java based *Photon Studio*. 

{% include image_custom.html file="blog/2023-10-10-blog_current_state_of_photon/photon_editor.png" alt="editor teaser" caption="A sneak peek at the new editor program." width="100%" %}

Currently, it has all the functionalities Photon Studio had. As you can already guess from the above image, we are going to support basic scene manipulation tools directly within the editor program. Asset creation (e.g., material, geometry, animation, etc.) can be done in Blender; however, some novel material models or rendering algorithms cannot be easily managed from any DCC tools. By building our own editor, we can reduce one more level of indirection and aid data visualization in a more straightforward way. One example is the sampling tool we have, which let you visualize random number and sample generation from the engine:

{% include image_custom.html file="blog/2023-10-10-blog_current_state_of_photon/photon_editor_tool.png" alt="editor tool" caption="Showing first two dimensions of Halton samples with PCG64-DXSM generator." width="100%" %}

Advanced color space management has been integrated into Photon. Inspired by `std::chrono`, a set of color utilities are implemented and new color space can be added by providing a couple of basic definitions (and color space casting is automatic supported). Different spectral representations can also be added as a generalized "color space", with automatic spectral up-sampling and down-sampling from/to tristimulus color spaces. These infrastructure allow us to take input data and render in any color space or spectral representation. Much of this changes are motivated by seeing the post written by Simon: [sRGB/ACEScg Luminance Comparison](http://simonstechblog.blogspot.com/2020/09/srgbacescg-luminance-comparison.html), as I like the "color bleeding" effect of ACEScg more.

We also added better logging, profiling (by integrating [Tracy](https://github.com/wolfpld/tracy)), [concurrency helpers](https://github.com/TzuChieh/Photon-v2/tree/3d8e39c2b22113574089ffdb6e8a325e18af7324/Engine/Source/Utility/Concurrent), filesystem utilities, etc. Most new features are code based and cannot be easily showed here. Nevertheless, the whole project is build on top of them and new modules can be added easily and with better quality then before.

## What to expect?


