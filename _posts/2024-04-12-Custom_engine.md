---
title: "Custom cross-platform engine"
categories: [Group projects]
---

## General information

This is a group project completed at university as part of a course assignment. The team consisted of 6 programmers. The goal was to develop a cross-platform game engine for PC and PS5 that is suitable to create first person shooters.

During the project, I deepened my knowledge in graphics and blender scripting, learned CI/CD pipeline and applied it in team work. It is worth to mention, I got some crucial lessons on why do we need peer code checks, team code style agreement and automize the process of code merging.

## Final demo gameplay result

![GIF from the engine](../assets/post_data/fps_coop/game.gif)
*Short gif of resulting demo level from the project*

## Features that project has:

- Cross platform support (PS Windows and PlayStation 5)
- Jolt physics library
- Keyboard, mouse and gamepad input handling
- PBR rendering *(provided in the template)*
- Variance shadow mapping
- Animations
- Blender plugin for level editing
- Level import pipeline directly from Blender
- Entity component system *(provided in the template)*
- Asset managment *(provided in the template)*

## Personal contribution

- I made shadows using variance shadow mapping technique on both platforms for every type of light source.
- I contributed to blender plugin

## Blender as level editor pipeline

<video class="w-100" controls>
  <source src="/assets/post_data/fps_coop/blender_to_bee.mp4" type="video/mp4">
</video>

> On this video you can see a small example of blender being used as level editor.\
Blender plugin has basic functionality for lights, geometry and predefined actors.
{: .prompt-info}