---
layout: post
title: 'The journey to Vulkan: Goals'
date: 2023-08-19 21:09 +0200
categories: [Graphics, Vulkan]
tags: [Graphics, Vulkan, Goals]
toc: true
img_path: "/assets/img/Posts/The journey to Vulkan"
image: 
    path: "Vulkan_Logo.png"
---

Currently, the world is full of graphics APIs: *DirectX*, *OpenGL*, *WebGL*, *Metal*... While some of them have very specific use cases (like WebGL), most of them acomplish the same purpose: give your application a way to comunicate with the GPU to render images (or make some compute task, but there's better alternatives to that). 

{: .prompt-info }

> There isn't anything bad or weird into using graphics APIs to do compute. In fact, *compute shaders* are made to do this and some APIs, like *Vulkan*, are designed without having the rendering as a mandatory task. But if you only need a way to comunicate with the GPU to make some compute task, you will be better suited with alternatives like [*OpenCL*](https://www.khronos.org/opencl/), [CUDA](https://developer.nvidia.com/cuda-toolkit) or [*ROCm*](https://www.amd.com/es/graphics/servers-solutions-rocm).

During my studies, I have learned OpenGL, a open source API that has been *DirectX* main competitor for years (at least, in pc). It's maybe one of the easiers graphic API to learn out there, with a lot of learning resources available but it **has a problem**. It's an API 20 years old and, while it has been updated, it has some design aspects that makes quite difficult achiving a good CPU multicore usage. The lastest update includes some API new functions to *Achieve Zero Driver Overhead* ([AZDO](https://www.khronos.org/assets/uploads/developers/library/2014-gdc/Khronos-OpenGL-Efficiency-GDC-Mar14.pdf)), necesary to make some *GPU driven rendering* and there's some [propietary Nvidia extensions](https://on-demand.gputechconf.com/siggraph/2015/presentation/SIG1512-Tristan-Lorach.pdf) that adds some lower level concepts to OpenGL in order to achieve less driver overhead like newers APIs. 

All of this, in addition that *Khronos group* abandoned *OpenGL* in favour of *Vulkan*, wide support of *Vulkan* and that practically all game engines are transitioning to newer APIs, made me think that I should learn it.

The main point of this post is to write down all the decisions I have already made about this journey and the main goals of it. 

## Programming language

One of the preliminary of any software project is which technology stack/language is going to use. In this case, one part of it is already told: *Vulkan*. But the language question still in the air. Here we have three options: 

### C

The most classical one. The Vulkan API is written in C, so choose this language could be a good option. In fact, there's some people that recommends it over C++ because it frees you from a lot of OOP performance problems in real time applications. But, on the other hand, it gives you very little as a language. For example, if you need any data structure, either you write it or use a someone's implementation. Due to this kind of things, I don't feel like C is an option that suits me.

### Rust

What can be the natural succesor of C/C++. It offers similar kind of performance but with safety by default. I have little experience with Rust but I like a lot some of the improvements it has like *const* by default, basic-types specifiers or crates system, as well as the explanation the compiler gives you for each error. 

However, having to learn practically from beginning two very complex things can be too much. 

### C++

The last option and one of the most choosen one. The most controversial aspect of this option could be all the OOP overhead mentioned previously. But using objects everywhere is not mandatory in C++. In fact, you can write only C code in C++, so you can achieve in C++ whatever you could achieve in C. 

This is the language I have most experience with and will be the choosen for this project. I will try to use objects only when it makes sense in the context of the application, in hope of achieve a *Data Oriented Design* (DOD).

## IDE

Visual Studio. That's it. There's others alternatives like *CLion* or *10XEditor*, but neither of them are free or offers a huge advantage over VS. 

On the other hand, one thing that will differ from my previous project is the build system I'm gonna use. Instead of Visual Studio native system, I will use *Cmake*. I have never understood it (I find Visual Studio system simplier), but practically everyone in the industry uses it, so i'll give it a try in a bigger project. 

## Learning resources

There's fewer learning resources for *Vulkan* than for *OpenGL*. But, on the other hand, they focus in newer techniques and it's easier to find resources for things like GPU driven rendering. 

I have already done some *workshops* oriented to learn the basics of *Vulkan*, like the one from [Johannes Unterguggenberger](https://www.cg.tuwien.ac.at/staff/JohannesUnterguggenberger.html), [VulkanWorkshop](https://github.com/cg-tuwien/VulkanWorkshop). This one is pretty good in teaching the very basics till part 4, where explanation videos aren't available and you get lost a lot of the time in the inmensity of code. 

So, as i don't thing that i trully dominates the basics, i'll start from scratch with [vkguide.dev](https://vkguide.dev/) adapting the concepts there explained to my own custom implementation (which could not be a good idea but...). This page is less dense than others tutorials like [vulkan-tutorial](https://vulkan-tutorial.com/) or the [Khronos' official guide](https://github.com/KhronosGroup/Vulkan-Guide) while explain all the basic concepts you need. In any case i need a more detailed explaination, i can always refer to these others resources. 

The nice part of the tutorial choosen is that it covers from the very basics to some more advances topics like multithreading the renderer or GPU driven rendering, some topics i'm willing to learn.

In addition to the previous tutorials, there's another pair of learning source in form of samples: [SaschaWillems/Vulkan](https://github.com/SaschaWillems/Vulkan) and [KhronosGroup/Vulkan-Samples](https://github.com/KhronosGroup/Vulkan-Samples).

## Libraries

I would like to keep low the number of dependencies, so i will mostly use indispensable  ones:

- **GLFW**: Needed to create the window and to access input devices. Quite popular, stable and I already have experience with it.

- **GLM**: Based on GLSL math specifications, it is intended to use in *OpenGL*, but as *Vulkan* uses GLSL, there's no problem in using it. 

- **Dear ImGUI**: There isn't discusion here. 

- **Vulkan Memory Allocator**: Not mandatory but quite convenient to suffer a little less with *Vulkan* memory management.

- **VK Bootstrap**: The most dispensable one. It makes an abstract layer over all the boilerplate that Vulkan has on initialization. I have already suffer part of it while doing the mentioned workshop, so I prefer keeping it away for now. 

## Goals

- [ ]  Build a simple vulkan renderer, capable of render 3D objects using simple techniques.

- [ ]  Learn about the advantages Vulkan offers to multithreading and implement it in the renderer.

- [ ]  Explore ECS paradigm and advantages that it could have in having a DOD.

- [ ]  Study about *Mesh shader* use cases and try to include it in the renderer. 

- [ ]  Implements "recent" lighting and materials techniques such as PBR or IBL.

- [ ]  Take advantage of *compute shaders* to apply optimizations like culling.

- [ ]  Switch to *GPU driven rendering* at some point.

- [ ]  Use the renderer built to acomplish other projects.
  
  - [ ]  Terrain with grass rendering.
  
  - [ ]  Particle system simulations.
