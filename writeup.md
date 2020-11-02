# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

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

The procesing pipeline consisted of 5 steps.

1st step: Conversion to grayscale

2nd step: Applied an gaussian filter to smooth the image and reduce the influence of noise and order higher frequency elements on the image

3rd step: Canny edge detection: Used to extract the edge in the image. It uses two paremeters, low threshold and high threshold to define which trasitions in the gradient will be considered as valid edges

4th step: Adjusting the ROI, region of interest, in order to focus the line processing to the region where we expect to find the ranes

5th step: Used the Hough transform to find which edge are part of an line. As part of this function the method draw lines was used to show theses lines over the input image and extrapolate then to the full length of the ROI. To do that we used the line slopes to classify if the points were from the left lane or right lane. Given the line equation, y = ax + b, a minimum square regression was used on the points for each side to get the line parameters, a and b, and draw the lines to the full extent of the image. 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline

One potential shortcomings of this pipeline is regarding the fixed position of the ROI and the possible presence of other vehicles over the lane marking, making the detection to blink. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use the fact that the frames are temporally conected and that the properties of the lane has to be mantained over subsequent frames. This assumption could be used to make the detect more stable and retain its properties even on occlusions of subtle changes of the light conditions. 