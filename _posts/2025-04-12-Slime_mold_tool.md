---
title: "Slime mold tool"
categories: [Articles]
image:
  path: assets/post_data/slime_mold/slime_mold.png
  alt: The slime mold that covers the world geometry
description: Unreal plugin to edit and generate Slime Mold in the editor
skills: [Solo, Unreal, Plugin, C++]
show_on_home_page: true
---

> This project is work-in-progress, probably the whole post will be rewritten.
{: .prompt-danger}



## What is this all about?

My team is working on a game called [Katharsi](../Katharsi). One of my tasks was to create a tool for artists to spread the slime mold (the goop) around the game environment. In this article I will explain the plugin I created for this tool and how the generation is built on top of it.

> The source code of the plugin and this tool is available on [<i class="fab fa-github"></i> GitHub](https://github.com/SmailikHappy/SlimeMoldTool), where you can also find instructions on how to use it for you own project.
{: .prompt-tip}


*A small video of the tool in action:*

<video class="w-100" controls>
  <source src="../../assets/post_data/slime_mold/beta_tool_showcase.mp4" type="video/mp4">
</video>

> In this video:
> - Firstly, I create a skeleton that the goop should follow.
> - Then I press `GenerateMesh` button to generate the goop mesh.
> - Finally, I am adjusting some of point parameters that impact the generation result.
{: .prompt-info}



## Plugin (C++ part)

The plugin is implemented in C++ using [InteractiveToolsFramework](https://www.gradientspace.com/tutorials/2021/01/19/the-interactive-tools-framework-in-ue426) (further ITF). It introduces a new editor mode with 2 tools:

- [**Skeleton tool**](#skeleton-tool)
- [**Mesh tool**](#mesh-tool)

### Skeleton tool

When this tool is selected, the user can place points and connect them with lines and adjust point data

*The video below shows most of the functionality of the tool and how 'the skeleton' reacts:*

<video class="w-100" controls>
  <source src="../../assets/post_data/slime_mold/skeleton_tool_usage.mp4" type="video/mp4">
</video>

### Mesh tool

When you select this tool, the user can press buttons to call delegates (events) in the actor they are editing. The user has to create their own properties (or use the example ones).

*The video below shows how the user can create custom properties and press buttons:*

<video class="w-100" controls>
  <source src="../../assets/post_data/slime_mold/mesh_tool_usage.mp4" type="video/mp4">
</video>

### Blueprint exposed functionality with an example

The user has access to the `SlimeMoldActorComponent`, which stores skeleton data (arrays of points and lines), has access to the custom properties and the delegates, which are called when the associated button is pressed.

*In the video below the goal is to generate cylinders on the lines and spheres on points.*\
*The video shows how easy it is to customize the tool and what blueprint code you need:*

<video class="w-100" controls>
  <source src="../../assets/post_data/slime_mold/full_tool_usage.mp4" type="video/mp4">
</video>

> Explanation of what is happening in the video:
> - At first, the `GenerateMesh` button is pressed but nothing happens because there is no code associated with the event. So we take the `OnGenerateMesh` delegate from the `SlimeMoldActorComponent`, attach the "Print" node to it and see that the button works.
> - After that, we add the actual generation code (see the video comments for more details).
> - Then we play with the skeleton to show that the skeleton data is used for generation.
> - After we are done, we try to change some custom parameters but nothing changes.
> - In the next frame, we rename the variables to fit our needs.
> - Then, we cast the property object, which comes with the delegate, to our `CustomProperties` class and link the "thickness" variable to the radius of the cylinder.
> - Testing and the thickness of the cylinder is being changed, but the radius of the spheres cannot be affected using parameters.
> - Next, we are doing the same with spheres, but this time the radius of the spheres is being changed as well.
{: .prompt-info}



## Generation algorithm

### References

![img](../assets/post_data/slime_mold/reference.png){: width="972" height="589" .w-50 .left}
This is the main reference - fungus that is growing over surfaces.\
The main game's reference is [The Last of Us fungus](https://thelastofus.fandom.com/wiki/Cordyceps_brain_infection).
<br>
<br>
<br>
<br>
<br>
<br>
<br>

### Unreal Geometry Script

I have used [Geometry Script](https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-scripting-users-guide-in-unreal-engine) plugin to generate the mesh. It is very similar to blender geometry nodes.

> The generation algorithm is not completely done yet.
{: .prompt-danger}


