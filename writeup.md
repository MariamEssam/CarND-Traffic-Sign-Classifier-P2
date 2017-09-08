# **Traffic Sign Recognition** 

[//]: # (Image References)

[image1]: ./writeupimages/samplesign.png "Random Sample"
[image2]: ./writeupimages/traindata.png "Train Data Distribution"
[image3]: ./writeupimages/30speedlimit.png "Speed limit (30 km/h)"
[image4]: ./writeupimages/30speedlimitgray.png "Speed limit (30 km/h) Gray Scale"
[image5]: ./writeupimages/30speedlimitshifted.png "Speed limit (30 km/h) Shifted"
[image6]: ./writeupimages/30speedlimitnoise.png "Speed limit (30 km/h) With Noise"
[image7]: ./writeupimages/30speedlimitdark.png "Speed limit (30 km/h) Darkness Increased"
[image8]: ./writeupimages/30speedlimitbright.png "Speed limit (30 km/h) Brightness Increased"

---

## **Overview**
In this writeup I am going to discuss my project and any experience I accquire while working in it.

## **Dataset Summary & Exploration**
### **DataSet Summary**
The data set is composed from three main parts:
1.Training data (samples = 34799)
2.Validation data (samples =4410)
3.Test data(samples =12630)

The data given is already separted so no need to split the data

## **Exploratory Visualization**
In this section I tried to display a random sign to see what will be explored 

![alt text][image1]

Also I checked the distribution of the train as shown below and as a quick remark I had some of the train data repeat alot while others are really rare this distribution is not good......

![alt text][image2]

**Remark:** One of lesson learned is stay close from your data is always a good idea

---

## **Design and Test a Model Architecture**
### **Preprocessing**

For the preprocessing I have made the following:
1.Convert image to gray scale
2.Augment the train data size 
3.Normailze the data


**Gray Scale Image**
Convert the image to gray scale is useful to accelarate the processing of training and is make the accuracy bit higher.
![alt text][image3]  ![alt text][image4]


