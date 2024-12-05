---
title: "Article on dynamic wetness"
categories: [Articles]
image:
  path: assets/post_data/dynamic_wetness/wetnessing.png
  alt: Screen mask and wetness functions applied
description: Article explaining how I made a responsive screen-space wetness
---

## What is this all about?
This project is a graphics concept for a future team game with plaguecore-decayed visuals and slow-paced gameplay. To contribute, I created a demo featuring dynamic rain particles, a material function for wet effects, and a screen-space wetness mask to show wet spots from rain drops. This required deep research into Unreal's Niagara system, materials, and rendering pipeline.

*In this article, I will explain what this effect consists of:*
<video class="w-100" controls>
  <source src="https://github.com/user-attachments/assets/ff1e54f3-59c8-4df7-8bfe-ccd45236d138" type="video/mp4">
</video>



## Key algorithm steps

1. **Creating a mask**\
All the wet spots from rain drops are rendered into a single texture as instanced primitives (in my particular case the primitive is a plane).

2. **Applying wetness mask**\
When material shader contributes to the pixel, it takes into account the wetness value from a screen mask, so that the surface can be wet.



## Niagara particles

The particles in the project are slightly modified ones from the [Ghislain Girardot's tutorial](https://www.youtube.com/watch?v=7stKYkRYmu0). Particles have complex and physicly accurate behavior that includes 3 different states:

1. **Sticky**\
The particle *(a rain drop)* sticks to the surface. It will follow the gravity and try to fall down, however, depending on the velocity and particle mass it will either stay sticky and follow the surface, or come off the and fall down.

2. **Fall**\
A free fall state.

3. **Splash**\
When the particle fas falling and reached the surface, it switches to a splash state. This state visualized the splash, then killing the particle.\
When the particle enters this state it contributes to the screen mask.



## Material function

A universal material function, that can make any material look wet by tweaking wetness values. The function in the project is based on [Ben Cloward's tutorial](https://www.youtube.com/watch?v=fYGOZYST-oQ).

### Real life observations

Through observation, I noted how materials react differently to water:

- **Absorbent Materials** *(e.g., towel, carpet, paper, stone)*:\
Water darkens the base color, making the surface look soaked.
- **Non-Absorbent Materials** *(e.g., glass, metal, plastic)*:\
Water accumulates on the surface, increasing the specular highlights.

### Node graph explanation

![Wetness function photo](/assets/post_data/dynamic_wetness/wetness-function.png)

## Conclusion

It was all about learning how to use Niagara, materials, and researching rendering pipeline in Unreal. I am more then happy with the result, especially being able to make some a cool graphics feature in Unreal, an engine already known for its outstanding graphical capabilities.

> There is a [link to the GitHub repo](https://github.com/SmailikHappy/GraphicsConcepting) with this Unreal project.
{: .prompt-tip}

Thanks for reading this article. GG

![BUas logo](../assets/post_data/deferred_renderer/buas-logo.png)
*The project has been undertaken as a university assignment.*