---
layout: post
title: LAIKA, the quadrupedal robot
description: Designed and built a 12-DOF quadrupedal robot dog from the ground up—Fusion 360 CAD and 3D-printed structure, inverse-kinematics gait control on a ROS framework, and Simulink locomotion simulation.
skills: 
  - Robotics
  - Control Systems
  - Inverse Kinematics
  - ROS
  - Power Management
  - 3D modeling

main-image: /laika_cover.jpg
---

## Project Overview
LAIKA is a 12-DOF quadrupedal robot dog I built based on inspiration from Boston Dynamic's Spot robot. The goal was to build a robot that can move reliably, be tested iteratively, and serve as a foundation for exploring efficient gait, sensor-based feedback control, and robotic design.

{% include image-gallery.html images="laika_cover.jpg" height="400" captions="full robot assembly" %}


## Showcase
{% include image-gallery.html images="images/3dprint.jpg, images/3dprint2.jpg" height="400" captions="3D-printed leg parts | more 3D prints" %}
{% include image-gallery.html images="images/legchk.gif, images/front.jpg" height="400" captions="movement testing | front assembly" %}
{% include image-gallery.html images="images/half.jpg, images/bodyassemb.jpg" height="400" captions="leg joints done | total body assembly" %}
On the mechanical side, I modeled the robot in Fusion 360 and 3D-printed-body-parts for assmebly, which took me around 3 days because of some failed printing jobs. For motion, I derived DH parameters for forward kinematics and implemented gait logic through inverse kinematics, so leg trajectories could be planned systematically rather than tuned joint by joint.

{% include image-gallery.html images="images/dh.jpg, images/rand.jpg" height="400" captions="DH analysis for transformation matrix instantiation | note for DH parameter calculation" %}


On the software side, I deployed a ROS-based framework on an Ubuntu-booted Raspberry Pi to keep sensing, control, and testing modules organized, and wrote Python test scripts to validate servos and sensors during bring-up before attempting full locomotion. To de-risk gait development, I used MATLAB Simulink to simulate movement and navigation in a repeatable environment, refining control assumptions before deploying changes to hardware.

{% include image-gallery.html images="images/simulink.jpg" height="400" captions="Simulink locomotion simulation" %}

For power, I calculated a typical operating current of ~13.25 A and sized the system for roughly 22 minutes of runtime under expected load, which directly informed battery selection and the tradeoff between runtime, weight, and mechanical performance.

{% include image-gallery.html images="images/pwrcalc.jpg" height="400" captions="power analysis" %}

Then, I proceeded to write explorational scripts to practice coordinated gaits on the actual robot.

{% include youtube-video.html id="/XGnWq85dWcM" autoplay="false" %}
