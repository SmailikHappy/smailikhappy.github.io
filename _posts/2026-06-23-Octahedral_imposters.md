---
title: "Octahedral imposters"
categories: [Articles]
description: Short overview of creating octahedral imposters for real-time rendering.
skills: [Graphics]
notes: [Internship]
show_on_home_page: false
---

> This article is still in a draft state. Major changes are expected.
{: .prompt-danger}

## Article outline

This file contains a structured authoring skeleton suitable for converting presentation slides into article sections. Each section includes placeholders where slide content, diagrams, code, or assets should be inserted.

- Abstract
- Motivation & goals
- Background and theory
- Capture & baking pipeline
- Octahedral encoding (theory + math)
- Atlas packing & mipmaps
- Imposter shader: decode, lighting, and optimization
- LOD strategy, blending, and transitions
- Integration: Unreal Engine steps and plugin notes
- Export settings, recommended parameters, and examples
- Visual results and performance metrics
- Troubleshooting, limitations, and trade-offs
- Appendix: code snippets, HLSL, tools, and scripts

---

## 1. Abstract

Short summary of the technique and the contribution of this work. Keep this to 2–4 sentences. (Insert speaker notes / slide summary.)

<!-- Placeholder: add short slide summary here -->

---

## 2. Motivation & goals

- Problem statement: expensive geometry for distant objects, foliage, and crowds.
- Goals: reduce draw-calls, memory cost, and runtime CPU/GPU overhead while preserving silhouette and lighting at distance.
- Constraints: realtime requirements, streaming, and memory budgets.

(Insert 2–3 slides describing high-level motivation.)

---

## 3. Background and related work

- Billboarding & imposters: planar, spherical, and multi-view imposters.
- Octahedral normal encoding: compact normal representation benefits.
- Common atlas and baking strategies used in industry.

(Insert literature or slide citations here.)

---

## 4. Capture & baking pipeline (step-by-step)

For each step below, paste the corresponding slide content and attachments.

1) Scene preparation
   - Mesh preprocessing, LOD selection, bounding volumes.
2) View selection
   - Number of views, distribution (uniform sphere, stratified, importance sampling), and suggested angles.
3) Render passes
   - Render targets: albedo, normal (world/view), depth, mask, and optional material properties (roughness, metallic).
4) Octahedral encode during capture
   - Encode normals before writing to atlas.
5) Post-processing & packing
   - Atlas layout, padding, mipmaps, and auxiliary channel packing.

Placeholders: capture utility script, sample render target formats, and command-line examples.

---

## 5. Octahedral encoding (theory)

- Short derivation and the mapping equations.
- Encoding pseudocode and decoding formulas.
- Precision notes (8-bit vs 16-bit textures) and quantization artifacts.

Placeholder: insert slide(s) with equations and visual explanation.

---

## 6. Atlas packing & mipmaps

- Atlas layout strategies: row-major grid, adaptive packing, and power-of-two textures.
- Padding & border handling to avoid bleeding during bilinear sampling and mipmap generation.
- Mip generation: generate mipmaps per-view or for the full atlas — trade-offs.
- Recommended atlas sizes and per-imposter resolution table (suggested values).

Recommended defaults (example):
- Small props: 512x512 per view, 4–8 views
- Foliage clusters: 1024x1024 atlas with 8–16 views

---

## 7. Imposter shader (decode + lighting)

- Sample atlas using UVs computed from billboard vertex.
- Octahedral decode to reconstruct normals.
- Reconstruct view-space/world-space positions from depth and camera matrices when needed.
- Lighting path: per-pixel Blinn-Phong / PBR approximation notes.
- Optional: normal blending and view-dependent shading (pre-baked view-dependent color).

Placeholders: add slide code snippets or full HLSL/GLSL excerpts in the Appendix.

---

## 8. LOD strategy & blending

- When to swap mesh -> imposter (distance, screen-size threshold).
- Cross-fade strategies and silhouette preservation (alpha cutout, depth reprojection).
- Multi-resolution imposters and blending between imposter LODs.
- Handling shadow casters and occlusion.

---

## 9. Integration: Unreal Engine notes

- Plugin layout: capture tool, asset importer, atlas asset type, material function for octahedral decode.
- Material graph example: inputs (atlas, parameters) -> decode -> lighting.
- Editor workflow: create imposter asset, place billboard actor, configure LOD ranges.

Placeholders for Blueprint/HLSL snippets and editor screenshots.

---

## 10. Export settings & recommended parameters

- Capture render target formats (RGBA16F for normals/depth if high precision needed, otherwise RGBA8 with packing).
- Atlas size recommendations and view counts per object class.
- Mip generation options: compute mips after packing, use clamp or wrap for borders.
- Capture angles (table): suggested pitch/yaw per view for even coverage.

Example table placeholder (move content from presentation here).

---

## 11. Visual results & performance measurement

- Visual comparison: full geometry vs imposter at multiple distances.
- Performance metrics to collect: draw-calls, VRAM use, GPU time, CPU time, triangles rendered.
- Recommended benchmarking scenes and measurement scripts.

---

## 12. Troubleshooting, limitations & trade-offs

- Visual artifacts: normal quantization, seams between views, mip bleeding.
- Lighting limitations: dynamic lights, reflection probes, specular mismatch.
- When not to use imposters: close-up dynamic interactions, high-specular surfaces requiring parallax.

---

## 13. Appendix (code, HLSL, tools)

- Octahedral encode/decode functions (place slides here).
- Capture utility CLI usage and scripts.
- Atlas packing script snippets.
- Material graph screenshots and HLSL / Material functions.

---

## Slide -> Article mapping (for the other AI)

Instruction for the other AI: For each slide provided, produce the following JSON-like structure (or a short labeled block) and paste it below the matching article section:

- slide_index: <number>
- slide_title: <title>
- target_section: <article section heading>
- bullets: [short bullet points extracted from slide]
- speaker_notes: <full speaker notes / transcript>
- assets: [list of image/video/code filenames and where to place them]

Example mapping (fill from presentation):
- slide_index: 1
- slide_title: Title / Overview
- target_section: Abstract
- bullets: [one-line summary, main claim]
- speaker_notes: <paste>
- assets: [cover.png]

This mapping enables programmatic merging of presentation content into the article.

---

## Next steps for you

1. Paste the presentation slides (title + speaker notes + assets list) or let me ingest the slide text.
2. For each slide I'll place the content into the mapped section and produce a ready-to-publish article draft.

<!-- End of structured draft -->