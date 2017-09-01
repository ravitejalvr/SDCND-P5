# Project-5 Vehicle Detection and Tracking using Machine Learning

The following steps are followed for this project:

* Select features of images using Histogram of Oriented Gradients (HOG) and also from color spaces.
* The extracted features are then used for training Linear SVC. An Accuracy of 99.04% is obtained in classifying car images from non-car images.
* For avoidance of over fitting of data, the training and test data is split randomly and also, the training data is shuffled. Also, for giving equal waitage for all features, the features were scaled.
* Then, the selected region of test image is slided for finding car images using the trained SVC Classifier.
* Then, the heat map is used for removing false positives from images. The final car detection is done used treshold over heat map of the previous step.
* Then, the above pipeline is followed for each frame in project video file.

The output video is given by:

[![IMAGE ALT TEXT](http://img.youtube.com/vi/wWu1ds_BJUQ/0.jpg)](https://youtu.be/wWu1ds_BJUQ)  

### Histogram of Oriented Gradients

#### Extracting HOG features
The extraction of HOG features is done using hog function of skimage library.
The inputs which were fed are orientations per cell, pixels per cell and cells per block. 
These hog features were extracted for all vehicles and non-vehicle images for training SVC classifier.

The sample hog features image is given below:

<a href="url"><img src="http://i.imgur.com/rTeRO8q.jpg" align="center" height="200" width="250" ></a>

The parameters for hog inputs were tuned for getting best accuracy in SVC classification. Finally, 11 orientations, 8 pixels per cell and 2 cells per block were selected. Color space of YCrCb is selected.

#### Train and Build Classifier using extracted features

Then, linear SVC is trained using features from vehicle and non-vehicle images supplied in the project and an accuracy of 99.04% is obtained.
To avoid over-fitting, shuffling and random splitting of test data is done.

### Sliding Window Search and Heat Map

#### Choice of window scales to search and how much to overlap windows?

The Method `find_cars()` from the lesson materials is used for detection of cars in entire image. This method extracts HOG features of all aimage and later splits according to the cell and block size. Then, also hog features and color space features were found out of each window and are resized to (64,64) for each window for classifier to predict. 

The output is given below:

<a href="url"><img src="http://i.imgur.com/skAZa0Q.jpg" align="center" height="200" width="250" ></a>

Then, the detected car blocks were added heat based on number of times it was overlapped. add_heat function is used for this purpose and it increases pixel value by 1 for every detection.

The output is given below:

<a href="url"><img src="http://i.imgur.com/8lQH3Kt.jpg" align="center" height="200" width="250" ></a>

Then, threshold is applied to the heatmap such that all images less than that value will be set to zero.

Based on the heatmap and threshold, final car detection boundary is set. 

The final detection boundary is given below:

<a href="url"><img src="http://i.imgur.com/FJ7A2wr.jpg" align="center" height="200" width="250" ></a>

The final detection boundary performs reasonably well with no false positives in the test images.

### Discussion

The project was challenging and interesting. It was good to learn about sliding window search, hog feature extraction and classifying images based on features. Interesting observed is even though classifier gives an accuracy over 99.5% doesnt guarantee lack of false positives. Data for training need to be more exhaustive for goodness of fit.
