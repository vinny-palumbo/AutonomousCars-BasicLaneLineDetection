# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](https://www.udacity.com/course/self-driving-car-engineer-nanodegree--nd013)

<img src="laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

### Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project, we will detect lane lines in images/videos from the front camera of an autonomous car using Python and OpenCV.

--- 
### Pipeline

My pipeline consists of the following steps: 
* Convert the orignial images to grayscale. (Using the OpenCV library)
    ![alt text][image1]
* Apply Gaussian smoothing, which is essentially a way of suppressing noise and spurious gradients by averaging. A larger kernel-size implies averaging, or smoothing, over a larger area. (Using the OpenCV library)
    ![alt text][image2]
* Apply Canny Edge Detection, which essentially detects points where neighbouring pixels have a big value difference. (Using the OpenCV library)
    ![alt text][image3]
* Define a four-sided polygon to only keep the Canny edges in the region of interest, where there could be lane lines.
    ![alt text][image4]
* Use Hough Transform to find lines from the Canny Edges in the region of interest. (Using the OpenCV library)
    ![alt text][image5]
* Generate single solid lane lines by averaging/extrapolating the Hough lines
    ![alt text][image6]
* Combine the original images with their generated single solid lane lines
    ![alt text][image7]
    
    
[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./examples/gaussina-blur.jpg "Gaussian Blur"
[image3]: ./examples/canny-edges.jpg "Canny Edges"
[image4]: ./examples/canny-edge-mask.jpg "Canny Edges in Region of Interest"
[image5]: ./examples/hough-lines.jpg "Hough Lines"
[image6]: ./examples/single-solid-lane-lines.jpg "Single solid Lane Lines"
[image7]: ./examples/result.jpg "Result"

