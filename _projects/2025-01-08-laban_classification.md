<!-- ---
layout: project
title: "Laban Gesture Classification"
subtitle: "Pytorch, Python, C++, CNN, Computer Vision, Multi Agent System"
date: 2024-01-01
description: "This is my current project focus."
featured_image: "/assets/images/light.jpg" 
featured_image: "/assets/images/movement.jpg"
# featured_image: "/assets/images/encricle_from_above.gif"

categories:
  - portfolio
---

<img src="{{site.baseurl}}/assets/images/encricle_from_above.gif" width="1400">

## Project Overview

This performance explores the evolving relationship between a human dancer and a swarm of robots through a **gesture-classification model that interprets the dancer’s effort qualities** and a **choreographic swarm system that translates those interpretations into collective robotic behavior**.



## Laban Movement Overview


Laban Movement Analysis (LMA) is a framework used across dance, choreography, and somatic practice to describe and understand human movement. Developed by Rudolf Laban and later expanded by Irmgard Bartenieff, the system organizes movement into four interrelated categories:

<div style="display: flex; justify-content: center;">
  <img src="/assets/images/laban-graph.png" alt="laban efforts" style="width: 50%; max-width: 1000px; height: auto; border-radius: 5px;">
</div>

**Body** —  what the body is doing and how different parts coordinate

**Effort** — the qualities of movement, or its dynamic and emotional texture

**Shape** — how the body changes form and what motivates those changes

**Space** — where movement travels and its spatial harmonics

Laban combined Space, Weight, and Time into what he called the Effort Actions or Action Drive. These combinations create eight named efforts: Float, Punch (Thrust), Glide, Slash, Dab, Wring, Flick, and Press.

<div style="display: flex; justify-content: center;">
  <img src="/assets/images/laban1.png" alt="laban efforts" style="width: 25%; max-width: 1000px; height: auto; border-radius: 5px;">
</div>


## Gesture Classifier 
The gesture classifier focuses on four of the eight Effort Actions— **Float, Punch, Glide, and Slash**—each selected for their expressive contrast and their ability to be embodied clearly by both human and robot movement. The first four gestures are a part of the beginning of the performance and are not directly associated with laban effort.

Using the Laban Effort Action Method, the dancer performed roughly 80 phrases for each of the four efforts, providing the classifier with consistent, intentional examples that captured both gesture form and expressive quality. 
![Frames]({{site.baseurl}}/assets/images/all_gestures_gif.gif)



Each phrase was represented as a feature vector including:
- Kinematic features (velocity, accel, jerk)
- Spatial features (ranges, positions, deltas)
- Geometric features (path length, straightness)
- Normalization features (relative to hip/shoulder)

<div class="gallery" data-columns="1">
    <img src="/assets/images/laban_confusion.png">
    <img src="/assets/images/laban_features.png">

</div>

Float often appears as low velocity with gentle variability in direction, while Punch presents sharp spikes in velocity and strong directional commitment. Glide maintains smooth, sustained timing with direct pathways, whereas Slash exhibits quick, forceful, and more spatially indirect motion.

<div style="display: flex; justify-content: center;">
  <img src="/assets/images/shapes.png" alt="laban efforts" style="width: 75%; max-width: 1000px; height: auto; border-radius: 5px;">
</div>


During performance, the classifier runs continuously. Every two seconds, it outputs a predicted effort label, which then triggers a corresponding swarm behavior. In this way, the dancer’s movement becomes a real-time choreographic score, dynamically shaping how the swarm organizes, disperses, or transforms its collective motion.

![Frames]({{site.baseurl}}/assets/images/punch_screen.gif) -->
