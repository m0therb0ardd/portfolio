---
layout: project
title: "Physics Simulator"
subtitle: "Python, Sympy, Dynamics, Processing"
date: 2024-01-01
description: "This project simulates a jack falling inside a rotating box using constrained Euler Lagrange equations to calculate and simulate impacts."
featured_image: "/assets/images/jack_beautiful.gif" # Replace with your thumbnail image or GIF
categories:
  - portfolio
---

## **Jack in the Box Dynamics**

This project involves simulating the dynamics of a jack in the box using Lagrangian mechanics, symbolic differentiation, and constraint handling. The goal was to model the interactions between the box and the jack, enforce constraints during impacts, and analyze the system's behavior.

---
![Jack Box]({{site.baseurl}}/assets/images/jack_beautiful.gif)


<!-- 
### **Set Up**

This diagram shows how I labeled and oriented my world frame, box frame, box side frames, jack frame, and jack endpoint frames. -->

#### **Box Frames from Center of Box**
```python
# Transformation matrices for box
g_wb = transformation_matrix_sym(theta_b, x_b, y_b)
g_b_top = transformation_matrix_sym(0, 0, box_length/2)
g_b_bottom = transformation_matrix_sym(0, 0, -box_length/2)
g_b_right = transformation_matrix_sym(0, box_length/2, 0)
g_b_left = transformation_matrix_sym(0, -box_length/2, 0)

g_w_top = g_wb * g_b_top
g_w_bottom = g_wb * g_b_bottom 
g_w_right = g_wb * g_b_right
g_w_left = g_wb * g_b_left

# Transformation matrices for jack
g_bj = transformation_matrix_sym(theta_j, x_j, y_j)
g_jjleft = transformation_matrix_sym(0, -jack_length, 0)
g_jjbottom = transformation_matrix_sym(0, 0, -jack_length)
g_jjtop = transformation_matrix_sym(0, 0, jack_length)
g_jjright = transformation_matrix_sym(0, jack_length, 0)

# Full jack in box frame transformations
g_b_jleft = g_bj * g_jjleft
g_b_jbottom = g_bj * g_jjbottom # Bottom of jack in world frame
g_b_jtop = g_bj * g_jjtop
g_b_jright = g_bj * g_jjright

``` 
### **Approach**

#### **1. Lagrangian Dynamics**
The system's Lagrangian was defined as the difference between kinetic energy KE and potential energy PE:

$$
L = \text{KE} - \text{PE}
$$


Using symbolic differentiation, I derived the following:
- Partial derivatives of $(L)$ with respect to the generalized coordinates $(q)$ and their time derivatives $(\dot{q})$
.
- The equations of motion:

$$
\frac{d}{dt} \left( \frac{\partial L}{\partial \dot{q}} \right) - \frac{\partial L}{\partial q} = F_{\text{external}}
$$



These expressions were set equal to the external forces and torques acting on the system, allowing the accelerations $(\ddot{q})$
 to be solved symbolically.

External forces included:
- Gravity acting on the box and jack.
- A force to keep the box from falling.
- A torque to rotate the box counterclockwise.

---

#### **2. Constraints and Impact Handling**
Constraints were added to ensure the jack and box interact correctly. These constraints maintain the jack's endpoints relative to the box's sides, such as keeping the bottom of the jack aligned with the bottom of the box.

$$
\phi_1 = y_j^{\text{bottom}} - y_b^{\text{bottom}}
$$

There are 16 total constraints to account for all sides of the jack and box.

- **Constraint Violations:**  
  The code evaluates the impact conditions for each constraint using the `impact_condition` function. Violations are detected when constraints exceed a defined threshold.

- **Impact Update:**  
  The `impact_update` function computes post-impact velocities by solving the following:
  - The impact equations with Lagrange multipliers $(\lambda)$ to enforce the constraints.
  - The Hamiltonian to ensure energy conservation.


---
\
This structured approach allowed the system to dynamically adjust its state based on physical principles, ensuring consistency with both energy conservation and interaction constraints.


---