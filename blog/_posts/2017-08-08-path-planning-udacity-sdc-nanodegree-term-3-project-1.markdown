---
layout: single
title: 'Path Planning: Udacity SDC Nanodegree Term 3 Project 1'
date: '2017-08-08 04:13:00'
tags:
- udacity
- sdc
---

## [Github](https://github.com/jaredjxyz/CarND-Path-Planning-Project)

## Introduction

In the MPC project we made a car follow a predefined path. In order to do that, though, the car needs a path to follow. In this project we made a smooth path for the car to follow and made it avoid other cars while keeping the correct speed and doing everything smoothly.

## The Simulator
This simulator works in a simple way. Every .02 seconds, the car moves to the next dot, so we then know exactly where the car is going to be in the next position.

## Logic
- If there is not another car in front of our current car, speed up to the max speed (45mph)
- If there is another car in front of our car, change lanes if possible, and if not, slow down to that car's speed until there is a lane available or until that car is going faster than our top speed.

## Smoothness
- Making a smooth line between waypoints: I used a spline library here. This library creates one smooth path through any points yoyu give it. On each calculation, the car makes a 9-point spline (with the 4 waypoints behind it, the 4 in front of it, and the closest one). It then uses that spline as a reference for where it should be.
- Speeding up smoothly. This is just a matter of slowly increasing velocity. We are increasing velocity at a rate of 2.5m/s^2, or .05m/s per .02s increment.
- Changing lanes smoothly. I decided to do this with a method called the Jerk-Minimizing Trajectory. We take the position we're at and find the trajectory that gets us from the lane we're in to the lane we want to be in that reduced jerk the most.
- While turning, there is extra jerk, so when calculating how fast to change lanes we also take into account the jerk from turning within the road.

## Feedback from Reviewer

I got some great feedback on this project that I wanted to share here

`Greetings Udacian,
Congratulations :star:
I must applaud this great work and I will say I really like the structure of the code and the documentation. This is a clear master-piece and deserves an acknowledgment. Please keep up the great work and remain brilliant.`

## Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/Y3wUAxTGsvk" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>