---
layout: single
title: 'PID Controller: Udacity SDC Nanodegree Term 2 Part 4'
date: '2017-06-06 05:53:00'
tags:
- udacity
- sdc
---

## [Github](https://github.com/jaredjxyz/CarND-PID-Control)

## Introduction

PID is one of the most common ways to get an object to get to the place you want it to go. With PID, all you need to do is give the algorithm the error (how far away you are from the goal) and tune 3 parameters to make it smooth. This is easy to implement, moves into position smoothly, and automatically compensates for cases where motor calibration is off (i.e. if you put weight on the end of a motor that's trying to lift something, the algorithm will naturally give more power to the motor).

## PID
In this project, we used PID to make a vehicle turn toward the center line on a track. Here's how each of the parts of PID relate to a car following a line:

P: Position. This is how far away the car is from the center line. We want to minimize this.
I: Integral. This is essentially how much time has been spent on one side of the track (with spending time far away from the track counting more than time close to the center). This will compensate in case the car has a left-turn or right-turn bias.
D: Derivative. This is the difference between the angle of the car and the angle of the line. We want the car to be going at the same angle as the line, so we try to minimize the difference.
The biggest advantage of PID is that it's easy to implement and works well in many scenarios. The biggest disadvantage is that it's reactive (as opposed to proactive), meaning that the car isn't planning ahead. This makes it hard to make a PID controller that will handle a car going excessive speeds. In my case I couldn't get the car going consistently over 120mph with a PID controller. For this project, Udacity provided a simulator that would give you the cross-track error (the distance from the center line) and I implemented the PID algorithm to make the car go around the track. 

## Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/dgIeP3ypdfE" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>