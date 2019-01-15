# **Finding Lane Lines on the Road** 

## Goals

* Make a pipeline that finds lane lines on the road
* Reflect on work in a written report

### Pipelines

My pipelines consist 5 steps. Each step will be manifestated below.

#### 1. Color Conversion

Original image has 3 channels, i.e. RGB. To make the problem easy, we change 3-channel images to 1 channel, grayscale image (shown below).

![alt text][grayScale]

#### 2. Blurring

In order to detect edges in a given image, gradient of color is used as metric. Pixels of high gradients usually indicate edges. However, despite edges of lane lines, other irrelevant edges can also be detected. To reduce those detectable edges, like flaws on road, blurring technique makes those edges blur and less detectable. Blurred image is shown below.

![alt text][blur]

#### 3. Detection of Edges

One important feature of lane line is its long edge in its direction. Retrieving all edges help us more focus on the edges not 
other details. Because edges matter in this task. Detected edges of image above is shown. White pixels are edges and black others.

![alt text][edges]

#### 4. Image Masking

Intuitively, the region of interest is where the lane lines lay on, almost the trianglar region of the bottom half of image. In this solution, instead of triangle, trapezoid is used as mask.

The first picture below indicat the trapezoid I used with bold white lines. The second picture is the image after masking. It is clear that, the task has became more simple.

![alt text][mask]

![alt text][masked]

#### 5. Line Detection

In an image, each pixel is denoted with its position X and Y and color. But color is not used in this part, so only discuss X and Y alone. It is easy to say which pixels form a line approximately with eyes, while it is not easy for computer only dealing with Xs and Ys. So we transform the image space to Hough space, in which, each pixel is denoted as a line. And one important feature is that, pixels in a line in image space intersect in Hough space. Each intersection means at least 2 pixels in a line. Thus, we use this trick to find lines in edges.



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


