---
title: "Bubble brawlers"
categories: [Group projects]
game_jam: true
image:
  path: assets/post_data/bubble_brawlers/logo.png
description: My first time in a global game jam (Y2025) with a team of 10 people
skills: [Team, Unreal, Game]
---

## General information

This project has been made for a global game jam in 2025 on topic - 'Bubble'.\
This is a local couch coop (2-4 players), where bubble buddies fight to be the last soap standing.

{% include embed/youtube.html id='rYIBy-wy3nI' %}

> You can download the game from [itch.io](https://mesibby.itch.io/bubble-brawlers). *But you need the controllers to play.*
{: .prompt-tip}

## Personal contribution

- Custom physics actor component\
> *Orange cube is twice as massive as green cube. Cone is positioned on a gravity center pull.*\
  *You can see how objects are pulled and resolve the collision when colliding with each other.*\
  *As a result, orange cube pushed away the green one.*
{: .prompt-info}
<video class="w-100" controls>
  <source src="/assets/post_data/bubble_brawlers/custom_physics.mp4" type="video/mp4">
</video>

- Game events:
  - Open tap - *fill the sink with a water, the tap water pushes objects from it.*
  - Spawn the hazard (fork or knife) - *simply spawns a new gameplay element (it can be pushed by the players or game events)*
  - Drain the water - *suck everything with the water*
<video class="w-100" controls>
  <source src="/assets/post_data/bubble_brawlers/event_system.mp4" type="video/mp4">
</video>