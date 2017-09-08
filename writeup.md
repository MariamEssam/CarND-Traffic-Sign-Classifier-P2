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
[image9]: ./writeupimages/SelectedImages.png 
[image10]: ./writeupimages/selectedimageswithtitle.png 


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



**Normaization of the data**


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
| Convolution 3x3     	| 1x1 stride, [Updated]valid padding, outputs 28x28x6 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride, [Updated]valid padding,  outputs 14x14x6 				|
| Convolution 3x3	    | 1x1 stride, [Updated]valid padding, outputs 10x10x16   	|
| RELU					|												|
| Max pooling	      	| 2x2 stride, [Updated]valid padding,  outputs 5x5x16 				|
| Flatten layer	      | outputs 400 				|
| Fully connected		|outputs 43     									|
| Dropout				| rate=0.5 for training set and 1 for test/Valid set     |

**Q:Describe how you trained your model**

Optimizer used is Adam optimizer

EPOCHS = 25

BATCH_SIZE = 128

Rate=0.0008

The model is Saved in net.ckpt

**Q:validation set accuracy of ?**

95.5%

**Q:Test set accuracy of ?**

93.7%
[Updated] While the model accuracy during training stage is 95.5% while the value in the test is 93.7% this due to under fitting of the model so I think increasing number of Epoch with the same learning rate can be a good idea. 
**Q:What was the first architecture that was tried and why was it chosen?**

I have use ConvLeNet-5Layers 

**Q:What were some problems with the initial architecture?**

the problem is that the model overfit very fast

**How was the architecture adjusted and why was it adjusted?**

Reduce FC layers to one and add a dropout to avoid overfitting

**Which parameters were tuned? How were they adjusted and why?**

Learning rate is reduced to 0.0008 to improve the acuracy and Epoch is increased to 25 Epochs as using this value the accuracy increase without decrease back..

**What are some of the important design choices and why were they chosen?**

Reduce number of FC layers....Fix overfitting issue
Add drop out....Fix overfitting issue
Augment the train data size....learn the model on the rare signs
Normalize the data.............better performance 

### **Test a Model on New Images**
[Updated] Now I will try the model on a set of images I found on the web, the set I have found is different than the image the model learnt on it in the following:
1-The web image brightness is more than that I trained the model on
2- The contrast between color is higher than that I used for training 
3-Also the size of the sign itself is different, the sign I had represent 100% from the image no padding while the image I used contain padding(crop this padding can be a good idea to overcome this shortcoming)

I have used the following images:

![alt text][image9]

That's how the model has seen them:

![alt text][image10]

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Road Work      		| Road Work   									| 
|No  U-turn     			| Ahead only									|
| children crossing					| children crossing											|
| Keep Right      		| Keep Right 					 				|
| No Vehicle		| No Vehicle      							|
| Pedestrian		| Speed limit 70      							|
| Stop		| Speed limit 60      							|
| wildanimalscrossing		| Road Work     							|
| No Entry	| No Entry     							|
| Speed limit 60     		| Speed limit 60      							|

## **Predication**


[Updated]My model looks very very certain from the results it had it give 1 for for the sign it has selected.

I really don't know if this mean the model is well trained or it overfit


| Image			        |     Probability	        					| 
|:---------------------:|:---------------------------------------------:| 
| Road Work      		| 1   									| 
|No  U-turn     			| 1								|
| children crossing					| 1											|
| Keep Right      		| 1 					 				|
| No Vehicle		| 1      							|
| Pedestrian		| 1     							|
| Stop		| 1    							|
| wildanimalscrossing		| 1     							|
| No Entry	| No Entry     							|
| Speed limit 60     		| 1      							|
