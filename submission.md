# **Finding Lane Lines on the Road** 

### 1.Pipeline Description

My pipeline consisted of 7 steps. The first step is to read the raw image and convert the image to grayscale.

[//]: # (Image References)

[image1]: ./writeup_images/1.png "Original"

---
[//]: # (Image References)

[image1]: ./writeup_images/2.png "Grayscale"

---

The second step was to apply gaussian blur on the grayscaled image in order to smoothen the image (reduce unwanted noise) and detect better edges with canny edge detection algorithm, thereby helping detection of lane lines. By trial and error, I found the parameter sigma for Guassian blur to be '5'.

[//]: # (Image References)

[image1]: ./writeup_images/3.png "Gaussian Blur"

---
In the third step, I applied Canny edge detection over the entire image with the values of low and high threshold as 50 and 150 (obtained through trial and error in course.)

[//]: # (Image References)

[image1]: ./writeup_images/4.png "Canny Edge"

---
Before I extracted the lines in the image, I masked the region of interest in step 4, by specifying the vertices and drawing a polygon of 4 sides over the image as we know that the lane lines are often in the bottom of the image.

[//]: # (Image References)

[image1]: ./writeup_images/5.png "Region of Interest"

---
In step 5 I used hough transform to extract the the slope and coordinates of the lines detected in the image after it is masked. Multiple lines were detected for the same image.

[//]: # (Image References)

[image1]: ./writeup_images/8.png "Hough Transform"

---
In step 6, I categorized the lines based on their slope. Based on the sign of slope, I have divided the lines into two categories, the ones with +ve slope and the ones with -ve slope to distinguish between left and right lanes. In order to draw a single line on the left and right lanes, I modified the hough_lines() function by using the 'median of coordinates' to obtain final coordinates of lines on left and right side.

[//]: # (Image References)

[image1]: ./writeup_images/6.png "Hough Transform with median averaging"

---
In the final step(7), I overlayed the lines detected onto the original image and ran the algorithm over a video.


[//]: # (Image References)

[image1]: ./writeup_images/7.png "Final Image with lane lines"

---
### 2. Shortcomings with current pipeline

Using median to average the lines does not detect the entire line and often result in the line starting from the middle and not reaching complete end. 

The algorithm doesn't detect curved lines properly due to fitting of straight line

The region of mask and the parameters have to adjusted for different road types and camera angles


### 3. Possible improvements to pipeline

The coordinates can be recombined to get the maximum length line instead of taking median.

A nonlinear equation (quadratic or cubic or higher degree) has to be used to fit the curved path. Hough transform might not be useful in that case. 
