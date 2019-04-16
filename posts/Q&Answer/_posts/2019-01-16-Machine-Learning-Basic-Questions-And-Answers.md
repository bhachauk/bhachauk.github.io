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

![Confusion matrix for binary classification](https://cdn-images-1.medium.com/max/800/1*OhEnS-T54Cz0YSTl_c3Dwg.jpeg)
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
    - [Towards data science](https://towardsdatascience.com/accuracy-precision-recall-or-f1-331fb37c5cb9)
    - [ROC and AUC by Google Crash course](https://developers.google.com/machine-learning/crash-course/classification/roc-and-auc)
{: .refbox}

<br>

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

<br>
<br>

Due to the nature of this post, Always can find updates
{: .txt-center style="color: #500"} 