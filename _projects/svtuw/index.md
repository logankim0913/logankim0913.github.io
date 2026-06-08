---
layout: post
title: Solar Vehicle Power Board
description: Designed a high-voltage battery control and power distribution PCB implementing contactor and precharge control, and protected power delivery for a solar race car.
skills: 
  - analog circuit design
  - power electronics
  - schematic layout
  - PCB design
  - embedded systems

main-image: /svtuw.jpg
---

## Project Overview
As an Electrical Engineer on the UW Solar Vehicle Team, I worked on the power electronics that bring the solar car to life. My work centered on two boards: a high-voltage battery board that safely energizes the car from its 126 V nominal main pack, and a 24 V power distribution board that feeds power to the rest of the car's subsystems. Since this is a high-power, safety-critical system, the focus was always on doing it safely, reliably, and in a way the team could actually test before trusting it on the car.

{% include image-gallery.html images="images/image.png" height="400" captions="the power electronics boards I designed for the solar car"%}

## Showcase
The first board is the high-voltage battery board. Connecting a 126 V pack straight to the car is a great way to fry something, so the board uses a precharge sequence to limit inrush current before fully energizing the system. It also includes a current-measurement shunt to keep an eye on what's happening during startup, and the whole switching sequence is managed by STM32-based logic that drives the relays in the right order.

{% include image-gallery.html images="images/hv_battery_board.jpg" height="400" captions="high-voltage battery board that safely energizes the car from the 126 V main pack"%}

The second board is the 24 V power distribution board, which I designed in KiCAD. It takes power from the battery and routes it out to eight independent subsystems across the car. I laid it out as a 4-layer PCB and sized each trace according to the load current it was expected to carry, so the board stays organized and doesn't cook a trace under real operating conditions.

{% include image-gallery.html images="images/PowerDistBoard.png" height="400" captions="KiCAD layout of the 24 V power distribution board: a 4-layer PCB feeding 8 independent subsystems"%}

Before committing anything to a final board, I simulated the key circuit behavior in LTspice and then built a breakout board to actually test the power source selection logic. This is where it got interesting: during testing I noticed a leakage current from the secondary source that caused a small voltage sag at the output when the relay closed. I went back into LTspice to dig into it, found the root cause, and fixed the design.

{% include image-gallery.html images="images/breakout_board.jpg, images/breadout2.jpg" height="400" captions="breakout board for testing the power source selection logic | another breakout board printed for testing STM32"%}

The video below shows one of those source-selection tests, checking whether one voltage source is correctly prioritized over the other when the relay closes.

{% include youtube-video.html id="o9TH71AT8ww" autoplay="false" %}

Overall, this project gave me a ton of hands-on practice connecting schematic design, PCB layout, simulation, and real-world testing—especially the part where the bench results don't match the simulation and you have to figure out why.
