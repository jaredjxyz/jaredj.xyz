---
layout: single
title: 'Traffic Sign Classifier: Udacity SDC Nanodegree Term 1 Project 2'
date: '2017-01-24 05:26:00'
tags:
- udacity
- sdc
---

## [Github](https://github.com/jaredjxyz/CarND-Traffic-Sign-Classifier)
## Introduction
This project was an introduction to CNNs in tensorflow. Udacity gives the student some suggestions on what a convolutional neural network looks like and then the student goes and implements that on their own


## My solution

Here's what my final CNN looked like. It was trained on the dataset provied my Udacity 

Input: 32x32x3 (a 32x32 pixel color image) Layer1: 2D convolution with an output of 28x28x6, and a pooling layer of kernel size 2x2 with a stride of 2 for an output of 14x14x6
Layer2: 2D convolution with output size 10x10x16, and a pooling layer with kernel size 2x2 for an output of 5x5x16
Fully Connected 0: Flatten layer 2
Fully connected 1: Matrix multiply with input 400 and output 120, then a relu activation
Fully connected 2: Matrix multiply with input 120 and output 84, then a relu activation
Output layer: Matrix Multiply with input 84 and output 43 (for 43 possible labels)

This was trained on the dataset provided by Udacity (https://d17h27t6h515a5.cloudfront.net/topher/2017/February/5898cd6f_traffic-signs-data/traffic-signs-data.zip) for an accuracy of 94.2% of the validation set