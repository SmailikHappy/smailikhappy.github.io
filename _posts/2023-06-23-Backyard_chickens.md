---
title: "Backyard chickens"
categories: [Group projects]
image:
  path: assets/post_data/backyard_chickens/logo.png
shipped_game: true
description: Local coop game made in Unreal, based on Rampart (1991) gameplay
skills: [Team, Game]
---

## General information

This is a group project completed at university as part of a course assignment. The team consisted of 14 developers.\
The game is a remake of [Rampart](https://en.wikipedia.org/wiki/Rampart_(video_game)) from 1991, featuring a chicken-themed style. It was developed using Unreal Engine.

> The game can be found on [itch.io](https://smooth-dedede.itch.io/backyardchickens)
{: .prompt-tip}

## Gameplay

Backyard Chickens is a two-player couch co-op game inspired by Rampart (1991). Players alternate between a building phase, where they construct defenses using randomly assigned Tetris-like fence pieces and cannons, and an attacking phase, where they fire their cannons to destroy the opponent's defenses!

{% include embed/youtube.html id='SCvI8EL6XrA' %}

## Personal contribution

- I setup Perforce (source control system)

- I made tools for designers to customize the world grid (playfield for the game)
  - Designers can resize and transform the game grid.
  - A river flows across the grid, splitting the map into two distinct sides.
  - The river is generated using an array of points, ensuring flexibility in a map design.

<video class="w-100" controls>
  <source src="https://github.com/user-attachments/assets/874d2ab5-b3e9-4ce3-b2b2-40e625fbe66e" type="video/mp4">
</video>

- I coded shaders and materials
  - Simple water shader for the river\
  ![water_shader](https://github.com/user-attachments/assets/7cd45dda-c589-4c5a-abef-d8a893115b46)

  - Post-process outline shader that highlights objects in different colors based on their team affiliation.\
  ![Outline_shader](https://github.com/user-attachments/assets/1947de0d-e123-4345-895d-552a3f44225d)

- Contributed to the game algorithms written in C++
  - CPP functions available in blueprints\
  ![world grid cpp exposed functions](https://github.com/user-attachments/assets/0b4ff239-0b27-4905-b02e-2131425c57ac)

  - Example function **create grid** written in C++\
  ![create grid](https://github.com/user-attachments/assets/a8c64bf8-b9e4-4703-ae51-d9d26364b734)