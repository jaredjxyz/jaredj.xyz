---
layout: single
title: 'Extended Kalman Filter: Udacity SDC Nanodegree Term 2 Project 1'
date: '2017-04-18 03:23:00'
tags:
- udacity
- sdc
---

## [Github](https://github.com/jaredjxyz/CarND-Extended-Kalman-Filter)

## Introduction

From sensors, you tend to get a lot of noisy data. When a sensor tells you that you're in one place one second and in another place another second, you have to decide which ones is right. This is where a Kalman filter comes in.

## Kalman Filters

A Kalman Filter keeps track of confidence levels in measurements. Usually you have two parts: A model of what should be happening, and the data from the sensor on what the measurements actually are.

Take, for example, the situation where the sensor is getting data every second. At the first second, it says an object is 2 meters away, and at the second second, it says the object is 3 meters away. Your model might predict that the object will be 4 meters away at the third second. What happens, then when the third second comes and the sensor says the object is 4.1 meters away? Do you trust the sensor, knowing that the sensor could be slightly off, or do you trust your model, knowing that your model could be slightly off? A Kalman filter will figure out which one to trust more and give a value that's usually somewhere between the sensor value and your predicted value.

## Extended Kalman Filter

The normal Kalman filter has a problem where it predicts things linearly. This means that, for example, at time t0 an object is 1 meter away, at t1 the object is 4 meters away, and t2 the object is 9 meters away, that it will have a hard time predicting that the next object will be 16 meters away. Extended Kalman Filters were created to help alleviate that. With an extended kalman filter, you can use a nonlinear function to model the behavior you expect. 

Unfortunately, thanks to the way Kalman filters use variances, it's not as easy as sticking the function in and being done with it. You have to use the jacobian matrix for the function, which is a matrix with every possible partial derivative. This will approximate the function as a linear function and is often a good enough approximation to keep estimate good.

## Sensor Fusion

The two parts of a Kalman filter, the data and the model, can be extended with multiple sensors. The model will stay the same, but we can update the data from multiple sensors together.

For this project, we emulated the data from a lidar and a radar. There are some key differenced between the two. A lidar will only directly give you position. If you want to figure out how fast an object is going, you have to take two measurements at two different times and figure out the difference between those two measurements, then divide that by the time between the two measurements. A radar, on the other hand, can directly measure speed. This means that when you're updating the data with the radar, you can give speed directly instead of looking at your model to determine speed. A radar has the drawback of being noisier than a lidar, so the data is going to be less consistent. If we use these two together, we can get a better idea of what the truth is. The filter will now figure out how confident it is in the model, the lidar, and the radar individually, and output one value that's a compromise between the three.

## Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/mJoeym6BnqU" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>

Here's a video of the kalman filter working. The red dots are lidar measurements, blue are radar measurements, and green is where the EKF thinks we are.