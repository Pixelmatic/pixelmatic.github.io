---
layout: post
title:  "Challenge: The sphere formation"
excerpt: "An interesting challenge in Infinite Fleet development was to generate positions for each flying formations, knowing that the number of spaceships could change (generating positions for a fixed number of allies was not a solution). "
categories: Challenges
author: Nahil Zamiati
tags: [ challenges, gamedev, algorithm ]
---

An interesting challenge in Infinite Fleet development was to generate positions for each flying formations, knowing that the number of spaceships could change (generating positions for a fixed number of allies was not a solution). 

{% include image.html url="/assets/posts/challenges-sphere-formation/formations-example.svg" description="Figure 1: Sample of common 2D formations" %}

Some were pretty easy to calculate (arrow-shaped formation, line formation…), but one, in particular, was a little bit more difficult: the sphere formation. How to find, in a deterministic way, the positions of N points so they are (almost) evenly distributed on the surface of a sphere?

This problem will have exact solutions only for some specifics numbers of N points, corresponding to the vertices number of regular solids: 

{% include image.html url="/assets/posts/challenges-sphere-formation/image.svg" description="Figure 2: Platonic Solids <a href='https://en.wikipedia.org/wiki/Platonic_solid' target='_blank'>https://en.wikipedia.org/wiki/Platonic_solid</a>" %}
 
In other cases, the solution can only be an approximation of an evenly distributed set of points on a sphere (but still enough for spaceship's positions). Many different algorithms exist to solve this issue, but which one fits the most for space formations in a game? 
Share your solution!

```csharp
Vector3[] SphereFormationPositions(float sphereRadius, int numberOfShips)
{
    // Share your solution!
}
```

<strong>You have an interesting solution? Please submit it to us and apply for a position at Pixelmatic: <a href="mailto:challenge@pixelmatic.com">challenge@pixelmatic.com</a>!</strong>