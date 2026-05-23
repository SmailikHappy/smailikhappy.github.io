---
title: "Octahedral imposters"
categories: [Articles]
description: Short overview of creating octahedral imposters for real-time rendering.
skills: [Unreal, Rendering, Shader, C++]
show_on_home_page: false
---

## General information

Octahedral imposters are an efficient method to represent complex 3D geometry using compact 2D textures and simple billboards. This post documents a concise overview of the technique, the pipeline I used to generate imposters, and the trade-offs considered when integrating them into a real-time engine.

> This is a short summary. I will expand the technical details, screenshots, and performance comparisons later.
{: .prompt-tip}

## Key algorithm steps

1. Capture views
   - Render the target mesh from a set of directions into render targets (albedo, normal, depth, and optionally a mask).
2. Encode normals with octahedral mapping
   - Pack 3D normal vectors into a 2D octahedral map to store per-pixel orientation efficiently.
3. Pack data into atlas textures
   - Combine captured views into a texture atlas with mipmaps and auxiliary channels (roughness, metallic, etc.) as needed.
4. Imposter shader
   - Sample atlas in the shader, reconstruct normal from octahedral encoding, and perform lighting in view-space or world-space depending on the approach.
5. LOD and blending
   - Blend between imposters and the original mesh (or different imposter LODs) to hide popping and preserve silhouettes.

## Implementation

- Engine: Unreal Engine (custom plugin + materials)
- Tools: Custom capture utility that automates render target creation and atlas packing.
- Shader: Material function for octahedral decode and lighting reconstruction.

The implementation uses a render-pass to bake view-dependent textures and a lightweight shader to reconstruct surface properties at runtime.

{% include embed/youtube.html id='VIDEO_ID' %}

## Personal contribution

- Designed the capture and packing pipeline used to generate imposter atlases.
- Implemented octahedral encode/decode utilities and integrated them into material graphs and HLSL functions.
- Built a simple in-engine tool to place imposters and manage LOD transition.

## Results

- Significant draw-call reduction for dense foliage and small props.
- Minor lighting differences compared to full-geometry at distant LODs; acceptable for medium-to-far camera ranges.

*Screenshots and performance charts will be added here.*

![Placeholder preview](https://placehold.net/default.png)


## Notes and next steps

- Add detailed shader excerpts and HLSL examples.
- Provide export settings, capture angles, and recommended atlas sizes.
- Include before/after performance graphs and visual comparisons.

<!-- End of post -->