---
layout: post
title: AI Vision Autonomous Wheelchair
description: Developed a ROS1-based autonomous wheelchair navigation system with YOLOv8 vision, RGB-D sensing, and Gazebo simulation, while redesigning onboard power distribution and integrating embedded compute on a Quantum Q6 Edge platform for real-time, crowd-aware mobility.
skills: 
  - Computer Vision
  - Linux (Ubuntu)
  - ROS
  - Gazebo Simulation
  - Embedded Systems

main-image: /engine_cover.jpg
---

## Project Overview
As part of the college capstone program, I worked for Cyberworks Robotics to rework the autonomous wheelchair platform built for real-time, crowd-aware navigation in shared indoor spaces. The project was focused on developing a binary heuristics for the wheelchair's autonomous navigation stack to decide whether it is safe for the wheelchair to proceed or not. My work focused on developing the perception pipeline from crowd detection to avoid decision(i.e. stop navigation temporarily) and integrating the software stack with the physical wheelchair.

{% include image-gallery.html images="images/diagram2.png" height="400" captions="diagram for system overview"%}


## Showcase
{% include youtube-video.html id="dpvz9xpOyQI" autoplay="false" %}
On the software side, I helped design and validate a ROS1-based pipeline that combined YOLOv8 object detection, OpenVINO inference, RGB-D sensing, TF transforms, and custom binary heuristics for crowd-aware navigation decisions. This includes writing ROS nodes that set up ROS topics to establish communication channel between sensors and YOLOv8 model for pedestrian recognition, outputting the binary flag for avoid decision, and forwarding motor commands to Arduino.

The validation of the pipeline was done entirely in Gazebo with PedSim to simulate how the autonomous navigation logic behaves in the presence of spawned pedestrian entities.

{% include image-gallery.html images="images/demo.png" height="400" captions="demo showing the entire software pipeline running in Gazebo simulation; it shows the binary flag for avoid decision, SLAM in place with LiDAR, and Gazebo simulation environment with spawned wheelchair and pedestrian entities"%}

On the hardware side, I redesigned and rewired onboard power distribution system to supply power from the 24 V battery rail to sensors and computing hardware. While the wheelchair is a proprietary product from a 3rd party vendor, it is quite challenging to infiltrate its native firmware to overwrite the motor signal externally. Instead, I designed a simple digital-to-analog conversion circuit to translate the PWM input from Arduino Mega to analog signal that the wheelchair's motor controller recognizes as a valid joystick command.  


{% include image-gallery.html images="images/custom_pcb.jpg, images/pcb_sch.jpg" height="400" captions="signal conversion board with Arduino Mega | schematic for signal conversion circuit"%}

{% include image-gallery.html images="images/powerdist_diagram.jpg, images/wheelchair.jpg" height="400" captions="hardware diagram for power distribution | wheelchair during assembly and testing"%}

Unfortunately, the hardware system is not fully functional to boot up the software stack; the hardware demo couldn't be made.There was a short in the power distribution while I crimped wires together, and thus not all peripheral devices were powered up safely. As a result, everything is tested on the Gazebo simulation, so the next step is to resolve the hardware issue and conduct real-world testing.
