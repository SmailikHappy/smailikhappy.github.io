---
title: "Article on variance shadow maps"
categories: [Articles]
descrition: How variance shadow maps work
---

> This article is being written now and not finished yet
{: .prompt-danger}

## What is this all about?

During my second year at [university](https://www.buas.nl/), we were divided into groups tasked with creating a custom engine that might be used to develop a game in the last quarter of the year.

As the graphics programmer for my team, I was responsible for implementing shadows. In this article, I will explain why I chose variance shadow maps and how they function.

> It would be helpful if you already have a basic understanding of light and shadow mapping algorithms.
{: .prompt-warning}



## Why variance shadow maps
Initially, I implemented the basic shadow mapping algorithm. However, the results were disappointing: shadows were pixelated, and shadow acne was the most annoying problem to face.

!.[Results with basic shadow mapping].()

//
// Probably, I shall mention PCF
//

After researching for a while, I decided to use a little more complex shadow mapping algorithm that provides efficient filtering, cheap edge softening, and a solution to the biasing problems of standard shadow maps.

!.[Results of VSM].()



## The pipeline

### Generating buffers & shadow maps

A shadow map is a texture containing light-view information, which is essentially the depth information of how far the light has reached.

> Algorithm to draw the shadow map is in the [next section](#shadow-pass--render-shadow-maps)
{: .prompt-info}

Typically, we would use only depth textures, but this algorithm requires to store 2 float values per pixel - depth and depth squared `float2( depth, depth * depth )`. Consequently, the texture will have 2 channels.

> You need to store the squared depth because you can't recalculate it after the filter pass; the math behind this will be [explained later](#why-we-cannot-recalculate-the-values-after-the-filter-pass).
{: .prompt-warning}

The size and number of shadow maps used per light source depends on the developer's choice. In my particular case, I used one large texture for the directional light, one small texture for the spot light, and a small cube texture for the point light. Coloured shadows are not taken into account in this implementation.



### Shadow pass / render shadow maps

Now, we are doing the same as all shadow mapping algorithms. We will render the scene from a light's point of view, which is similar to how a camera works. In this case, we are only interested in the depth information. The camera settings are unique per light type:

**Directional light**:
- Uses orthographic projection
- The *camera* is positioned far away from the center of the scene (or the player), so that all objects that can occlude are within the light's viewing frustum.
- The *camera* direction is the same as the light's direction

**Spot light**:
- Uses perspective projection
- The *camera* is located at the spot light's position
- The perspective FOV angle matches the light's angle
- The *camera* faces the same direction as the light

**Point light**:
- Uses 6 perspective projections to render a cube texture
- The *camera* is positioned at the point light's location
- The perspective FOV angle is 90° for each face of the cube texture.

> I recommend you [this beginner tutorial from OGLDEV](https://youtu.be/uhCbfZ_L7uc?si=f9bDW9sbryrW3Tsx) that explains how to render shadow maps for point light sources. There are some nuances.
{: .prompt-tip}

After setting all the necessary parameters, we pass the scene mesh data and render it to the shadow map in the form of `float2( depth, depth * depth )`.



### Filter pass (blurring)

In this pass, we need to blur the shadow map values. I have used a [Gaussian blur](https://en.wikipedia.org/wiki/Gaussian_blur) algorithm in my case. This algorithm is applied twice - horizontally and vertically.

```hlsl
void main()
{
	vec4 pixelColor = vec4(0.0f);

	vec2 finalUV[7];
	uint i = 0;

	for (float offset = -3.0; offset <= 3.0; offset += 1.0f)
	{
		finalUV[i++] = clamp(v_uv + offset * u_blurScale, float2(0.0f), float2(1.0f));
	}
	
	pixelColor += texture(raw_shadowMap, finalUV[0]) * (1.0f / 64.0f);
	pixelColor += texture(raw_shadowMap, finalUV[1]) * (6.0f / 64.0f);
	pixelColor += texture(raw_shadowMap, finalUV[2]) * (15.0f / 64.0f);
	pixelColor += texture(raw_shadowMap, finalUV[3]) * (20.0f / 64.0f);
	pixelColor += texture(raw_shadowMap, finalUV[4]) * (15.0f / 64.0f);
	pixelColor += texture(raw_shadowMap, finalUV[5]) * (6.0f / 64.0f);
	pixelColor += texture(raw_shadowMap, finalUV[6]) * (1.0f / 64.0f);

	frag_color = vec4(pixelColor.xy, 0.0f, 0.0f);
}
```

#### Why we cannot recalculate the values after the filter pass?

..show mathematics..

`((a+b) / c)^2 != (a^2 + b^2) / c`\
`(a+b)^2 / c^2 != (a^2 + b^2) / c`\
`(a^2 + 2ab + b^2) / c != a^2 + b^2`\
`a^2 + 2ab + b^2 != c*a^2 + c*b^2`



### Render pass

Code to sample the shadow map

- `shadowMap` - The shadow map texture to sample
- `coords` - The texture coordinates to sample the shadow map at
- `compareValue` - The depth value to compare with the shadow map
- `varianceMin` - The minimum allowed variance (to avoid division by zero)
- `lightBleedReductionAmount` - The amount of light bleed reduction to apply

```hlsl
float linstep(float low, float high, float v)
{
    return clamp((v-low) / (high-low), 0.0f, 1.0f);
}

float SampleVarianceShadowMap(sampler2D shadowMap, vec2 coords, float compareValue, float varianceMin, float lightBleedReductionAmount)
{
    vec2 moments = texture(shadowMap, coords.xy).xy;
	
	float p = step(compareValue, moments.x);
	float variance = max(moments.y - moments.x * moments.x, varianceMin);
	
	float d = compareValue - moments.x;
	float pMax = linstep(lightBleedReductionAmount, 1.0, variance / (variance + d*d));
	
	return min(max(p, pMax), 1.0);
}
```

> The values I used for OpenGL
>
```cpp
const float c_directLightBleedReductionAmount = 0.6f;
const float c_directVarianceMin = 0.000002f;
const float c_spotLightBleedReductionAmount = 0.9997f;
const float c_spotVarianceMin = 0.0000004f;
const float c_pointLightBleedReductionAmount = 0.997f;
const float c_pointVarianceMin = 0.000009f;
```
{: .prompt-tip}



## Weighing 

Show results



## Impressions

...



Thanks for reading this. GG

![BUas logo](../assets/post_data/deferred_renderer/buas-logo.png)
*This project was part of university course*