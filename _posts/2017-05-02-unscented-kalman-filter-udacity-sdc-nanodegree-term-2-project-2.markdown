---
layout: single
title: 'Unscented Kalman Filter: Udacity SDC Nanodegree Term 2 Project 2'
date: '2017-05-02 03:13:00'
tags:
- udacity
- sdc
---

## [Github](https://github.com/jaredjxyz/CarND-Unscented-Kalman-Filter)

## Introduction

We learned about Kalman Filters and Extended Kalman Filters in the [last lesson](http://ghost.jaredj.xyz/extended-kalman-filter-udacity-sdc-nanodegree-term-2-project-1/). Extended Kalman Filters have the problem where they are still linear - the jacobian is essentially a linear approximation. Motion, however, is rarely linear. An Unscented Kalman Filter attempts to fix that.

## CTRV Model

In the last project, we assumed the car had a constant velocity. This becomes inaccurate when the car is accelerating or turning. There are a few different models that can take into account acceleration, turning, and other motions. The one we use in this project is the CTRV model which stands for Constant Turn Rate and Velocity. The Unscented Kalman Filter will allow us to account for turning, where this model would screw up the Extended Kalman Filter

## Sigma Points

The reason we can only use linear functions in an Extended Kalman Filter is that it depends on keeping a gaussian disctibution for how sure it is of the points. When we apply the transformations that an Extended Kalman Filter uses, it turns that function into a non-gaussian distribution, which means that we may have two or more ideas of where the true value is.

Instead of applying our non-linear function directly, what an Unscented Kalman Filter does is is finds points that are representative of each of the variables we're changing and the gaussian function representing them. It then transforms those points, and from that transformation we can now create a new gaussian distribution. It's difficult to explain without a full lesson (you can find full lessons on Youtube if you're interested), but the basic idea is that this new gaussian is representative of your confidence in the new, non-linear function. This tends to work better than an Extended Kalman Filter in places where motion changes a lot.

## Video
<iframe width="560" height="315" src="https://www.youtube.com/embed/L8rUOcP5imE" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>

If you compare this one to the video in the previous lesson, you'll notice that the green triangles are much closer to the circle and less spread out than in the last lesson.