---
github: reality_of_one_shot_learning
oneliner: Face recognition with small data set
---

<kbd class="imgtitle">Contents</kbd>

1. [Introduction](#introduction)
1. [Setup details](#setup-details)
1. [Results](#results)
1. [Conclusion](#conclusion)
1. [References](#references)
{: .contentBorder .txt-pad}

#### Introduction

The goal of the post is to share my experience with this topic called <mark>One Shot Learning</mark> which is normally used
while we have a small training data set for face recognition. After testing with various codes shared in github and posts shown
in references, I made this post to show my observations and collected results. 

**One shot learning :**

It is commonly a classification / categorization / similarity identification technique while having small training
data set for <mark>computer vision</mark> tasks such as object detection, face recognition and hand writing recognition. 
Normally computer vision models have very large deep neural networks which are all not easy to train and requires more resources
and training data. But real time problems doesn't have that much data to train those large models. One shot learning is the
recommended solution for these kind of specific problems.


![siamese_base](/images/ds/siamese_base.jpeg)

*Sample structure - One Shot Learning - source : [reference_1](#-references)*
{: .txt-center}

<br><br>

Here **Two ConvNet pre-trained models** are followed by a custom layer with <mark>sigmoid</mark> activated final layer 
used to learn the similarity between the two image inputs. The work flow would be like,

- <mark>Pre-trained networks</mark> generates the **feature vectors** from its final layer.
- <mark>That custom layer</mark> which joins the both pre-trained models, used to found the **Euclidean distance**
between the generated feature vectors.
- <mark>Sigmoid activation</mark> in last classifies the distance value to its target label.

#### Setup details

The pre-trained deep learning neural model [Keras-VGG-Face-ResNet-50][1] is used again for training to learn our custom data faces.
The reason for choosing <mark>ResNet50</mark> was discussed in the evaluation of [Face Authentication][4]. Custom Final 
layer followed by sigmoid activation function was implemented on tensor layers for calculating the euclidean distance.

![SiameseNet](/images/ds/SiameseResNet50.png)


#### Results

The results of Siamese Network test accuracy scores and real time scores are not up to the expectation as discussed in
theories. I have experienced these scenarios for various data and also in varying metrics size of the data (but low for single class), 
number of epochs learned. Until increasing the size of training data for single class, can not found any enhancement in 
test set accuracy score and real time accuracy.

The results are shown below,

###### Applying Low Epochs size : 5

|Loss History|Accuracy History|
|------------|----------------|
|![Low_epoch_Loss](https://raw.githubusercontent.com/Bhanuchander210/reality_of_one_shot_learning/master/SiameseResNet_Loss_Old.png)|![Low_epoch_Accuracy](https://raw.githubusercontent.com/Bhanuchander210/reality_of_one_shot_learning/master/SiameseResNet_Accuracy_Old.png)|

 
###### Applying Low Epochs size : 50

|Loss History|Accuracy History|
|------------|----------------|
|![Low_epoch_Loss](https://raw.githubusercontent.com/Bhanuchander210/reality_of_one_shot_learning/master/SiameseResNet_Loss_50.png)|![Low_epoch_Accuracy](https://raw.githubusercontent.com/Bhanuchander210/reality_of_one_shot_learning/master/SiameseResNet_Accuracy_50.png)|


After increasing the epochs size, The model seems well with cross validation test data. But when this trained loaded applied in 
real time test data, It may even get **0 %** accuracy.

The point is **Siamese network** for face authentication with the discussed **One shot learning** technique is not reliable in my observations or may be i am wrong with implementation (If yes please correct me).
As said in theories, the siamese network with transfer learned deep learning neural network can't learn from lowest data 
(4-5 images per class. Even they mentioned 1 image per class idk how ?) even highly performing transfer learned model loaded.


#### Conclusion

One shot learning with siamese network may be work well with simple convolutional neural networks having few layers only.
These kind of architecture only fit for the **Similarity Detection** based tasks such as hand write recognition, 
shapes similarity level calculation and etc. 

If we increase the size of the convolutional network the learning phase would requires more system resources and time.
So continuous / online learning is a difficult one for this kind of situations. Please correct me if any thing wrong.

#### References
---

Thanks to the sources,
    - [One shot learning - siamese][2]
    - [Keras VGG-Face][1]
    - [ONe shot learning - Machine learning mastery](https://machinelearningmastery.com/one-shot-learning-with-siamese-networks-contrastive-and-triplet-loss-for-face-recognition/)
    - [One shot learning - wiki](https://en.wikipedia.org/wiki/One-shot_learning)
{: .refbox}

[1]: https://github.com/rcmalli/keras-vggface
[2]: https://towardsdatascience.com/one-shot-learning-with-siamese-networks-using-keras-17f34e75bb3d
[3]: https://github.com/iwantooxxoox/Keras-OpenFace
[4]: https://github.com/Bhanuchander210/face_authentication