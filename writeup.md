# **Finding Lane Lines on the Road** 

## Writeup 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[color_select]: ./img/color_select.png "Grayscale"

[blur_gray]: ./img/blur_gray.png "Grayscale"

[edges]: ./img/edges.png "Grayscale"

[masked_edges]: ./img/masked_edges.png "Grayscale"

[line_image]: ./img/line_image.png

[line_simple]: ./img/line_simple.png

[overlay]: ./img/overlay.png

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 

First, I converted the images from RGB space to HSV space, then I extracted yellow segments and white segments by using cv2.inRange() and mixed them as a mask image.
Second, I applyed Gaussian smoothing for the mask image.
Third, I applied Canny edge detection for it.
Fourth, I defined the region of interest and made the masked edge image by the region of interest mask.
Fifth, I applyed Hogh transform for it to get its lines.
Finally, I drow the lines on the original image.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function. I separated line segments by whether their slope are negative or positive, then I calculated the line's slope and intersept. I calculated medians of them. Because median is robust for outliers. 
By doing this, I can get 2 lines(left and right). Finally, I drow the lines.

The result images of each step of my pipeline are shown below.  

- Extracting yellow segments and white segments

![color_segment][color_select]

- Applay Gaussian smoothing

![color_segment][blur_gray]

- Apply Canny edge detection

![color_segment][edges]

- Masked by the region of interest

![color_segment][masked_edges]

- Apply Hogh transform to detect lines

![color_segment][line_image]

- Drawing single line

![color_segment][line_simple]

- Overlay lines

![color_segment][overlay]



### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would not working well when it's rainy, snowy and night.
The images would be so different from sunny day. My pipeline might have overfittedto 3 sample videos.

Another shortcoming could be not working if the image has no white or yellow line (For example, one lane road).
My pipeline extract yellow line and white line. So, if it's one lane road with no line, my program would not be working.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use a previous frame to find lanes in the next frame.
It suppose lanes don't change the positions rapidly. It may be good at the scene whose lane is not visible temporally.

Another potential improvement could be to extract road segments by using their color feature.
My pipeline extracted yellow and white segments. It needs lines.
But, if the program can extract road segments, it dosen't need lines.
So it can be used for one lane road.
