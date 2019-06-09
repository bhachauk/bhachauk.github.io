---
layout: qanda
---

##### What is Machine Learning and Why we are using it ? 
{: .qandaq}

<br>
  
It may be a funny question to ask in this technological era. Any way, Let’s start with
this question.
It is like, computers learn by themselves not using any explicit programming
requirements. Here we need to align the process flow to achieve this. Such as like,

- Data preparation
    For example the data we prepared is the key factor for the
        machine learning, If we use meaningless data inside, It will affect the model.
- model Selection
    model selection is also important as said in data preparation, It also should be meaningful.
    The model will vary according to the data. For example we can't use the model for **Nominal data**, which is used in **Continuous Data**. 
- Other Environment configurations
    The environment we have should support the algorithm to run. we can say the all like,
    - libraries
    - GPU or RAM Configuration
     
**Why ?**
The normal statistical methods such as correlations, etc., can be used to do the work but the key point and the truth is we are letting the machine learning model to do the various statistical analysis and getting the summary or formatted model based outputs.
- **What is Dimensionality Reduction Technique and Why we need it ?**
As i have absorbed from many open source posts, I can conclude that the dimensionality reduction mainly used to compressing the actual data into a logical dimension by removing unwanted variance elements from various dimensions. Most of the times, It is used to reduce the memory consumption and model runtime by removing unwanted datas.

It can cover the topics like,
- Features Filtering
- Component Analysis

###### Feature Filtering
---
- Features filtering can be applied by our wish also to be more careful of what we doing.
- Some of those like
- High Null carriers filter
- Low correlated filter
- Feature Importance Analysis and Filtering
- Low variance or Constant level Filter

###### Component Analysis
---

In these techniques, Actual data converted into **Components** which carries the characteristics of the data. It is like, Extracting the most important information from data what actually the data trying to convey to you. Some of the methods are,
- PCA (Principal Component Analysis) for Linear
- T-SNE (Stochastic Neighbour Embedding - T distributed) for Non linear
- UMAP (Uniform Manifold Approximation and Projection)

**Reference :**
    - [The Ultimate Guide to 12 Dimensionality Reduction Techniques (with Python codes) by Analytics Vidhya ](https://www.analyticsvidhya.com/blog/2018/08/dimensionality-reduction-techniques-python/)
{: .refbox}

<br>

##### What are all the best metrics to evaluate the machine learning model and explanation ?
{: .qandaq}

<br>

Accuracy is the well known metric but this not only the important metric. Rather than this some of others
are <mark>Precision</mark>, <mark>Recall</mark>, <mark>F1 Score</mark> and <mark>ROC</mark>. 

<br>

- Accuracy

$$
Accuracy = {Total Correct Predictions \over Total Data Size}
$$

- Precision

$$
Precision = {TruePositive \over Predicted True Count}
$$

- Recall

$$
Recall = {Total Correct Predictions \over Actual True Count}
$$

Precision and Recall are related to the **Confusion Matrix** values <mark>TP</mark>, <mark>TN</mark>, <mark>FP</mark>
and <mark>FN</mark>. The confusion matrix looks like,

###### Confusion Matrix
{: .txt-center}

| |Positive|Negative|
|-|--------|--------|
|**Positive**|TP|TN|
|**Negative**|FP|FN|
{: .dataframe style="margin-left: 40%;"}

<br>

So There may be a confusion between precision and recall :P. 
For quickly grab this difference, It can be concluded that, The Importance of predicting 
the non true observations as true. For example,

It is like saying to a non-infected patient that he (or) she was infected.
{: .output}

So now you can easily grab it for **Recall**.

It is like saying to a infected patient that he (or) she was not infected.
{: .output}

From above two examples, you can find that both are so important. We need to find the good balance format
for these metrics. So what about **F1 Score** ?

- F1 Score

$$
F1 Score = {2 * {Precision + Recall \over Precision * Recall}}
$$

- ROC Curve (Receiver Operating Characteristics) and AUC (Area Under ROC Curve)

    This curve is constructed from the parameters,
    
    - True Positive Rate
    - False Positive Rate

$$
TPR = {TP \over {TP + FN}}
$$

$$
FPR = {FP \over {FP + TN}}
$$

<br>

###### ROC Curve
{: .txt-center}

![img](https://developers.google.com/machine-learning/crash-course/images/ROCCurve.svg)
{: style="width: 500px; margin: auto"}

*Image source in Ref*


**Reference :**
    - [Machine Learning](https://github.com/Bhanuchander210/Learn_MachineLearning)
    - [Towards data science](https://towardsdatascience.com/accuracy-precision-recall-or-f1-331fb37c5cb9)
    - [ROC and AUC by Google Crash course](https://developers.google.com/machine-learning/crash-course/classification/roc-and-auc)
{: .refbox}

<br>

##### What is Regularization in machine learning ?
{: .qandaq}

**Regularization**  is so important technique as it determines ***how the learning should be***. 
The word itself means, making the training or learning as a common one and not to converge by the current training data.
It is a technique to protect the model from over-fitting. It can be simply explained from below lines,

- It controls the learning by introducing changes in traditional work flow or math functions of the model.
- It will decide the level of non-linearity and iterations which decides the learning level and provides better **Test accuracy**.
- It will fit the model before it got over-fitted, can call **Apt-fitting**.

Well-known-techniques :

- L1 Regularization (Can make weights as zero and compress the model to attain apt-fitting)
- L2 Regularization (It reduces the weights almost to zero.)
- Dropout (It will logically remove the weight as it cause for over-fitting.)

**Reference :**
    - [Regularization post from towards-data-science](https://towardsdatascience.com/regularization-an-important-concept-in-machine-learning-5891628907ea)
    - [Fundamentals of Regularization Techniques by analyticsvidhya](https://www.analyticsvidhya.com/blog/2018/04/fundamentals-deep-learning-regularization-techniques/)
    - [L1 and L2 Regularization](https://towardsdatascience.com/l1-and-l2-regularization-methods-ce25e7fc831c)
    - [Keras Regularizers](https://keras.io/regularizers/)
    - [Regularization in Machine Learning ](https://towardsdatascience.com/regularization-in-machine-learning-76441ddcf99a)
    - [Regularization for simplicity by Google](https://developers.google.com/machine-learning/crash-course/regularization-for-simplicity/l2-regularization)
{: .refbox}


##### What is KFold in python and why we need to use it ?
{: .qandaq}

<br>

**K Fold** is a technique used to evaluate the model like **Test-train split** .  It internally splits the training data into **k** number of groups (by default 10). Each group are the test data while another all groups are trained. This technique is commonly known as **Cross validation**.
It will generate a log for each group test result. So you can understand how your machine learning model acts with various groups. If your model produces highly various result **accuracies**, That means the model over-fitted for some of the classes. That’s why it can’t detect some poorly recognized classes.
The total object is to find out which model works better for all classes involved in the input data.

**Reference :**
    - [KFold Doc by scikit](https://scikit-learn.org/stable/models/generated/sklearn.model_selection.KFold.html)
    - [Cross Validation](https://scikit-learn.org/stable/models/cross_validation.html)
    - [K-Fold Cross validation](https://machinelearningmastery.com/k-fold-cross-validation/)
{: .refbox}

<br>

##### Why we need to use epochs in training ?
{: .qandaq}

<br>

The goal of using **epochs** is to reduce the **Error Rate** of the model. In machine learning, It really works to improve the model accuracy by trying to Good fit the model. It can be absorbed when we use <mark>history</mark> plot. We can use the **epochs** until it saturated at some point to avoid over-fitting and remove unnecessary run.
So, In practical we can’t be sure how much **epochs** needed for good results. Manual Observation required to validate to find out the epochs value.
In deep learning, The sample code would be like,

history = model.fit(X, Y, validation_split=0.33, epochs=150, batch_size=10, verbose=0)
{: .output}

**Reference :**
    - [Display Deep Learning Model Training History in Keras](https://machinelearningmastery.com/display-deep-learning-model-training-history-in-keras/)
{: .refbox}

<br>

##### What is seed and why we need to use it ?
{: .qandaq}

<br>

This is because **stochastic** nature of the model. Every time you run, the model runs with random initialized values. To get the same results from a Machine learning model, we can generate a same random values for every time.
Thi is the syntax to set random seed in numpy package.

from numpy.random import seed
seed(7)
{: .output}

So you need to be aware of what random package used by your model.
 
**Reference :**
    - [Reproducible Results by machine learning mastery](https://machinelearningmastery.com/reproducible-results-neural-networks-keras/)
{: .refbox}

##### How to determine the number of hidden layers required ?

This question was the often arouse and also more complicated. I hope the notes and references below will help you to understand why i said like that.

- The number of hidden layers equals one.
- The number of neurons in that layer is the mean of the neurons in the input and output layers.
- It is observed that most of the problems can be solved using the above said 2 rules.
- If you build a very deep and wide network, that means you may end up memorizing or computing the results you want on output layer at very near hidden layer from the first.
- Obviously it will take too much (unwanted) computation time and resource.
- Literally All you want is a generalised data which is more important to be considered.
- Increasing the Depth and width of a network, may cause over-fitting and also practically observed.   

**Reference :**
    - [Stack overflow discussion](https://stats.stackexchange.com/questions/181/how-to-choose-the-number-of-hidden-layers-and-nodes-in-a-feedforward-neural-netw)
    - [5.2 Capacity Over-fitting and Under-fitting](http://www.deeplearningbook.org/contents/ml.html)
    - [Stack Exchange Question and Answer 1](https://stats.stackexchange.com/questions/222883/why-are-neural-networks-becoming-deeper-but-not-wider)
    - [Stack Exchange Question and Answer 2](https://stats.stackexchange.com/questions/338255/what-is-effect-of-increasing-number-of-hidden-layers-in-a-feed-forward-nn)
{: .refbox}


##### How to replace the layers in NN ? (Collecting)

- [Keras replacing input layer](https://stackoverflow.com/questions/49546922/keras-replacing-input-layer)

<br>
<br>

Due to the nature of this post, Always can find updates
{: .txt-center style="color: #500"} 