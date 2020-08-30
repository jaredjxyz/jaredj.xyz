# MPC Controller: Udacity SDC Nanodegree Term 2 Project 5
## [Github](https://github.com/jaredjxyz/CarND-MPC-Project)

## Introduction

When humans drive, we don't just look to see how far away from the center of the lane we are and how close to the speed limit we are. We look ahead and slow down if there's a sharp corner coming up, and we try to do so smoothly. When coming out of a turn, we try to slowly bring the steering wheel to its desired position. And we do so differently depending on if we have a sports car or SUV. Model Predictive Control attempts to replicate this behavior.

The idea is that with a Model Predictive Controller, we look ahead a certain distance and figure out, knowing how quickly we can accelerate and how much we can turn, what the best possible way to get there is. After we have a plan for how to accomplish our goal, we then take the first step, and then recalculate before sending the car another direction.

## Model...

A model, in this context, is the computer's idea of what the car can do. A simple model could assume that the car will never slide and will figure out how much the car will turn when we turn the wheels a certain amount and go a certain distance. A more advanced model will take into account maximum acceleration, maximum grip, and take into account delays.

## Predictive...

After we have an idea of what our car will do, we then can take a set of instructions over time and estimate what the car will do if we give it those instructions. The better our model is, the better our prediction is and the better our prediction is, the more accurate our trajectory will be.

## Control

Once we have the equation for what the car will do given any set of instructions, we then can use an optimizer tool to figure out the best set of instructions to accomplish our goal. We can also give different weights to multiple goals, such as telling the car to follow a line, but prioritize smoothness over being close to the line, or to prioritize minimal acceleration over being close to the speed limit.

## In This Lesson

The model keeps track of 8 variables:

x: the x position of the car, in relation to the map
y: the y position of the car, in relation to the map
psi: the orientation of the car in relation to the map
v: the velocity of the car, in meters/second
cte: the cross-track error between the car and the middle of the map
epsilon: the difference between the angle of the car and the angle of the track
delta: the amount that the car should be turning
acceleration: the amount of throttle the car is putting on.
These are calculated at each step in .1 second intervals for the next 20 intervals, so the car can plan ahead for the next two seconds. I tried .5 second intervals, but the car just didn't update fast enough.

In order to figure out where the car has to go, I first convert the global coordinates given by the map into local coordinates to the car. The idea behind this is that the local coordinates are going to have lower numbers and therefore it's less likely to have inaccuracies due to any conversion imprecision.

The program has a simulated 100ms latency, to account for the fact that in the real world, readings aren't going to come instantly. In order to combat this, I made it so that the time interval between the dots it predicts is low. The more frequently we're calculating the things directly ahead of us, the better our accuracy is going to be for the things directly ahead of us.

## Video

<iframe width="480" height="270" src="https://www.youtube.com/embed/B1sXaZ1Z6js" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
