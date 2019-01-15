# **Finding Lane Lines on the Road** 

## Goals

* Make a pipeline that finds lane lines on the road
* Reflect on work in a written report

### Pipelines

My pipelines consist 5 steps. Each step will be manifestated below.

**1. Color Conversion**

Original image has 3 channels, i.e. RGB. To make the problem easy, we change 3-channel images to 1 channel, grayscale image (shown below).

![alt text][grayScale]

**2. Blurring**

[grayScale]: ./writeup_images/gray_scale.jpg "Grayscale"
[blur]: ./writeup_images/blur.jpg "Blur"
[edges]: ./writeup_images/edges.jpg "Edges"
[mask]: ./writeup_images/mask.jpg "Mask"
[masked]: ./writeup_images/masked.jpg "Masked"
[line]: ./writeup_images/line.jpg "Line"
[final]: ./writeup_images/final_extend.jpg "Final"

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)



---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...


