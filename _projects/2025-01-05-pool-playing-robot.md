---
layout: project
title: "Pool-Playing 7 DoF Robot"
subtitle: "ROS2, Python, OpenCV"
date: 2024-01-01
description: "This project demonstrates the Franka Emika robot playing pool, using computer vision to identify and pocket balls dynamically."
#featured_image: "/assets/images/fran_cropped.jpg" 
#featured_image: "/assets/images/fran_sketch_color.jpg" 
featured_image: "/assets/images/output.jpg" 
#featured_image: "/assets/images/fran.jpg" 
#featured_image: "/assets/images/fran_sketch.jpg" 
#featured_image: "/assets/images/fran_stock.jpg" 

categories:
  - portfolio
---



## Pool-Playing Robot with Franka Emika Arm

This project was designed to make the Franka Emika Robot play a modified game of pool on a tabletop pool set. Using ROS2 and computer vision, the Franka dynamically identifies pool balls, calculates optimal shots, and executes precise movements to pocket balls.

--

<video controls width="800" style="display: block; margin: 0 auto;">
  <source src="/assets/images/pool.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>


### Subsystems

#### 1. Franka Emika Robot Arm
The Franka Emika robot was controlled using the ROS2 MoveIt API. Its trajectory planning capabilities were used to align our 3D-printed cue stick with the ball and complete accurate shots.

#### 2. Computer Vision
An Intel RealSense D435 Camera was used for vision processing:
- **April Tags**: Used for calibrating the position of the table and pockets relative to the robot.
- **Object Detection**: The vision system detected the red ball (our cue ball) and blue balls.

#### 3. Gameplay Coordination
A ROS2 package was developed to:
- Detect and identify the positions of balls and pockets.
- Plan optimal trajectories for shots.
- Handle game state transitions.

---

### System Flow

#### Table Calibration
- An April tag was affixed to the side of our pool table to identify the pool table and the pockets.
- A series of transformations related all objects in our scene to the base of the Franka arm.

#### Ball Detection
- Computer vision detected the position and color of balls on the table.

#### Shot Planning
- Our pool algorithm determined the best shot based on the current ball positions.
- A trajectory was generated for the robot arm to align the cue stick and execute the shot.

#### Gameplay Execution
- The robot arm continued to make shots until the cue ball was pocketed.
- If the cue ball was accidentally pocketed before all the blue balls, the Franka arm would return to its home position until a user placed the red ball back on the pool table.

---

### Personal Work

Personal contributions to the project include:
- Integrating the computer vision system with the ROS2 shot planning service.
- Testing and tuning the trajectory generation for precise and repeatable shots.

---

### Team Members

This project was developed as part of **ME 495: Embedded Systems in Robotics** at Northwestern University. Group members:
- An Nguyen
- Caroline Terryn
- Catherine Maglione
- Joseph Blom
- Logan Boswell


---
