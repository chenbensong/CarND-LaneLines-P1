# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps.

First, I converted the images to grayscale.

Second, I applied Gaussian blur with kernel size 11.

Third, I used Canny edge detection to find edges.

Fourth, I defined a region of interest to concentrate on the region that should contain the lanes.

Finally, applied Hough transformation to remove noise (shorter lines) so the most possible lane lines remain.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first categorizing them into
left and right lines, averaging their slope and intersection parameters, and find the endpoints. Then I plotted
the two lines with adjusted accuracy.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the road is curved. My approach of averaging straight lines will make a "linear fit" to
the curve instead of reflecting the curved lanes.This is shown in the optional challenge video.

Another shortcoming could be that when one lane line is dotted and not clear enough, that line may not be detected for certain frames in the video.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to try to fit curves instead of always assuming lanes are straight. This is difficult and will require more complex math models on fitting.

Another potential improvement could be to use recent frames' lane detection to fill out the missing lane line in the current frame, to address very occassional missing detection problem. This should work because we know the lane won't disappear in a split second. We do need to be careful not to allow for going back to history for too long, as the live situation may change within a second or two (for instance, obstables or sunlight changes).
