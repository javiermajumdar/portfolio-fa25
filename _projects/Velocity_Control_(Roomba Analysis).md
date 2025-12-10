---
layout: project
title: Velocity Control (Roomba Analysis)
description: Velocity Control for Roomba
technologies: [MATLAB]
image: /assets/images/roomba.jpg
---

For this project, our team conducted an analysis of the Roomba robotic vacuum, focusing on its sensing, navigation, and control. My role in the group was to investigate the Roomba's velocity control, responsible for regulating wheel speed and enabling motion. This involved studying how the Roomba interprets sensor inputs, how its motor controllers respond to velocity commands, and how these behaviors can be modeled using state-space representations and dynamic simulations.

Velocity control is central to how a Roomba moves and responds to its surroundings. The Roomba adjusts its wheel speeds based on sensor inputs, which may include dirt detection sensors, obstacle sensors, cliff sensors, and surface hardness detection sensors [6]. These adjustments are controlled through a PID controller that manages the motor speed in RPM. Understanding the velocity control system provides insight into how the Roomba converts sensor inputs to motion through the wheels.

![Figure 1]({{ site.baseurl }}/assets/images/velocitycontrol.png)

To visualize the behavior of a closed-loop velocity controller, I created a MATLAB script that simulates the velocity response of a motor similar to that of a Roomba. Figure 1 shows the step response to a velocity setpoint of 300 RPM. The model I used to get the measured velocity curve was made using a simplified model of DC motor dynamics. The equation I used to model this was:
ω(t)=300(1-e⁻⁰·⁰⁰⁸ᵗ) + 5 sin(0.01t)
The term with the exponential represents the first-order increase in speed due to the dynamics and inertia of the system, and the sinusoidal term represents the effects of closed-loop behavior due to disturbances, friction, or controller tuning. 

With the line of the setpoint plotted next to the system response, performance metrics may be evaluated, including the rise time, settling time, overshoot, and steady state error. These metrics are important for tuning the velocity controllers for the Roomba.


![Figure 2]({{ site.baseurl }}/assets/images/motordynamics.png)

![Figure 3]({{ site.baseurl }}/assets/images/kinematics.png)

These figures illustrate the different state space models used to describe the velocity-controlled motion of the Roomba. 

Figure 2 shows the state space model for the motor dynamics of the Roomba. This model describes how the motor voltage delivers the wheel velocity. The state variables include the motor angular velocity and the motor current. The input of this model is the applied motor voltage, while the output is measured by the wheel angular velocity. The state space model was formed using both electrical and mechanical dynamics of the system using the torque-current relationship, the back-emf relationship, and other friction/resistance terms. 

Figure 3 shows the kinematic state space model that describes how the wheel velocities control the Roomba’s motion. The state variables include the x and y position on the floor and theta, the angle at which it turns. Inputs include the wheel angular velocities for both the left and right wheels coming from the motor velocity controllers. The kinematic equations used to describe this system include the forward velocity, angular velocity, and position, which are used to form the state space model as shown above.

Both of the state space models demonstrate the complete motion of the velocity control in the Roomba. The motor voltage creates angular velocity in the wheels, and the kinematic model shows how the wheel speeds translate into motion. The models are separated since the motor dynamics occur much faster than the motion of the Roomba. Furthermore, it allows the velocity controller to regulate the wheel speed independently of the position.
