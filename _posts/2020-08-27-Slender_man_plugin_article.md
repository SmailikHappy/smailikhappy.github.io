---
title: "Article on Slender man Minecraft plugin"
categories: [Articles]
description: More details and installation guide of my MC plugin 
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
- Innocents collect papers just left-clicking them.
- Slenderman is invisible by default. To reveal itself, a player must press the <kbd>Shift</kbd> button.
- If an innocent's view captures **visible** Slenderman, the innocent takes damage.

## GIFs
![Slenderman places notes](/assets/post_data/slender_man/place%20notes%20gif.gif)
*Slenderman hides some notes around the map*
<br>

![Slenderman attacks](/assets/post_data/slender_man/damaging.gif)
*Slenderman reveals itself and damages players in this way*
<br>

![Innocent picks up the note](/assets/post_data/slender_man/taking%20note.gif)
*Innocent player finds a note*

## Download

<!-- It is a download link, so it must have a correct path to the file according to the link in the browser. -->
[Download](../../assets/post_data/slender_man/SlenderMan-MCPlugin.zip "Download") the plugin to try it out.
> As this plugin is too old and no longer supported, this plugin generates numerous errors on modern server cores. So you will find `spigot-1.16.2.jar`{: .filepath} server-file to run it (though with some warnings).
{: .prompt-warning}

## Usage

### Installation guide

0. Download the `.zip`{: .filepath} via the link above.
1. Create a server using provided server `spigot-1.16.2.jar`{: .filepath} file.
2. Unzip the archive and put `SlenderMan-MCPlugin.jar`{: .filepath} file into `/plugins`{: .filepath} folder.
3. Launch the server and use the commands below

### Commands

> Commnads cannot be issued from a server console, only client (player on the server) can execute them.
{: .prompt-warning}

- `/innocentadd <nickname>` - gives a player an innocent role
- `/slenderadd <nickname>` - gives a player a slender-man role
- `/innocentremove <nickname>` - removes the role from a player
- `/slenderremove <nickname>` - removes the role from a player
- `/setslenderspawn` - sets a position where slender-mans will spawn
- `/setinnocentspawn` - sets a position where innocents will spawns
- `/start` - starts the game
- `/finish` - stops the game