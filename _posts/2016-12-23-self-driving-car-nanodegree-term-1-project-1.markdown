---
layout: single
title: 'Finding Lane Lines: Udacity SDC Nanodegree Term 1 Project 1'
date: '2016-12-23 05:15:00'
---

## [Github](https://github.com/jaredjxyz/CarND-Finding-Lane-Lines)

## Background
I was picked when I was a senior in college to be one of the first 500 people in the first cohort of Udacity's Self-Driving Car Nanodegree. I was told later that I was picked because I had taken many online classes before and that not many people applied to take the nanodegree while simultaneously taking college courses.

## Introduction
This project is an introduction to OpenCV. The goal is to find lane lines on a video feed of a car driving on a highway

## Finding Lane Lines

### CV Algorithms
In order to finish this project, we were taught some classical computer vision techniques, such as:

#### Canny Edge Detection
This algorithm finds where edges in the picture might be, and brings them back as a list of lines. Parameters one might adjust include how long the minimum and maximum lines must be and how sensitive the algorithm is to deciding whether something is a line or not.

### Hough transform
Hough Transform is another name for taking lines in x,y coordinate space and turning them into r, theta coordinate space. From here, we can easily find lines that are close to each other and going the same direction, so that if we have many similar lines from the output of the canny edge detection, we can combine those into one line

### Pipeline
From picture to video, here's what my final pipeline looks like:

1. Greyscale the image
2. Gaussian blur the greyscaled image, with kernel size 5
3. Apply canny edge detection with a low threshold of 0 and a high threshold of 200
4. Apply a mask to the places where we expect the road might be.
5. Use hough transform to find lines, with a minimum line length of 100 pixels and maximum gap between lines being 100 pixels as well.
6. Split the lines into two groups: the lines with positive slope (left lines) and the lines with negative slope (right lines)
7. Find the standard deviation of each set and filter out any lines not within one standard deviation
8. Find the mean line of all remaining lines. This is our new line.

<img src={{ '/assets/images/2017/12/drawnlines1.png' | relative_url }} style="width:50%;"></img><img src={{ '/assets/images/2017/12/drawnlines3.png' | relative_url }} style="width:50%;"></img>

### Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/qtWZ4ueGL8g" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/tCgqcR-FB2U" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/RYxGdt_Y6Cs" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SP8R8b3w1Ws" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>
