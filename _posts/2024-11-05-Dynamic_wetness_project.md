---
title: "Dynamic wetness"
categories: [Personal projects]
pin: true
image:
  path: assets/post_data/dynamic_wetness/wetnessing.png
  alt: Screen mask and wetness functions applied
description: Self-development research project that introduces wet spots from rain VFX
---

## General information

This project is part of my year 3 [university](https://www.buas.nl/) coursework. It introduces wet spots from rain VFX

> ~~I wrote an [article](/posts/Dynamic_wetness_article/) with detailed explanations of how it works.~~ *Didn't yet :P*
{: .prompt-tip}

*Final result, with the "wetness" screen mask displayed in the top right corner:*
<video class="w-100" controls>
  <source src="https://github.com/user-attachments/assets/ff1e54f3-59c8-4df7-8bfe-ccd45236d138" type="video/mp4">
</video>

## Features of the project

- The surface becomes wet precisely at each raindrop's impact point.
- Full access to buffers and render targets containing all relevant data, accessible from blueprints and material graphs.
- High performance is maintained by rendering wetness information in a separate screen-space mask, which is then applied.

> There is a [link to the GitHub repo](https://github.com/SmailikHappy/GraphicsConcepting) with this Unreal project
{: .prompt-tip}