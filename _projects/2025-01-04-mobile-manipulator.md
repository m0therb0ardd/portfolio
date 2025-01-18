---
layout: project
title: "Mobile Manipulator"
subtitle: "Trajectory Planning, Odometry, Feedback Control, Coppeliasim"
date: 2024-01-01
description: "This project demonstrates precise control of the youBot manipulator in CoppeliaSim."
#featured_image: "/assets/images/output.gif"
featured_image: "/assets/images/output_bw.gif"
#featured_image: "/assets/images/manip_color.gif"
#featured_image: "/assets/images/manipulation_bw.gif"


---


## Mobile Manipulator

This project focused on developing software to control the **youBot mobile manipulator**, a four mecanum-wheeled base and a 5R robotic arm. The goal was to create trajectory planning, odometry, and feedback control to enable precise end-effector manipulation.

The youBot picks up a block from a specified location, transports it to a target position, and releases it. These capabilities were visualized in the **CoppeliaSim simulation environment**.

![Mobile Manipulator Simulation](/assets/images/output.gif)

---

### Project Milestones

#### **1. Reference Trajectory Generation**
The end-effector trajectory was defined in eight segments using a combination of `CartesianTrajectory` and `ScrewTrajectory` functions from the modern-robotics library.

#### **2. youBot Kinematics Simulator**
The kinematics of the youBot were simulated using first-order Euler integration. The inputs included:
- The robot's current configuration (chassis position, wheel angles, and arm joint angles).
- Joint speeds.

The outputs predicted the next configuration. The transformation matrix for the chassis was computed based on the odometry equations.

#### **3. Feedforward Control**
The `FeedbackControl` function was implemented to compute the kinematic task-space feedforward and feedback control law. This method involved:
- Comparing the current end-effector configuration with the reference configuration at the current and next time steps.
- Deriving the commanded end-effector twist.
- Converting the commanded twist into wheel and arm joint speeds using the pseudo-inverse of the mobile manipulator Jacobian.

---



