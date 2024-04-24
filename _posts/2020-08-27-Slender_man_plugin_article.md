---
title: "Slender man Minecraft plugin"
categories: [Articles]
---

## General information

This plugin allows you to play as Slenderman against your friends in Minecraft.

## Rules

- Game has a team of slender-mans and innocents.
- Slender man's goal is to kill everyone.
- Innocent's goal is to collect 8 out of 9 hidden papers on the map, evading looking on the slender-man.

## Gameplay

- Slender man places 9 papers around the map.
- When all papers have been hidden, the actual game starts.
- Innocents collect papers just right-clicking them.
- Slenderman is invisible by default. To reveal itself, a player must press the <kbd>Shift</kbd> button.
- If an innocent's view captures **visible** Slenderman, the innocent takes damage.

## Download

[Download](../../post_data/slender_man/SlenderMan-MCPlugin.zip "Download") the plugin to try it out.

## Usage

### Installation guide

0. Download the `.zip` via the link above.
1. Create a server that supports plugins (for example [bukkit](https://getbukkit.org/download/craftbukkit) or [spigot](https://getbukkit.org/download/spigot)).
2. Unzip the the archive and put the downloaded `.jar` file into `/plugins` folder.
3. Launch the server

### Commands

- `/add_innocent <nickname>` - gives a player an innocent role
- `/add_slender_man <nickname>` - gives a player a slender-man role
- `/remove_innocent <nickname>` - removes the role from a player
- `/remove_slender_man <nickname>` - removes the role from a player
- `/set_slender_spawn` - sets a position where a slender-man spawns
- `/set_innocent_spawn` - sets a position where an innocent spawns
- `/start_game` - starts the game
- `/stop_game` - stops the game