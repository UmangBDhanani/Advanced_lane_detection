# Advanced_lane_detection

The project aims at extending the conventional road edge deteciton techniques such as canny edge detection and hough transformation to further using image processing methods to adopt to different road conditions to perfoorm better at every road corner.

The first part consists of method of edge detection where canny algorithm first tries to find the edges in the image using gradiet in the pixels and then the detected edges are then passed further to the hough transformation wherein the aklgorithm tries to fnid the consistent lines and draws a singular line from the cosecutive pixels of the image.

The second part deals with the techniques of image thresholding and computer vision to perform the same task more effectively.

### 1. Camera calibration
This the most critical part of the whole system as the faulty reuslts into poor vision for the sensor and hence induces errors in the calcualations. The camera calibration step is required as the camera has distortion during operation that is caused due to principle workinf of the camera.
Chess board corners methods of opencv library are used to calibrate camera and remove the distortion from the camera output image. Practicalle the undistortion of the camera is performed on the image of chess taken from the camera that is going to be used in th e self driving car but for the sake of this project images are taken from google.

![camera_cal](https://user-images.githubusercontent.com/84092636/205178066-12f487cb-9662-4ea7-b149-6888a9f4056c.jpg)

### 2. Perspective Transformation

In the next step perspective transformation is performed on the image to visualize the image from the top so called Bird's eye view to detect the curves in the road ahead and the angle of direction using the same camera image.

![perspective transfrom](https://user-images.githubusercontent.com/84092636/205178531-8b7b1d78-8f86-409a-ae44-844af70c79eb.jpg)


### 3 Binary Thresholding

This step consists of converting the undistorted transformed image into binaries of HLS, LAB and LUV color channels. The gradients of the filtered thresholded image is used to detect various colors from the image which in our case would be the white and yellow lane lines.
The L channel and the B channel seems to be good at detecting the yellow adn white line respectively which was found by performing trial and errors with many possibilities. Sobel gradient filter used here uses gaussian smoothining to reduce the noise in the image. 

![binary image after thresholding](https://user-images.githubusercontent.com/84092636/205179525-c2d38fb6-b0f3-4308-88dd-3b03e26330a5.jpg)

### 4. Sliding window technique

After threshoding the resultant image are used to plot the histogram and the peaks in the image signifies the presence of the lanes on either side. 

![histogram peaks](https://user-images.githubusercontent.com/84092636/205179799-eda4c326-17db-4f76-9213-cff82630fc6f.jpg)

The two distinct peaks are then used as a starting point for the sliding window method which scans from the bottom of the image till the top iteratively to find the connecting pixels and center them around the mean position.

![sliding window](https://user-images.githubusercontent.com/84092636/205180210-b8ebb159-b434-4174-ad38-1832a1d1528f.jpg)

After successfully defining the right and left lanes from the continuity of pixels from sliding window, the road is defined in between the both lanes and used to navigate the vehicle.  

![detected lane overlay](https://user-images.githubusercontent.com/84092636/205180489-be70f087-6a99-4980-ae17-6ef996d78ae9.jpg)

#### Below shown is the video of the output from canny edge detection algorithm which always draws straight lines for road lanes.

https://user-images.githubusercontent.com/84092636/205183678-b38d724b-b212-4ed9-8472-b216098e9d1f.mp4

#### Below shown is the video output from image thresholding and computer vision method.

https://user-images.githubusercontent.com/84092636/205183959-e0873207-5783-47be-b4ec-d44d7c04ea98.mp4

The whole system works well but the redundancy in transforming the image induces latency in the detection and the system may fail miserably during low light condition or in night. I assume a better approach and more advanced detections can be performed from the neural networks where system can learn to adapt to the given condition after training on similar scenarios earlier.

