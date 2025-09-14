---
date: "2025-09-04"
draft: false
title: 'Lightroom Notes'
author: 'King Jin'
tags: ["Color theory","Photography"]
showtoc: true
---
I really love the feeling about using photo to represent some themes. Recently, I tried lightroom, which is a post-process software for photos. I learned many color theorys and tools behind it. Let's have a look.

## Color Theory.
1. Additive Color: RGB for Red, Green and Blue.
   - Red + Green + Blue = White  
2. Subtractive Color: These are created by mixing two additive colors.
   - Red + Green = Yellow
   - Green + Blue = Cyan
   - Red + Blue = Magenta
   - Yellow + Cyan + Magenta = Black

## Basics
1. Histogram: a graph that displays the brightness and color distribution of an image
   1. From left to right, each column represents the number of the white-black pixels in different level
   2. It has five different region, from left to right, they are blacks, shadows, exposure, highlights and whites.
   3. There are two triangles at the top left and top right. 
      1. the top left one is shadow clipping which will show you whether your image has region that was too dark
      2. the top right one is highlight clipping which show you whether your image has region that was too light
      3. the reason using clipping is because we can't represent a value of a pixel by the number of bits. For example, the most common bit to represent image is 8 bits(0-255), such as (0，128， 254). When the value over 255 or less than 0, the pixel will be break, and the information will be clipped to 255 and 0.
   4. There are several colors in the triangle
      1. gray - all details are well preserved
      2. red - red channel overexposure/underexposure
      3. green - green channel overexposure/underexposure
      4. blue - blue channel overexposure/underexposure
      5. yellow - yellow channel overexposure/underexposure
      6. cyan - cyan channel overexposure/underexposure
      7. magenta - magenta channel overexposure/underexposure
      8. solid white - RGB channel channel overexposure/underexposure in the same time
2. White balance
   1. Temperature
   2. Tint
3. Tone
   1. Exposure: change the overall brightness of the photo
   2. Contrast: Increase or decrease the difference between highlights and shadows in a photo. It can make highlights brighter and shadows darker or vice versa.
   3. Highlights: Only the brighter areas in the photo are controlled, excluding the brightest pure white areas, such as cloud details in the sky, hightlights on the skins, etc.
   4. Shadows: Only the darker areas in the photo, but does not include the darkest pure black parts, such as the details of people in the shadows, the dark parts of buildings, etc.
   5. Whites: Define the brightest point in photo, it controls the rightmost end of the brightness range and determines which parts of your image become pure white.
   6. Blacks: Define the "darkest point" or "black point" of your photo. It controls the leftmost end of the brightness range and determines which parts of the image will become pure black.
4. Presence
   1. Texture: Focus on the surface texture, such as skin pores, surface of rocks, etc.
   2. Clarity: 它不像“纹理”那么精细，而是让物体的轮廓和结构显得更“硬朗”或更“柔和”。It isn't as fine-detailed as "Texture". Instead, it makes the outlines and structures of objects appear "harder" or "softer".
   3. Dehaze: 主要用于消除照片中的大气薄雾、雾霾或朦胧感，同时增加色彩的饱和度。It is primarily used to eliminate atmospheric haze, smog, or mist in a photo, while simultaneously increasing color saturation.
   4. Vibrance: 它会优先提升画面中本身不太饱和的颜色（比如天空的蓝色、植物的绿色），而对于已经很饱和的颜色则影响较小. It selectively boosts the less saturated colors in an image (like the blue in the sky or the green in plants), while having a smaller impact on colors that are already highly saturated.
   5. Saturation: 一个“简单粗暴的”色彩增强工具。它会对画面中的所有颜色进行无差别的、同等程度的提升。A "simple and heavy-handed" color enhancement tool. It boosts all colors in the image indiscriminately and to the same degree.

## Tone Curve
1. The square graph looks similar with histogram, but contain a line segment from bottom left to top right.
2. We can pull the curve to change tone in specific region, pull the curve left and up will make region lighter(add more RGB) and right down make region darker(add more CMYK) for point curve.
3. we can also pull RGB channel separately.
4. S curve to increase contrast
5. Tips: e.g. to increase Yellow, we can pull the blue-yellow curve to yellow more, or we can pull red-cyan to red more and green-magenta to green more.

This post will update frequently.