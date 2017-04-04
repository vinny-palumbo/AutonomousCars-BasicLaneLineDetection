# **Finding Lane Lines on the Road** 

---

The goal of this project are the following:
* Make a pipeline that finds lane lines on the road


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./examples/gaussina-blur.jpg "Gaussian Blur"
[image3]: ./examples/canny-edges.jpg "Canny Edges"
[image4]: ./examples/canny-edge-mask.jpg "Canny Edges in Region of Interest"
[image5]: ./examples/hough-lines.jpg "Hough Lines"
[image6]: ./examples/single-solid-lane-lines.jpg "Single solid Lane Lines"
[image7]: ./examples/result.jpg "Result"

---


### Reflection

### 1. Describe the pipeline. Explain how I modified the draw_lines() function.

My pipeline consists of 6 steps: 
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

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:
* Separating the generated Hough lines with negative slopes (for the left lane) from those with positive slopes (for the right lane)
* Filtering out the lines with slopes that have outlier values
* Setting the slope of each of the left and right lane to the mean value of their respective lines' slopes
* For each of the left and right lane, drawing a line with the previously set slope that starts from the bottom of the image and extends out to the top of the region of interest.



### 2. Identify potential shortcomings 
* Crashes when no Hough lines generated in an image
* Hough Transform can't generate curved lines (eg: when the car is in a curve)
* Can't detect lane lines if outside the region of interest (eg: when car is switching lanes)
* Algorithm might get confused if there is something in the region of interest (eg: cars, pedestrians, shadows, etc.)
* Can't predict where the lane lines should be if there are no lane lines


### 3. Suggest possible improvements 
* Catch error when no Hough lines are generated for either the right or left lane
* Add color detection to only detect lines that are white or yellow
* Give bigger weight to longer lines and calculate a weighted-average slope, to filter out noisy Housy lines that bias the average slope