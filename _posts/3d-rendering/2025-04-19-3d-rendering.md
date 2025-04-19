---
layout: post
title: 3D world rendering
date: 2025-04-19
categories: jekyll update
usemathjax: true
---

There's a pipeline which is usually applied to every object before it's got on a user screen.
It is not that straigtforward as it could be, but after realizing how it is deduced, it's getting much easier.
The reason of the following text is to finally figure out how all these things work under the hood. 

General view of the process

<img src="3d-rendering/general_view.jpg"> 

So as you may see, there is 5 spaces in which an object may exist:
- 1. Local space - in its own coordinate system.
- 2. World space - in the world coordinate system.
- 3. View space - in the camera's coordinate system. 
- 4. Clip space - TODO 
- 5. Screen space - TODO

There is nothing really interesting to say about the first 2 spaces, 
let's just skip it.

The fun begins from the 3rd one. What is the view space? 

Let's say we have a camera just wandering around in the world space. The camera's coordinate system forms the view space. 

What parameters does the camera have? 
- Position in the world space 
- Direction 
- Up vector 

Position \\(\vec{P}\\) is a vector starting from a world space origin and pointing to a camera position.

Direction \\(\vec{D}\\) is a vector starting from a camera position and pointing to a certain point in the world space.

Up vector \\(\vec{U}\\) is a vector pointing up relatively to the camera. It is not supposed to be always perpendicular to \\(\vec{D}\\) and is always adjusted (gonna text about it later).

The first thing that should be done is a calculation of basis vectors from a view space coordinate system. 

Let's say \\(\vec{f}\\) (front), \\(\vec{r}\\) (right), \\(\vec{u}\\) (true up) are basis vectors of this system. The first thing we should do is calculate \\(vec{r}\\) the \\(\vec{r}\\)
