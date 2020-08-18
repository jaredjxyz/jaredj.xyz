---
layout: single
title: 'Programming a Real Self-Driving Car: Udacity SDC Nanodegree Capstone'
featured: true
date: '2017-10-02 23:50:00'
tags:
- udacity
- sdc
---

## [Github](https://github.com/CarND-Emoji-Team/CarND-Capstone)

## Introduction

All of the projects in the Udacity lead up to one final project. In this final project, you team up with up to 4 other people from the program and put your code on Udacity's real self-driving car.

## Parts

### Traffic Light Detection

This was the part I worked on. My team split this into two parts

1. Transform space. We were supplied the location of the traffic light relative to us. If you know the focal length and a couple other details about the camera, you can figure out which pixels represent the object if you know where in space the object is.
2. Classification. We needed to classify the traffic light as red, yellow, or green, so that we would know whether to go or not.

### Waypoint Following

The car needs a list of waypoints to follow. In this project, we're given a list of base way points and the position of the car, and we need to provide a list of waypoints ahead of us so that the car knows what to follow.

Once we know where the traffic lights are and whether they're red or green, the waypoint updater then cuts off the waypoints at red lights and extends the waypoints to green lights.

### Drive-By-Wire

The interface to the car gives goal speed and turning values and the drive-by-wire module is responsible for turning those into throttle and brake. Our team solved this using PID with the steering and throttle individually.

## Video

I was lucky enough to be one of the few to see the car run my team's code in person. Here's a video of it attempting one loop around.

<iframe width="560" height="315" src="https://www.youtube.com/embed/PX6_7RRYyM4" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>