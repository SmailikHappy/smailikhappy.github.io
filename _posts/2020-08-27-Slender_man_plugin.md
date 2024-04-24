---
title: "Slender man Minecraft plugin"
categories: [Personal projects]
---


This is a plugin that allows you to play as a slenderman against your friends in a Minecraft.


## Rules

Game has a team of slender-man's and innocents.\
Slender man's goal is to kill everyone.\
Innocent's goal is to collect 8 papers on the map, evading looking on the slender-man.

## Gameplay

Slender man places 9 papers around the map.\
When all papers have been hidden, the actual game starts.\
Innocents can collect the paper just right-clicking it.\
Slender-man by default is invisible. To show itself a player should press <kbd>Shift</kbd> button. If the innocent's view captured the slender-man, the innocent takes damage.

## Download

You can [download](../../post_data/slender_man/SlenderMan-MCPlugin.zip "Download"). the plugin if you want to try it out.

## Usage

### Installation guide

0. Download the `.zip` via the link above.
1. Create a server that supports plugins (I have tested it on bukkit and spigot cores).
2. Unarchive the `.zip` and put the downloaded `.jar` file into `/plugins` folder.
3. Launch the server

### Commands

There is the list of commands available in the plugin

- `/add_innocent <nickname>` - gives a player an innocent role
- `/add_slender_man <nickname>` - gives a player a slender-man role
- `/remove_innocent <nickname>` - removes the role from a player
- `/remove_slender_man <nickname>` - removes the role from a player
- `/set_slender_spawn` - sets a position where a slender-man spawns
- `/set_innocent_spawn` - sets a position where an innocent spawns
- `/start_game` - starts the game
- `/stop_game` - stops the game