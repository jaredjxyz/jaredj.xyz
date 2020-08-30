# Kidnapped Vehicle (Particle Filter): Udacity SDC Nanodegree Term 2 Project 3

## [Github](https://github.com/jaredjxyz/CarND-Kidnapped-Vehicle-Project)

## Introduction

Kalman Filters work great, but can be difficult to implement. What if we want an easy way to figure out what the robot is doing without having to figure out a model for it? This is where particle filters come in.

## Kidnapped Vehicle

The premise behind this project is that there is a vehicle that has sensors on it, and you need to figure out where it is.

## Particle Filter

To figure out where the vehicle is, or 'localize' the vehicle, a particle filter follows the following steps:

1. Place a bunch of virtual robots around the map in random positions.
2. Take measurements with our actual robot.
3. Compare the measurements of our actual robot with the measurements that we think each of our virtual robots would have taken
4. If this virtual robot's measurements are similar to what the physical robot's measurements are, we know that that virtual robot is much more likely to be in the same positon as our physical robot.
5. Make a new set of virtual robots, making more robots close to the virtual robots with high probability of being correct.
6. Move the physical robot, and simulate movement for each of the virtual robots in the same motion. Then repeat the entire measurement process.


This will eventually give you an estimate for the robot's location. This can be extended to velocity and acceleration as well.

## No Video This Time

Unfortunately because I was in the first cohort, Udacity did not have a vidualizer ready for this project.
