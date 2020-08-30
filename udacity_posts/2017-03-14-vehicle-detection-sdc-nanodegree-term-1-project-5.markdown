# Vehicle Detection: Udacity SDC Nanodegree Term 1 Project 5

## [Github](https://github.com/jaredjxyz/CarND-Extended-Kalman-Filter)

## Introduction

Figuring out where cars are in a picture is less easy than it sounds. First, you need a classifier that can correctly figure out what is and is not a car. Second, you have to figure out where those cars are in a way that is both accurate and computationally inexpensive. This is what we learned in the fifth project of the SDC Nanodegree.

## Pipeline

This particular project did not have a lot of leeway for how to complete it. Here is the pipeline Udacity suggested that I also used:

### Histogram of Oriented Gradients

This is an algorithm that will figure out how the color is changing in each part of an image and by how much is that color changing. In the pictures below, the gradients and their magnitudes are represented by white lines in a black box. The algorithm separates the picture into smaller boxes and figures out the gradient for each box. You'll notice that the lanes are represented well by gradients of approximately the same angle as the lane.

![hog_examples]({{ '/assets/images/2018/01/hog_examples.png' | relative_url }})

### Support Vector Machine

An SVM is a machine learning algorithm that takes in a list of features and classifies them. In this case, each of the features was the output of the histogram of oriented gradients. An SVM can be used in many of the same ways as a neural network, without having to worry about layer sizes. It can be customized with different kernels to fit more complex data. It can also be much quicker to train than a neural network.

In my training set, I used around 60,000 images of cars and not cars.

### Sliding Window

After we have an SVM that will classify a car consistently, we can use a sliding window method to figure out where in the image the car is.

The idea is simple: We have a classifier that can figure out whether an image is a car or not. We then take that classifier and run it on various parts of the image. Because the car could be at any distance, we also take different sized samples and run the classifier on them.

![sliding_window_examples]({{ '/assets/images/2018/01/sliding_window_examples.png' | relative_url }})

### Hotboxes

After we've run the sliding window algorithm, we now have a bunch of boxes that probably have a car in them. We now need to take those boxes and figure out which ones are accurate. We can do that by finding the areas where lots of boxes intersect. We call this method 'hotboxes'.

![hotbox_examples-1]({{ '/assets/images/2018/01/hotbox_examples-1.jpg' | relative_url }})

## Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/mPWucgykBWA" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>
