---
title: "Custom cross-platform game engine"
show_on_home_page: true
categories: [Group projects]
image:
  path: assets/post_data/fps_coop/fps.png
description: PC / PS5 cross-platform engine that uses Blender as level editor
skills: [Team, Custom engine, C++]
---

## General information

This is a group project completed at [Breda University](https://www.buas.nl/) as part of a course assignment. The goal was to **develop a cross-platform game engine for PC and PS5** suitable for shooters in teams of programmers, my team had 6 programmers overall.

During the project, I deepened my knowledge in graphics and blender scripting, learned CI/CD pipeline and applied it in team work.

It is worth to mention, I got some crucial lessons on why do we need peer code reviews, code style agreement and automatic codebase merge workflow.

> The project's codebase cannot be shared due to protection of NDA rules!
{: .prompt-warning}

## Demo of the project

<video class="w-100" controls>
  <source src="https://github.com/user-attachments/assets/0e870f69-abd3-4876-a9f3-917ac928d00c" type="video/mp4">
</video>

## Features that project has:

- Cross platform support (PS Windows and PlayStation 5)
- Jolt physics library
- Keyboard, mouse and gamepad input handling
- PBR rendering *(provided in the template)*
- Directional, spot and point light support
- Variance shadow mapping for all the light types
- Animations
- Blender plugin for level editing
- Level import pipeline directly from Blender
- Entity component system *(provided in the template)*
- Asset managment *(provided in the template)*

## Personal contribution

- I made shadows using variance shadow mapping technique on both platforms for every type of light source.

{% assign input_posts = site.posts | where: 'footnote', '445432' %}
{% include footnote-post.html %}

- I contributed to blender plugin

{% assign input_posts = site.posts | where: 'footnote', '938274' %}
{% include footnote-post.html %}