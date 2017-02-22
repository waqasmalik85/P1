#**Finding Lane Lines on the Road**

##Project writeup



---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of following steps:-
1. Gray scalled the images
2. Applied Gaussian blur
3. Used Canny edge detection algorithm to identify the edges
4. Cropped the relevant region of the images with only road in it
5. Applied Hough transform to identify lines


In order to draw a single line on the left and right lanes, I modified the draw_lines() function in following ways:-
1. A slope threshold was set to discard lines other than the ones from the lane markings
2. Length of each line was estimated to give higher weightage to the points belonging to a longer line
3. Weighted linear regression was applied to the points to estimate the slope and intercept of the resulting left and right line
4. A buffer of last 10 slopes and intercepts was kept and mean slope and intercept was used to draw the lines at any given time
5. Left and right lines were drawn from bottom till the visibe road surface





###2. Identify potential shortcomings with your current pipeline


I first tried the linear kalman filter to smooth the slope and intercepts but it didn't show good results as I wasn't using process noise matrix 'Q'

I ended up using a buffer of size 10 to keep past slopes and intercepts and use their average to plot the lines. In case of sudden change in the car trajectory there would be a latency of upto 10 measurements to correct the lines again





###3. Suggest possible improvements to your pipeline

A possible improvement would be to use a Kalman filter to smooth the slopes and intercepts of the lines. Moreover Yaw rate of the car could be used to compensate for changing slope and intercepts
