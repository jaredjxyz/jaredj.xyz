# Semantic Segmentation: Udacity SDC Nanodegree Term 3 Project 2
## [Github](https://github.com/jaredjxyz/CarND-Semantic-Segmentation)

## Introduction

Detecting the boxes surrounding an object is something that works well in certain circumstances, but sometimes you need a higher level of precision. What if you could label each pixel as the type of object it is a part of? That's where semantic segmentation comes in.

## Fully Convolutional Neural Networks

In a normal convolutional neural network, we usually have two parts. The first part is convolutional. This part recognizes shapes. The second part does the dirty work of labeling that shape as one (or one of many) label.

In a fully convolutional network, we don't have that second part. Instead, after the convolutional part is done, we then reverse the convolutions in order to bring the image back to its original size. This allows us to label each pixel and to keep the information about where in an image each part was.

## Examples

You can see examples from the final output of my project [here](https://github.com/jaredjxyz/CarND-Semantic-Segmentation/tree/master/runs/1504486156.0100474)
