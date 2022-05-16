# ASL Recognition CNN OpenCV

In this project, I wanted to raise awareness for the hearing impaired. Do not forget every learning starts with the alphabet. You can make predictions about the **American Sign Language Alphabet** to the model by camera. So let's dig out the project some more.
<img src="https://user-images.githubusercontent.com/81585804/168675071-f64e8df6-d62c-42af-a44b-7b554d3212cf.png" width="100" height="100">

I cover this project on the three step.
* About Dataset
* Deep Learning - CNN
* OpenCV
* How to run

##1. Dataset
I use two different dataset for this project. The first one is, [asl-alphabet](https://www.kaggle.com/datasets/grassknoted/asl-alphabet), used for training and testing parts. It consist of 29 classes and each class has 3000 image. For Training 78300 image and  testing 8700 image used.
Second dataset is,[asl-alphabet-test](https://www.kaggle.com/datasets/danrasband/asl-alphabet-test), is used for evaluating. These two dataset is too diffrent from eachother. Later we see some consequence of this.

##2. Deep Learning - CNN
First things first we should some pre-process before training. [One hot encoding](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html) and [RGB normalization](https://akash0x53.github.io/blog/2013/04/29/RGB-Normalization/). These links are usefull if you don't know about them. Tradionally CNN is for mostly used for Image Processing and ı kept this tradition. The following two figure are Confusion Matrix of respectively test and evaluation.  Before, ı mention about the difference about two dataset.  That is the consequence of difference. Test images are so similar with the training set so accuracy and values of Confusion matrix is so high.  On the other hand evaluation set is so much diffrent than training that is the reasen why evaluation scores too low.

<img src="https://user-images.githubusercontent.com/81585804/168676983-3094ac59-9b7b-4f6e-97f2-3908624eae0c.png" width="100" height="100">
<img src="https://user-images.githubusercontent.com/81585804/168677085-43356f35-aed3-4e2d-b010-cec958e7a4d3.png" width="100" height="100">

Finally here some different training result:

| OPTIMIZER | EPOCH | TEST ACCURACY | EVALUATION ACCURACY |
| --- | --- | --- | --- |
| rmsprop | 5 | %99.609 | %40.46 |
| rmsprop | 10 | %99.989 | %52.529 |
| adam | 5 | %99.494 | %38.506 |
| adam | 10 | %99.805 | %38.62 |

***Lack of hardware such as GPU and having a large datasets, ı use Google Colaboratory and suggest you to use that kind of cloud systems***

##3. OpenCV
Now, it is time for the **real-time** predictions. But there was a problem. Hand detection is not simple as face detection nor common. To overcome this difficulty, I first detected the hand from the camera (hand_detection.py).
Then CNN is implemented to the OpenCV. But predictions were way ridiculous. Here is the reason of it :point_down: : 

* I thought that if ı make the sign to the window (which is opened by Opencv), model can easily predict. But it didn't turn out the way I thought. Because model took whole the window as an input. Including myself, door etc.
* Then the idea of drawing a square came to my mind. Unfortunately that's a another fail. Model took the whole window again.
* Finally ı managed the crop the square. That's why prediction only works in the square.

<img src="https://user-images.githubusercontent.com/81585804/168678162-4722404a-1fd3-44d9-8f6e-ab90ce95abb4.jpeg" width="100" height="100">


##4. How to run 

After fork, you can run ASL_Recognition.py. But if you want you can run .ipynb and you can build your own model. It is up to you. 
