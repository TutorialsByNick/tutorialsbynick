---
layout: post
title: "Buying Robot Parts"
comments: true
author: Nicholas Day
email: true
category: "Building a Robot"
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/kZHaTGiakZM?start=8" frameborder="0" allow="autoplay; encrypted-media" style="display: block; margin: 0 auto; margin-bottom: 20px;" allowfullscreen></iframe>

Swerve drive is a fantastic omni-directional drive train. It can go in any direction at any time with full speed. Go ahead and watch the video above. I'll wait. 

Wasn't that amazing? A swerve drivetrain has 4 independent swerve modules that change the direction the wheel faces and the speed of the wheel at the same time. It allows for complex maneuvers like you saw in the video. I want to build a swerve drive so that I can understand how it works, what code is required, and because I've always wanted to build one. 

Honestly, making a artisan, hand-crafted swerve drive made from scratch is quite a daunting undertaking. The following major skills seem to be required:
* CAD 
  * Computer aided design software which lets the user model their design or _robot_ without having to draw lots of 3d models on paper
* Embedded programming
  * You may be familiar with traditional programming which focuses on things inside a computer, but embedded programming is used when programming a smaller computer called a microcontroller which is slower and less powerful, but has real time access to input and output to the real world like LEDs or switches or motors. 

Last year, I was on FTC Team 731 as the lead programmer. FTC, or First Tech Challenge, is a high school robotics sport that lasts for the latter half of the school year. Our robot had to be able to place these foam blocks in a vertical grid within an operator-controlled (called Telop, for 2 minutes) and autonomous portion (30 seconds, not very long at all!) of the match. I linked a video of our robot below. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/2zds6AWhhSI" frameborder="0" allow="autoplay; encrypted-media" style="display: block; margin: 0 auto; margin-bottom: 20px;" allowfullscreen></iframe>

During the competition, I spent most of my time trying to work through issues surrounding the control system and the lag that occurred when sending commands to the robot. This made it hard to achieve more accurate positioning. It was frustrating, but it's also part of the reason why I'm so inspired to take on this project so that I get some "real world" experience and a chance to apply some of the skills I learned.

Because swerve drive is a really challenging drivetrain to make from a mechanical and programming standpoint, I figured I would get my feet wet by starting with a mostly built robot robot kit, and learning a few things along the way. On a Pololu sale, I found this gem:

<iframe width="560" height="315" src="https://www.youtube.com/embed/bSA3A0wpirA" frameborder="0" allow="autoplay; encrypted-media" style="display: block; margin: 0 auto; margin-bottom: 20px;" allowfullscreen></iframe>

It's a robot kit with software already made to control most of it and a [tutorial](https://www.pololu.com/blog/577/building-a-raspberry-pi-robot-with-the-a-star-32u4-robot-controller) on how to build it. I liked the idea of using a Raspberry Pi as a high level controller that could handle regular computer programs and processing. It could host a web server and use a webcam with computer vision techniques to recognize items in the real world and send movement commands to the robot. It also would allow for any device with a web browser to control the robot like shown in the video. The microcontroller is a Atmega 32u4 8 bit microcontroller, which is like a regular computer processor but it's slower and more focused on the electronics control side.

I decided to get [these motors](https://www.pololu.com/product/3076) instead because they had a shaft on the end of the motor. That way I can install [this encoder](https://www.pololu.com/product/3081) on the back of the motor. Encoders measure the rotations of the shaft when it moves forward and backward. If you know the wheel circumference, you can determine the distance that the robot has traveled with it's measured rotations. You can also determine the speed of the robot by using the rate of rotation of the motor. Encoders make a lot of sense for my project because I want to accurately control the speed of motors and the autonomous functionality of the robot. 

For the Raspberry Pi, I chose to get the latest version (Raspberry Pi 3) instead because it would offer more processing power for computer vision tasks and machine learning if I need it.

My eventual vision for this project involves a Raspberry Pi and camera for sensing objects which communicates with the internet and controls the microcontrollers, multiple microcontrollers for controlling the motors and providing a high level motion control interface to the Pi. Oh, and the drivetrain would be swerve drive of course. :)

I'll try to post a build log of my efforts in a semi-tutorial fashion. Stay tuned as I write up more on how to build a robot!