---
title: "Dynamic wetness"
categories: [Articles]
description: Article explaining how I made a reponsive screen-space wetness
---

## What is this all about?
This project is a graphics concept for a future team-developed game. Initially, team decided to have a plaguecore-decayed visuals with slow-paced gameplay. As a graphics programmer, I thought on the way to contribute to this artistic idea.

As a result, I delivered a demo with dynamic rain particles, material function that can make any material look wet and a screen space wetness mask that utilizes the material function to make wet spots appearing after rain particle drop. It forced me to dive into deep research in Niagara, materials and rendering pipeline of Unreal.

In this article, I will explain what this effect consists of:\
\!\[Video with the result]()

## Niagara particles

First, I needed some rain particles. The particles in the project are slightly modified ones from the [Ghislain Girardot's tutorial](https://www.youtube.com/watch?v=7stKYkRYmu0). Particles have complex and physicly accurate behavior. It includes 3 different states:

### 1. Sticky
It means the particle *(a rain drop)* sticks to the surface. It will follow the gravity and try to fall down, however, depending on the velocity and particle mass it will either stick and follow the surface, or it starts falling down to the floor

### 2. Fall
It is a free fall state for the rain drop. When a particle reaches the surface, it switches to a splash state.

### 3. Splash
This state simply draws a splash sprite adter that killing the particle.

## Material function

The idea was to have a universal material function, that can make any material look wet by tweaking original material values. The function in the project has been taken from this [Ben Cloward's tutorial](https://www.youtube.com/watch?v=fYGOZYST-oQ).

### Real life observations
...

### Node graph explanation
![Wetness function photo](/assets/post_data/dynamic_wetness/wetness-function.png)

## Dynamic wetness

I implemented a screen mask where all the wet spots were rendered as primitives, then this wetmask is sampled right from material graphs and affects the wetness value. As a result I can have wet spots exactly where the rain drops dropped.