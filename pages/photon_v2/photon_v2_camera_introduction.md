---
title: Introduction
keywords: 
last_updated: September 26, 2018
summary: "Camera plays an important role in the scene: it captures light and record an image on its film--so you can see the virtual world which just got rendered."
sidebar: photon_v2_sidebar
permalink: photon_v2_camera_introduction.html
---

Camera plays an important role in the scene: it captures light and record an image on its film--so you can see the virtual world which just got rendered. Photon currently supports two types of perspective camera: pinhole and thin lens. A pinhole camera is simply composed of a hole (which serves as its lens system) and a film. Images captured by this camera is similar to how a normal human perceives the world but with several simplifications. Due to its simplicity, it is widely adopted in computer graphics industry.

{% include image_gallery.html file="photon_v2/pinhole.png" alt="" caption="Image rendered by a pinhole camera. Notice the sharpness in foreground and background; there is no difference and it appears to be in focus everywhere." width="90%" %}

For thin lens camera, as its name suggests, the lens system in this camera is assumed to be a single lens with negligible thickness. The biggest advantage of it is that depth of field effects are possible under this model. In the following render, depth of field is achieved by a 72 mm lens focusing on the first metallic monkey.

{% include image_gallery.html file="photon_v2/thin_lens.png" alt="" caption="Image rendered by a thin-lens camera. Notice the depth of field effect." width="90%" %}

Types of camera that are currently supported by Photon:

* Pinhole
* Thin Lens
* Environmental (360)
* Energy Measurement (radiant flux)
