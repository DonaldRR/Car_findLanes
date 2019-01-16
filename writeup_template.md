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

![alt text][rawLine]

The green lines drawn are lines of edges.


### Reflection

### 1. Modification on draw_lines() function

The final objective is finding the direction of two lanes line, i.e. drawing two long lines in the left and right. In the original solution, we get lines of edges, while including noises. To eliminate some lines, I use thresholding on the slope of lines. Here are rules for thresholding process.

- Lines lie on the left ROI have negative slope, otherwise positive. Others are eliminated.
- Absolute value of slope of all lines have to be greater than 0.5, i.e. at least 30 degrees to the horizon.

After that, we still get a bunch of lines, we need form a long line based on them. The strategy here is fitting a line with linear regression given Xs and Ys of endpoints of lines. And train two linear regreesors on both left and right lines. Then drawing fitted lines on the image. 

There is one more detail in such fitting process. Even after thresholding process, noise still exist. It can confuse the fitting process. To reduce the noise, longer lines get higher sample weights and shorter ones get lower weights. Thus the regressor would focus more on long lines which are more likely lines of lanes.

The blue lines below are resulting lane lines.

![alt text][line]

Combined with original image, it gives: 

![alt text][final]

### 2. Potential shortcomings with current pipeline

The first shortcoming is SHADE on lane road can introduce much noise. That can be shown with picture below:

![alt text][shortcom1]

In this image, green lines indicate lines of edges and red lines are final lane lines. It's clearly that, lots of noise are taken into account, as green lines in shade are considered. 

The second shortcoming is BRIGHT lane road makes gradient of color so low that edges of lane line is hard to detect, as shown below.

![alt text][shortcom2]

Only few short green lines is detected on the left yellow lane line, however, number of lines from the shade is much larger than that. Even loosing the thresholding in Canny() function which allows more edges to be considered, more noise is also included.

### 3. Possible improvements to pipeline

+ Masking

Despite clearing out area outside trapezoid, area between two lane lines are no necessary in this task. Here I can fill this triangular area black before finding lines.

+ Black out lines

It's intuitively that lines having small slopes are not lane lines. Here I draw those lines black and then detect lines of resulting image.



[grayScale]: ./writeup_images/gray_scale.jpg "Grayscale"
[blur]: ./writeup_images/blur.jpg "Blur"
[edges]: ./writeup_images/edges.jpg "Edges"
[mask]: ./writeup_images/mask.jpg "Mask"
[masked]: ./writeup_images/masked.jpg "Masked"
[rawLine]: ./writeup_images/raw_line.jpg "RawLine"
[line]: ./writeup_images/line.jpg "Line"
[final]: ./writeup_images/final_extend.jpg "Final"
[shortcom1]: ./writeup_images/shortcom1.png "ShortComing1"
[shortcom2]: ./writeup_images/shortcom2.png "ShortComing2"

