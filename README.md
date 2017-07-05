Vehicle Tracking Project
========================

The steps of the project are the following:

 - Apply a color transform and append binned color features, histograms of color, a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a classifier Linear SVM classifier.
 - Implement a sliding-window technique and use your trained classifier to search for vehicles in images.
 - Use heat map to remove the false positives and accurately capture the cars.
 - Run the pipeline on a video stream

Data Exploration
----------------

I download the data set “vehicle” and “nonvehicle” from Udacity, each one contains about 8500 images. The following figure is the visualization of data:

![](https://github.com/rainbamboooo/Vehicle-Tracking-Udacity-Self-Driving-Car-Nanodegree-Term1-project5/raw/master/1.png)

Feature Extraction
------------------

In this project, I use **bin_spatial()**, **color_hist()**, and **get_hog_features()** to extract features. I use **extract_features()** to combine all of the three features above. My parameters are:

![](https://github.com/rainbamboooo/Vehicle-Tracking-Udacity-Self-Driving-Car-Nanodegree-Term1-project5/raw/master/2.png)


I also tried parameters like color_space = RGB and HSV at first, but I found that they do not perform well. YUV performs the best in my test. The following figure is the visualization of YUV color space image and the hog features of its channel:

![](https://github.com/rainbamboooo/Vehicle-Tracking-Udacity-Self-Driving-Car-Nanodegree-Term1-project5/raw/master/3.png)

Train a Classifier
------------------

I use the features I extracted above to train a **LinearSVC Classifier**.
I **StandardScaler()** to normalize the data, and use **train_test_split()** to split the training set and testing set. After the training is finished, 
I also let it to predict 10 images to see its accuracy. The results are following:

![](https://github.com/rainbamboooo/Vehicle-Tracking-Udacity-Self-Driving-Car-Nanodegree-Term1-project5/raw/master/4.png)

It seems good.

Sliding Windows Search
----------------------

I use the **find_cars()** function to apply the sliding windows search. 
It is simple. Just to split the image into small pieces, extract the little image’s feature, 
and use the classifier to predict whether it is a car or not. If it is, then draw a box. The results are:

![](https://github.com/rainbamboooo/Vehicle-Tracking-Udacity-Self-Driving-Car-Nanodegree-Term1-project5/raw/master/5.png)

Heat Map
--------

As shown in above, sometimes there are multiple boxes drawn on one car and 
sometimes there are false positive, so I use the heat map to solve this problem. Here is the result:

![](https://github.com/rainbamboooo/Vehicle-Tracking-Udacity-Self-Driving-Car-Nanodegree-Term1-project5/raw/master/6.png)

By the way, I set the threshold of heat map to 0 (actually it means that I have not removed any false positive) because when I set it to 1, sometimes it cannot detect cars. It seems that my detector does not often detect false positives.

Video Implementation
--------------------

The video is already in the folder. Its name is “vehicle_tracking.mp4”

Discussion
----------

I think the most difficult part for me is parameters tuning. I tried it so many times and costed a lot of time. I know that parameters tuning is always a big question in machine learning, but I hope that there are some better ways to solve that.

About my pipeline, I think there are some ways to improve. First is about parameters. Maybe there are even some better parameters. Second is sliding windows search. I can set different size of windows so that when I apply the heat map, the cars can be detected more accurate and the false positives will be removed.
