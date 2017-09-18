# **Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


### 1. Description of the pipeline

My pipeline consisted of the following steps:	

* Read Image
* Gray Scale Image
* Apply Gaussian Blur to the image
* Apply the Canny Edge Detection Algorithm
* Select the region of interest 
* Apply Hough Transform the the region of interest
* Add the lines that were given by Hough Transform to the original image
* Show the image and draw the lines on it 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by performing the following:

For each line given by the hough transform step ( a line consist of two points (x1,y1) and (x2,y2)
* We compute the slope i.e (y2-y1/x2-x1)
* We group the points by the ones with a positive slope (left lane) and the ones with a negative slope (right lane)
* We eliminate any line with a high slope or a very low slope to reduce potential "noise" (slope is expected to be in [0.5, 2] range)
* We apply a polynomial fitting (a line is a polynomial of degree 1)
* We use the width of the image as a starting point to draw and we draw up to 40% of the image going up


### 2. Potential shortcomings with my current pipeline

* Curves won't be handle properly as we made the assumption that a lane is a rigid line (y = mx + b)
* Slope is expected to be in 0.5 and 2
* The region of interest could be wrong if the road is steep
* Parameters are tuned for the set of pictures provided. There is no guarantee that the pipeline would work for darker images or images with considerably different luminosity 


### 3. Possible improvements to my pipeline

* Assume a lane is a curve instead of a line using maybe a parametric equation of a curve
* Implement a smarter region of interest selection. We could be looking for a portion that looks like a road in the image instead of just a fixed frame
