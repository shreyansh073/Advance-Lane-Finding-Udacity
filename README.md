# Advanced Lane Finding Project
This project was part of Udacity's Self Driving Car Nanodegree. In this project, I have detected highway lane lines on a video stream using OpencV image analysis techniques to identify lines, including Hough Transforms and Canny edge detection.

The project includes the following steps:
## Camera Calibration
Here I have calibrated the camera using the functions as discussed in the tutorials. There
are 9 corners in rows and 6 corners in columns. The images in camera_cal folder have been
used to calibrate this camera.

The object points refers to the 3d points on the chessboard in real world space. The image
points are calculated using cv2.findChessboardCorners(). These object and image points
are further used to calibrate the camera using cv2.calibrateCamera() function.

![Calibrate](/readme/1.png "calibrate")
![Calibrate](/readme/2.png "calibrate")

## Pipeline(Single image)
### Conversion from rgb to binary image
The binary image has been created by taking the saturation channel, red channel and
the x-gradient threshold. These thresholds were chosen after experimenting in differentchannels and thresholds. Although it works in the video, it doesn’t do well in intense
brightness or broad daylight, for which, the lightness channel also needs to be incorporated.

![Binary](/readme/3.png "binary")

### Perspective Transform
Here, the source and destination points have been entered manually. These points are
used to get the transformation matrix M and the inverse transform matrix M_inv using the
function cv2.getPerspectiveTransform. You can see the bird-eye-view of the image below.

![Bird](/readme/4.png "bird")

### Sliding window technique
The sliding window technique has been used to detect and find lane lines. This is an initial
brute force technique to find lane lines. Later in the pipeline, this step has been
avoided(wherever possible) and an average of previous 10 frames has been taken to reduce
computation and improve accuracy.

![Window](/readme/5.png "window")

## Pipeline(Video)
In the pipeline, a few global variables have been used to keep track of the previous 10
frames which are used to take average of lane lines. In case we have appropriate values
from previous frames, the search is done apriori as mentioned in the tutorials.
To detect outliers, apart from the threshold values used to create the binary image, imperfect
lane findings have also been removed. It compares the current mean difference between the
left and right lanes and the previous averaged mean difference. If it goes beyond a
threshold, then the lane detected is considered as an outlier.

In the end, the warped image is unwarped using the M_inv matrix and is filled with green
color, followed by writing the corresponding offset and ROC on the video.

<a href="http://www.youtube.com/watch?feature=player_embedded&v=-5fiYPXx_eo
" target="_blank"><img src="http://img.youtube.com/vi/-5fiYPXx_eo/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="480" height="360" border="10" /></a>





