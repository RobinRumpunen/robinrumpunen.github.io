---
layout: page
menus: header
title: Engine
permalink: /engine
---

# Echo Engine
This is a brief overview of my ongoing personal engine, dubbed “Echo Engine”.
Down below you will see the current achievements of the project.
Try it out for yourself! Download binaries by pressing the button, no installation required.
<br>
<br>
<i> * I am aware </i> that there are some shadow related issues on certain AMD systems. I've tracked it down to be the cause of a shader, but at this moment i'm not sure how to fix it. Further investigation is needed.
<a class="robinBtn robinBtnDwnload" href="/assets/download/engine/EchoEngine_v0_33.zip" download> Win32 </a>



### An engine created from scratch by me.
It was started as a way for me to better understand what is truly going on
under the hood of a modern game engine. The languages used have been C++, GLSL (translated to SPIR-V), and a very small amount of batch script for task automation.
The project has been developed in my spare time and currently features 6 core systems and over 9000+ SLOC.
  * Vulkan backend renderer 
  * Image importing library
  * Math library 
  * Window and Input system (windows only)
  * Dynamic soft shadows
  * Physically based shading

And plenty of smaller systems such as:

  * Time, clocking system
  * Image manipulation, orientation
  * Shader compilation, batching

<i>Slight correction, </i>everything used except Assimp is written by me, more details further down.

### Vulkan renderer.
Fully written renderer backend with Vulkan.
No extensions part from Khrono’s “swapchains” has been enabled.
Allowing any platform supporting Vulkan to be compatible.

<img class="img-fluid" src="/assets/img/engine/FullRender.PNG" alt="Screenshot of the renderer">

### Dynamic soft shadows.
Variable soft shadow mapping has been implemented based on three render passes using 2 pipelines*.
1. Light-space pass storing depth (D).
2. X-direction filter storing a two component texture (D-filtered, D2-filtered).
3. Y-direction filtering based on the previous texture.
  * Currently only supporting one directional light.

<img class="img-fluid" src="/assets/img/engine/EngineSoftShadows.gif" alt="Variance Soft Shadows Gif">

### Physically based shading model.
PBS based on Epic Games’ approach, curtousy to LearnOpenGL.com for the great introduction.
Utilizing “Image Based Lighting” provided via preprocessed cubemap textures used to generate
radiance and irradiance textures.

<img class="img-fluid" src="/assets/img/engine/PBS_Model.PNG" alt="Physically based shading model">

### Image importing library.
Fully written image importing library supporting KTX v1.1 and TGA file formats.

Supporting various features:
  * 8, 16, 32 bits/channel data
  * Cubemaps
  * Mipping
  * Texture Arrays
  * Meta data (e.g. internal formats)

Smaller tools:
  * Mirroring
  * Image manipulation (e.g. orientation)

### Math library.
The engine uses a custom math library written from scratch.
Starting of as a way for me to exercise and read up on my mathematical knowledge
this has become the foundation of this journey. It has been a great learning
experience but also streamlining the code without introducing 3rd party overhead.
  * Vectors
  * Matrices
  * Trigonometric functions
  * Normalizing, dot product
  * View, projection matrices

### Window & input handling. 
Input handling has been configured to consists of states, keys and ‘actions’.
On startup the system registers key-codes to actions*.
Each frame the Window might trigger an input update, the input handler then
goes through the registered keys and updates their state;
Pressed, Released (max one frame), or Inactive, as well as toggled.
Any system can then query the input handler and create logic based on an action
and a state with the following interface:

```ruby
language: C++

  if (_inputInfo.ActionToggledState("Control") == false || timer_playerCinema_lerp.GetPercentage() < 1.0f)
  {
    [...]
  }

  if (_inputInfo.ActionState("MoveRight") == KeyState::Pressed)
  {
    [...]
  }
```

<img class="img-fluid" src="/assets/img/engine/EngineInput.gif" alt="Gif of input resistration inside the engine.">

### Model loading.
Model importing is provided by the 3rd party library Assimp.
<a href="https://github.com/assimp/assimp">https://github.com/assimp/assimp</a>

### Contribution?
As this is an educational project developed during my spare time, contribution wont be enabled.
If there is interest in seeing source code, I can look into publishing it. 😀

Thanks for reading!

// Robin Rumpunen