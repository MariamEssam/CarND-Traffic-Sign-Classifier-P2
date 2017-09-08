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

Convert the image to gray scale is useful to accelarate the processing of training and to make the accuracy bit higher.


![alt text][image3]      ![alt text][image4]

**Augment Data Size**

As mentioned above the data distribution is not good some sign repeat alot while others not the same, here I tried to augment the data that does not repeat alot so I can have better distribution. To  Augment the data I have followed randomly one of the following ways:
**1- Shift and Rotate the image**
Randomly select a value to use it for shifting the image  and rotate it

![alt text][image3]      ![alt text][image5]

**2- Add Noise**

![alt text][image4]      ![alt text][image6]

**3- Increase Brigthness**

![alt text][image4]      ![alt text][image8]

**4- Increase Darkness**

![alt text][image4]      ![alt text][image7]

** Normaization of the data**

To normalize the data we use (pixels-128)/128
I can see the mean of the train, valid and test set is:
-0.318228855468
-0.365025175968
-0.353497899455

### **Model Architecture**

In this part I have tried the same architecture used in the lessons *ConvLenet-5*, I compared this versus what I have seen the Yann paper I have just taken the idea of reduce the number of FC layers to one but I have not implemented exactly same model of Yann.
My Model is composed of 
| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 Gray Scale Image   							| 
| Convolution 3x3     	| 1x1 stride, same padding, outputs 28x28x6 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 14x14x6 				|
| Convolution 3x3	    | 1x1 stride, same padding, outputs 10x10x16   	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 5x5x16 				|
| Flatten layer	      | outputs 400 				|
| Fully connected		|outputs 43     									|
| Dropout				| rate=0.5 for training set and 1 for test/Valid set     |
