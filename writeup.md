# **Finding Lane Lines on the Road** 


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflection in a written report

---

### Reflection

### 1. Pipeline Description

My pipeline consisted of 6 steps. 

1. Grayscaling. I converted the images to grayscale, using the cv2.cvtColor function with the cv2.COLOR_RGB2GRAY as parameter. For another usage this function can also convert the RGB-image to GBR(which i will use for cv2.imwrite later),HSV... after this i used the gaussian-blur-function to smooth the grayscaled image.

2. Edges detection. I used the Canny-filter to find out the edges(horizontal and vertical) of the images. One important thing to do is, watch the output and adjust the threshold for detection.

3. Find region of interest and mask. I tried to find out the vertices of interesting region of images. For straight and smooth driving, it seems that the vertices of the images have only tiny difference. Then i applied mask to images to get the region that mainly include the lanelines.

4. Line detection and drawing. I used cv2.Hough_LinesP to detect the lanelines in image with tuning parameters and draw_lines function to draw the lines on a new line image. I modified the draw_lines() function several times. The first time i was trying to get the points and divide them into left and right line groups with the slope condition. Then i could use cv2.fitLine() function modify the left and right lanelines and draw them according to the boundary and the vertices of images. It worked pretty well on image processing. But when i applied it to videos, problems came out that in some frames the detection went wrong with extrem slope. To solve this i came back to add some boundary conditions for the draw_lines() function.

5. Overlap the initial image and line image. I used the cv2.addWeighted() function to adjust the lines to make it semi-transparent.

6. Output. I used the cv2.imwrite function. But before that i need to use cv2.cvtColor to convert the RGB to GRB.

### 2. Identify potential shortcomings with current pipeline


One potential shortcoming would be that it failed to detection when the vertices and the polygon of lines are changed.( when driving in a curve, or the vehicle jolts a lot) In my detection algorithm the vertices were set up to be a certain proportion to the size of the image. 

Another shortcoming could be that the project based on my current pipeline is still vulnerable to disturbance, such as the shadows, bad weather...


### 3. Suggest possible improvements to my pipeline

A possible improvement would be to detect the lines with the correlation between frames. If i try to compare and process the images in a video frame by frame, it can be easier to locate the lane line and reduce the error. 

Another potential improvement could be to keep tuning the parameters to make the project a better performance. In another way maybe i can figure out some methods for parameter tuning.

