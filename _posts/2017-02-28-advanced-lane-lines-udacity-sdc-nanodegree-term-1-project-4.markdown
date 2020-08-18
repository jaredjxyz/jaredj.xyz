---
layout: single
title: 'Advanced Lane Lines: Udacity SDC Nanodegree Term 1 Project 4'
date: '2017-02-28 05:09:00'
tags:
- udacity
- sdc
---

## [Github](https://github.com/jaredjxyz/CarND-Advanced-Lane_Lines)

## Introduction

In project 1 of term 1, we made a pipeline that can detect lane lines, but only straight lane lines. In a real car, you need something more complicated to figure out exactly where the lane lines are. This project is an extension of the first project in term 1. In this project, we use perspective transforms and thresholding to fit lines to the lanes we see.


## The Pipeline
Here I will go through each of the methods we learned in this lesson and give an example of how we get from start to finish

We will start with our original image: 

![test2_original]({{ '/assets/images/2018/01/test2_original.jpg' | relative_url }})


### Color thresholding

We know that our lane lines will be one of two colors: yellow or white. We can use that knowledge to signal out only the yellow or white parts of the image. We say that if this part of the image is above a certain percentage of yellow, we make it white, and if it's below that, we make it black.

### Sobel Operator
Once we have the white and yellow parts of the image, can use the Sobel Operator to find edges. The sobel operator looks at a bunch of pixels and finds the gradient between them. In other words, it highlights the place where the color change, and highlights big changes in color more than smaller places. We know that the color is going to change a lot in out lane lines, so this will help them stand out.

After color thresholding and sobel operator, this is what the image looks like:

![test2_thresholded]({{ '/assets/images/2018/01/test2_thresholded.jpg' | relative_url }})

### Perspective Transform

In order to find curves to fit these lane lines, we want to be looking at them from above. There is a tool available with OpenCV to transform an image so that it looks like you're looking from another direction. Here's what the image looks like after a persepective transform:

![test2_warped_thresholded]({{ '/assets/images/2018/01/test2_warped_thresholded.jpg' | relative_url }})

From here, we try to fit two curves to the pixels in the right palce. This is the hard part. I made my pipeline look at the left and right sides of the pictures and find places with a lot of vertical pixels. I then used a sliding window to find the pixels above that, then adusted the sliding window to halfway between the mean of the new pixels and the mean of the old pixels.

Once we figure out which pixels to use for our lines, it's easy to fit a polynomial curve to them and then highlight the area between the two curves. Here's what it looks like after this process:

![test2_warped_thresholded_with_lines]({{ '/assets/images/2018/01/test2_warped_thresholded_with_lines.jpg' | relative_url }})

After we've done that, we undo the perspective transform that we did earlier so that the picture is in the same perspective as earlier.

![test2_thresholded_with_lines]({{ '/assets/images/2018/01/test2_thresholded_with_lines.jpg' | relative_url }})

If I then put the old picture back in, here's what it looks like

![test2_with_lines]({{ '/assets/images/2018/01/test2_with_lines.jpg' | relative_url }})

Now I do that for every frame of the video. Here's what it looks like:

<iframe width="560" height="315" src="https://www.youtube.com/embed/6B6QawlZBgI" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/LyacTp2JgEk" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>

