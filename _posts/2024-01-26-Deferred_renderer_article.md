---
title: "Article on deferred renderer with PBR on PS5"
categories: [Articles]
image:
  path: assets/post_data/deferred_renderer/deferred.png
  alt: 3 thousand lights illuminating the scene
descrition: Details of deferred rendering pipeline
---


## What is this all about?
This was the project I chose as a self-study for my university. My primary focus was looking for technical challenges. It was crucial for me to comprehend how things work and the way I can control them via provided API. Before I experienced only OpenGL, which is not deep enough to operate on every aspect of GPU functionality.

My goal was to understand how professionals squeeze maximum performance from diverse hardware, what considerations specialists have when designing simple light-object interactions, and why some renderers achieve realistic graphics at an acceptable framerate while others struggle with output of basic models. To pursue this goal, I needed a project that was both simple and challenging enough.

I settled on a deferred rendering pipeline. This blog post will delve into the main technical details of the project and share the insights I gained from it.

## Philosophy of deferred
When selecting the project, I carefully analyzed the overall difficulty in achieving the final outcome. While analysing, I found that the fundamentals of deferred pipeline are commonly used in modern games. This technique leverages memory to optimize light calculations. Modern GPUs provide ample memory to support such methods, even for 4K gameplay at a nice framerate. The core concept of the algorithm is to separate the entire rendering process into 3 passes – geometry, lighting and final. Additionally, I incorporated a transparent and direct passes into the pipeline.

## The pipeline

### Geometry pass
In the geometry pass, we render world geometry into multiple render targets. This results in having several images with all the information for later usage. Essentially, every pixel stores the information it requires. This pass enables us to overwrite all the initial values at the beginning of the frame, saving time from all wasteful light calculations.

![Render targets with necessary information](../assets/post_data/deferred_renderer/Picture1.jpg)
*As a result, I store roughness, metallic, normal and diffuse data per pixel*

The rendered information is stored in so called **Geometry Buffers** *(later GBuffers)*. All pixel data is passed to GPU memory as full-screen textures, where every pixel knows its corresponding values. 
 
### Lighting pass
One more trick to save performance is to pass lights as spheres. In the vertex shaders we calculate vertex data as if these spheres genuinely exist in our virtual world. Subsequently, in the fragment shader, we use this vertex data to obtain screen coordinates, which are then utilized as UV input for GBuffers.

This approach ensures that we have all the essential information required to calculate light at a specific pixel. The calculated data is blended with one of the buffers called **Light Accumulation**. This principle significantly accelerates light calculations, as we only operate on pixels affected by light.

When I was working on my first renderer, I could not exceed the limit of 10 lights, regardless of their sizes. This was because every light operation impacted every pixel on the screen. However, this case prevents numerous wasteful calculations.

![Accumulation buffer after lighting pass](../assets/post_data/deferred_renderer/Picture2.png)
*For now, that is how the light accumulation buffer will look like*

### Direct light pass (personal addition)
In virtual worlds, we encounter various types of light, with point and direct lights being the most common. Direct light sources influence the entire scene, illuminating everything from the same angle.

In this scenario, there is no need for optimization, so we straightforwardly traverse every pixel and assess the resulting color.

![Updated accumulation buffer with direct light source information](../assets/post_data/deferred_renderer/Picture3.png)
*After filling the scene with one direct light, that what we will see*

### Transparency pass (personal addition)
By default, transparency is not handled in this pipeline (later will be discussed why). The way I implemented is pretty simple – I project model onto the screen and multiply the opacity coefficient with a base color texture. Nothing else.
   
![Updated accumulation buffer with transparent objects in the scene](../assets/post_data/deferred_renderer/Picture4.png)
*Temporal outcome with some transparent objects drawn*

### Final pass
In this stage, we might perform some post-process (but I do not), then finally render the image on the screen. Typically, we just extract the pixel data from Light accumulation buffer and display it on the screen.

![Final outcome](../assets/post_data/deferred_renderer/Picture5.png)
*I added an ambient light to the final outcome*

## Weighing 
As a result, we see improvements in light interactions with the world. Additionally, smaller lights incur smaller performance costs. However, this comes at the expense of increased memory usage. Thankfully nowadays, VRAM / SMEM is not such a big deal. Despite its optimizations, the deferred renderer faces two common disadvantages, which programmers must overcome with distinct solutions:

- **Anti-Aliasing**\
In the geometry buffers, only precise data is stored, interpolation in this algorithm is not possible. Otherwise, values for light computations will lead to artifacts.

- **Transparent surfaces**\
GBuffers store only the foreground of what you see, and if new data is closer to the camera than the older one, it will rewrite all the values.

There are also other issues stemming from the separation geometry from lighting, but they will not be covered in my blog.

## Impressions
The challenges I overcame, the knowledge I gained, the feedback I have received… were enormous. This project was solely mine; no one else on my course was working on the same thing. Other students have been working on their own ideas and passions. As a result, many aspects of my project were unique.

I am very pleased with the work I have accomplished. Moreover, the fact - that I have completed my initial plan and was not adjusting anything - brings me pleasure for time-planning skill.

Thanks for reading this. GG

![BUas logo](../assets/post_data/deferred_renderer/buas-logo.png)
*This project was part of university course*