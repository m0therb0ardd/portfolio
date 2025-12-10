<!-- ---
layout: project
title: "Swarm Choreography"
subtitle: "Pytorch, Python, C++, CNN, Computer Vision, Multi Agent System"
date: 2024-01-01
description: "This is my current project focus."
# featured_image: "/assets/images/light.jpg" 
# featured_image: "/assets/images/movement.jpg"
featured_image: "/assets/images/encricle_from_above.gif"

categories:
  - portfolio
---

<img src="{{site.baseurl}}/assets/images/encricle_from_above.gif" width="1400">

## Project Overview

This performance explores the evolving relationship between a human dancer and a swarm of robots through a **gesture-classification model that interprets the dancer’s effort qualities** and a **choreographic swarm system that translates those interpretations into collective robotic behavior**.


## System Overview
The system transforms the dancer’s movement into real-time swarm behavior by capturing video from a front-facing camera, extracting body landmarks with MediaPipe, and classifying each 2-second movement window using a Laban-inspired Random Forest model. Each predicted movement quality then triggers a corresponding algorithm on the Coachbot swarm, allowing the robots to collectively express the dancer’s dynamics through emergent group motion.
<div style="display: flex; justify-content: center;">
  <img src="/assets/images/overview_swarm.png" alt="system overview" style="width: 50%; max-width: 1000px; height: auto; border-radius: 5px;">
</div>



## Swarm Algorithms 
The swarm algorithms were designed as creative interpretations of Laban Effort qualities—translations of human expressive dynamics into fully distributed robotic behaviors. Each algorithm began in simulation, where considerations such as shape, directionality, flow, and effort quality guided both the control logic and the emergent group patterns. 

A key transition point in the system is Encircling—a behavior that does not correspond to a Laban Effort but marks the shift from purely directional command to laban inspired movement dialogue. Encircling, Float, and Slash are the three most complex and visually dynamic algorithms, each crafted to evoke a distinct movement quality while maintaining decentralized control across the swarm. Additional choreographed behaviors (Left. Right, Glitch, Punch, Glide, etc.) are documented on github but the following three form the expressive core of the system.


<iframe title="vimeo-player" src="https://player.vimeo.com/video/1144723633?h=bcf4b6dd0a" width="640" height="360" frameborder="0" referrerpolicy="strict-origin-when-cross-origin" allow="autoplay; fullscreen; picture-in-picture; clipboard-write; encrypted-media; web-share"   allowfullscreen></iframe>

#### Encircling
The Encircling behavior creates a coordinated vortex around the dancer, where the swarm self-organizes into two concentric rings. The inner ring moves counterclockwise while the outer ring moves clockwise, producing a braided, ribbon-like motion that wraps the human performer in a dynamic orbit.
- At startup, each robot measures its distance from the arena’s center, assigning itself to either the inner or outer ring based solely on this initial radius—no communication or central coordinator is required.
- Each robot computes the correct tangential direction for its ring: the inner ring rotates counterclockwise, while the outer ring rotates clockwise, ensuring the two layers weave past each other without collision.
- Throughout the motion, robots continuously correct their radial position using a proportional controller, pulling themselves back toward the ideal ring while maintaining tangential velocity to sustain the orbit.
- Soft-wall boundary logic modulates forward speed near edges and halts the robot if it enters a critical zone, preserving safety while keeping the encirclement smooth and coherent.



####  Float
The Float behavior evokes lightness, indirectness, and gentle wandering. Robots drift as if carried by invisible currents, weaving softly through the space with subtle oscillations and loose flocking interactions that produce an airy, dreamlike motion.
- Robots apply a global upward drift paired with a sinusoidal side-to-side wave, creating a motion field that feels buoyant and fluid rather than directional or forceful.
- A soft flocking system—separation, cohesion, and alignment—keeps robots loosely gathered without locking them into a rigid structure, allowing the swarm to breathe and expand organically.
- Wave phases differ between robots, producing asynchronous lateral sway that gives the swarm a shimmering, floating quality rather than synchronized oscillation.
- Boundary forces gently nudge robots inward when they stray near arena walls, preserving the soft wandering motion while preventing collisions; if a robot reaches a critical boundary it stops safely.

#### Slash 
The Slash behavior is forceful, fast, and diagonally peeling. Robots carve sharp, sweeping paths through the space, accelerating along angled trajectories while breaking uniformity with sudden zig-zags and drifting arcs. The motion feels heavy and decisive — a cutting gesture that slices across the swarm rather than flowing with it.
- Robots begin by exchanging positions to estimate the swarm’s center and dynamically split into inner and outer groups. Each group is assigned a different vertical migration target, causing the whole formation to shear apart in opposing diagonal directions.
- During the main slash motion, each robot follows its ring path upward or downward while adding a sharp tangential component created from two sources: a high-frequency zig-zag oscillation and a directional drift away from the swarm’s centerline. Together, these produce the characteristic diagonal, slicing feel.
- An anti-jam tangential repulsion term pushes robots sideways relative to the ring whenever they approach neighbors too closely, preventing head-on collisions and reinforcing the sense of bodies cutting past one another.
- When the migration phase ends, robots enter a correction state that removes the zig-zag and drift, pulling each bot cleanly back into its proper ring position. Boundary conditions continuously enforce safety, while ring-based LEDs visually distinguish the two diagonally splitting layers














#### Directional Left/Right
A rigid-body translation where the swarm computes its own center of mass and then slides together mainting its formation. 
- Distributed COM estimation: Robots exchange small heartbeat packets (x, y, id) to estimate a shared center-of-mass in ~3 seconds without any global controller.
- Relative offset locking: Each robot saves its personal offset (dx, dy) from the estimated COM, guaranteeing shape preservation during the translation.
- Time-parameterized movement: The formation center interpolates from C0 to Cfinal over a fixed duration, guaranteeing synchronized motion across robots.
- Soft-wall repulsion: A continuous force term pushes robots away from arena boundaries, maintaining safety without abrupt stopping.



#### Glitch
The Glitch behavior embodies disruption, fragmentation, and sharp irregularity in the swarm. It introduces temporal randomness and abrupt radial bursts that break the flow of the swarm and create a feeling of instability.
- Each robot begins idle, then selects a random delay (2–8 seconds) before activating, creating desynchronized motion across the swarm.
- When activated, the robot computes the radial direction away from the arena center and turns toward it using a proportional controller.
- It performs a sharp outward burst, moving exactly 6 inches beyond its starting radius at a high, fixed speed.
- Once it reaches its target distance, the robot stops and freezes in place, signaling completion with a green LED.

#### Encircling
The Encircling behavior creates a coordinated vortex around the dancer, where the swarm self-organizes into two concentric rings. The inner ring moves counterclockwise while the outer ring moves clockwise, producing a braided, ribbon-like motion that wraps the human performer in a dynamic orbit.
- At startup, each robot measures its distance from the arena’s center, assigning itself to either the inner or outer ring based solely on this initial radius—no communication or central coordinator is required.
- Each robot computes the correct tangential direction for its ring: the inner ring rotates counterclockwise, while the outer ring rotates clockwise, ensuring the two layers weave past each other without collision.
- Throughout the motion, robots continuously correct their radial position using a proportional controller, pulling themselves back toward the ideal ring while maintaining tangential velocity to sustain the orbit.
- Soft-wall boundary logic modulates forward speed near edges and halts the robot if it enters a critical zone, preserving safety while keeping the encirclement smooth and coherent.


#### Glide
Glide expresses Laban’s light, sustained, indirect effort quality. Instead of sharp bursts or impacts, Glide produces a continuous, graceful motion in which the swarm moves together like a drifting, rippling organism. The robots maintain fixed relative positions, following a shared moving “wave center” that oscillates laterally and slowly rises through the arena.
- When Glide is activated, the robots first exchange short heartbeat messages to estimate the swarm’s collective center of mass (COM). Each robot records its own offset from this shared center—its “place in the ring.”
- Once the COM is established, the robot enters continuous Glide:
- The COM begins to drift upward while oscillating side-to-side in a gentle sine wave.
- Each robot follows this moving COM while maintaining its original offset, creating a rigid, drifting ring that moves as a single body.

#### Punch
Punch is designed around Laban’s strong, quick, direct effort quality. In the swarm, Punch becomes a coordinated wave of force: robots align downward, aim precisely, and then execute a sharp forward dash. The behavior emphasizes commitment, acceleration, and impact — a robotic equivalent of a decisive, forceful strike.
- Robots continuously exchange pulse messages; receiving a new pulse triggers a punch cycle.
- Upon activation, a robot aims toward a downward heading (–90°) with slight random jitter, aligning itself for a direct strike.
- After a short aiming phase, the robot enters a high-speed dash lasting ~1.2 seconds, moving strongly and directly downward.
- A cool down interval prevents the robot from punching repeatedly, creating rhythmic waves of motion across the swarm.
- Boundary checks ensure safety; robots near the arena edge trigger a global stop signal.

####  Float
The Float behavior evokes lightness, indirectness, and gentle wandering. Robots drift as if carried by invisible currents, weaving softly through the space with subtle oscillations and loose flocking interactions that produce an airy, dreamlike motion.
- Robots apply a global upward drift paired with a sinusoidal side-to-side wave, creating a motion field that feels buoyant and fluid rather than directional or forceful.
- A soft flocking system—separation, cohesion, and alignment—keeps robots loosely gathered without locking them into a rigid structure, allowing the swarm to breathe and expand organically.
- Wave phases differ between robots, producing asynchronous lateral sway that gives the swarm a shimmering, floating quality rather than synchronized oscillation.
- Boundary forces gently nudge robots inward when they stray near arena walls, preserving the soft wandering motion while preventing collisions; if a robot reaches a critical boundary it stops safely.

#### Slash 
The Slash behavior is forceful, fast, and diagonally peeling. Robots carve sharp, sweeping paths through the space, accelerating along angled trajectories while breaking uniformity with sudden zig-zags and drifting arcs. The motion feels heavy and decisive — a cutting gesture that slices across the swarm rather than flowing with it.
- Robots begin by exchanging positions to estimate the swarm’s center and dynamically split into inner and outer groups. Each group is assigned a different vertical migration target, causing the whole formation to shear apart in opposing diagonal directions.
- During the main slash motion, each robot follows its ring path upward or downward while adding a sharp tangential component created from two sources: a high-frequency zig-zag oscillation and a directional drift away from the swarm’s centerline. Together, these produce the characteristic diagonal, slicing feel.
- An anti-jam tangential repulsion term pushes robots sideways relative to the ring whenever they approach neighbors too closely, preventing head-on collisions and reinforcing the sense of bodies cutting past one another.
- When the migration phase ends, robots enter a correction state that removes the zig-zag and drift, pulling each bot cleanly back into its proper ring position. Boundary conditions continuously enforce safety, while ring-based LEDs visually distinguish the two diagonally splitting layers. -->