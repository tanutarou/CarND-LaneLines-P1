# **Finding Lane Lines on the Road** 

## Writeup 

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

My pipeline consisted of 5 steps. First, I converted the images from RGB space to HSV space, then I extracted yellow segments and white segments by using cv2.inRange() and mixed them as a mask image.
Second, I applyed Gaussian smoothing for the mask image.
Third, I applied Canny edge detection for it.
Fourth, I defined the region of interest and made the masked edge image by the region of interest mask.
Fifth, I applyed Hogh transform for it to get its lines.
Finally, I drow the lines to the original image.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function. I separated line segments by whether their slope are negative or positive, then I calculated the line's slope and intersept. I calculated medians of them. Because median is robust for outliers. 
By doing this, I can get 2 lines(left and right). Finally, I drow the lines.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
