#**Finding Lane Lines on the Road** 

##Writeup Report

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[image1]: ./images/out_solidWhiteCurve.jpg "Detected Lines"
[image2]: ./images/full_extent_solidWhiteCurve.jpg "Full Extent Lines"

---

### Reflection

###1. Pipeline description.


My pipeline consisted of the next steps. First, I converted the images to grayscale using the helper function *grayscale()*,
then I defined three parameters (**kernel_size**, **low_threshold** and **high_threshold**) that was used on the helper
functions *gaussianblur()* and *canny()*. Then I blurred the image with the function *gaussianblur()* and with the blurred
image, I applied *canny()* to detect edges on the images. Next, I defined the vertices of the polygon that masks the images
and then I applied the helper function *region_of_interest()* to keep the region defined by the polygon. Then I defined the
parameters (**rho**, **theta**, **threshold**, **min_line_length**, **max_line_gap**) used on the helper function
*hough_lines()* that finds the Hough lines and draws on the image. Finally, I used the helper function *weighted_img* to
overlay the original image with the image with the lines.


Original image with the detected lane lines of the road:
![image with lines][image1]


In order to draw a single line on the left and right lanes, I modified the *draw_lines()* function as follows. First of all, I
defined four lists to store all the slopes (**rm** and **lm**) and centers (**rc** and **lc**) for the left and right lines.
With all the slopes and centers of the left and right lines, I calculate the average of the slopes and the (x, y) centers
coordinates for all lines. Using the average value of slope and center, I extrapolated the line using the equation y-y' = m(x-
x') and the extremes of the polygon that masks the image to find the x coordinates and finally draw the fully extent of the
line lanes.


Original image with the average/extrapolated lines:
![image with lines2][image2]



###2. Potential shortcomings

One potential shortcoming would be what would happen when the road doesn't have a totally flat asphalt creating new lines and
make the calculation of the lane lines difficult. 

Another shortcoming could be when the road have sharp curves. The lane lines on the road has to be found on a smaller mask.


###3. Possible improvements

A possible improvement would be to impose another condition to *draw_lines()* function to filter de horizontal lines that
could apper on the road and disturb the lane lines detection.

Another potential improvement could be to create a more refined polygon to mask the image of the detected lines.
