---
layout: qanda
---

##### What is Machine Learning and Why we are using it ? 
{: .qandaq}

<br>
  
It may be a funny question to ask in this time of era. Any way, Let’s start with
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

![Confusion matrix for binary classification](data:image/png;base64,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%0A)
{: style="width: 500px; margin:auto;"} 

*Image source in Ref*

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