---
layout: page
menus: header
title: Engine
permalink: /engine
---

# Echo Engine
This is a brief overview of my ongoing personal engine, dubbed “Echo Engine”.
Down below you will see the current achievements of the project.

Try it out for yourself!
Download binaries here:
<p class="btn_dwnload"><a href="/download/XXX">[Win64]</a></p>
<p class="btn_dwnload"><a href="/download/XXX">[Win32]</a></p>
<p class="btn_dwnload"><a href="/download/XXX">[OSX]</a></p>
<p class="btn_dwnload"><a href="/download/XXX">[Linux]</a></p>

### Echo engine is a personal engine created from scratch* by me.
It was started as a way for me to better understand what is truly going on
under the hood of a modern mid sized game engine.
- Development is still a work in progress.
 * Everything used except Assimp is written by me, more details further down.

### Vulkan renderer.
Fully written renderer backend with Vulkan.
No extensions part from Khrono’s “swapchains” has been enabled.
Allowing any platform supporting Vulkan to be compatible.

![deploy using travis](/assets/img/engine/VKRenderer.png){:class="img-fluid"}

### Dynamic soft shadows.
Variable soft shadow mapping has been implemented based on three passes*.
1. Light-space pass storing depth (D).
2. X-direction filter storing a two component texture (D-filtered, D2-filtered).
3. Y-direction filtering based on the previous texture.
 * Currently only supporting one light, however work has started on supporting
   multiple lights.

![deploy using travis](/assets/img/engine/Shadow.gif){:class="img-fluid"}

### Physically based shading model.
PBS based on Epic Games’ approach.
Utilizing “Image Based Lighting” provided via cubemap textures used to generate
radiance and irradiance textures.

![deploy using travis](/assets/img/engine/PBS_Model.png){:class="img-fluid"}

### Image importing library.
Fully written image importing library supporting KTX v1.1 and TGA file formats.
The KTX file format allows for storing mips, meta data (e.g. internal formats),
cubemaps, texture arrays, and beyond 8 bit/channel data. Also included are
image manipulation tools such as mirroring and image orientation.

### Math library
The engine uses a custom math library written from scratch.
Starting of as a way for me to exercise and read up on my mathematical knowledge
this has become the foundation of this journey. It has been a great learning
experience but also streamlining the code without introducing 3rd party overhead.

### Window & input handling. 
Input handling has been configured to consists of states, keys and ‘actions’.
On startup the system registers key-codes to actions*.
Each frame the Window might trigger an input update, the input handler then
goes through the registered keys and updates their state;
Pressed, Released (max one frame), or Inactive.
Any system can then query the input handler and create logic based on an action
and a state.

 * Work has started on an XML-style key configuration file, mapping actions to
   key-codes enabling user customization.
Currently only supported platform is windows, but work has been put through to
change between system configurations when alternatives have been implemented.

![deploy using travis](/assets/img/engine/WindowInput.gif){:class="img-fluid"}

### Model loading.
Currently provided via 3rd party Assimp file loading library.
Used to import model data, but the plan is to create a custom system.
https://github.com/assimp/assimp

### Contribution?
Feel free to take a look inside the source code
Issue requests are open, contribute via Github!
