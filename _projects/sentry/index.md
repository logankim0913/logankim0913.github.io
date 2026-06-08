---
layout: post
title: Face Tracking Turret
description: Built a 4-DOF face-tracking turret with OpenCV-based detection, ESP32 servo control, and PD control tuned for smooth real-time tracking at ~30 FPS.
skills: 
  - Computer Vision
  - Embedded Systems
  - Control Systems
  - Mechatronics

main-image: /thumbnail.jpg
---

## GitHub Source
{% include github-repo.html repo="logankim0913/face-tracking-turret" %}

## Project Overview
This project is a 4-DOF face-tracking turret that detects a person's face and moves its joints in real time to keep the target centered in view. A small Raspberry Pi camera v1.3 is used to capture video, and the Raspberry Pi 3 processes the videostream to control the turret servos via ESP32.

## Showcase

{% include image-gallery.html images="images/turret.jpg" height="400" captions="hardware structure of the turret: composed of 5 DOF turret (one joint is completely locked), Raspberry Pi 3B+ with camera, ESP32, and breadboard for wiring"%}

It's actually quite a bit of time since I got into the concept of "face tracking." It was my introduction to computer vision, which seemed like a magic to me (still is). My first objective was to move the SG90 servo from the Arduino kit by moving my face across the webcam.

And then I wanted to build the actual movable joint that can take that tracking motion one dimension higher; hence the turret. It has a relatively simple structure with 5 revolute joints, composed of MG 996R servos, and 5 VDC supply to power up the servos. 

With the mechanical side roughly working, the rest of the project became a software handoff problem: the `pi_face_tracking.py` script starts the vision pipeline, finds the face position from the camera feed, and sends target movement commands over serial, while the `turret_servo_control.ino` file on the ESP32 listens for those commands and turns them into servo motion.

{% include image-gallery.html images="images/pipeline_diag.png" height="400" captions="diagram of the system pipeline"%}

I was only familiar with OpenCV's HaarCascade model for face detection, but I soon realized that its face detection rate is horrendous.


{% include youtube-video.html id="TSN5yqj1AkM" autoplay="false" %}
As you can see, the HaarCascade-base face detection has high frame speed, but the accuracy is really terrible. So, I explored more modern face detection model: Yunet. It was more resource-intense than HaarCascade but still light enough to run without much issues:

{% include youtube-video.html id="M6DuHUNKxYM" autoplay="false" %}
I was very surprised at the accuracy improvement compared to HaarCascade, albeit the fps is noticeably lower. Since it was practically impossible for the turret to track my face with HaarCascade, I tested the turret tracking with Yunet:

{% include youtube-video.html id="734P45mJgzk" autoplay="false" %}
It came out pretty nicely. The wires are messy, and the build quality is admittedly clumsy; a quick design for pcb will make it far more delicate and robust (the turret killed its own wiring a few times by slamming into them).
