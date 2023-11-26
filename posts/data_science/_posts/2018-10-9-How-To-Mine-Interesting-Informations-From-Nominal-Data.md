---
github: Learn_MachineLearning
oneliner: Turning Data into Interesting Information
kaggle: data-mining-a-demo-with-titanic-data
---

<kbd class="imgtitle">Contents</kbd>

1. [Introduction](#introduction)
1. [Association Rule Mining](#association-rule-mining)
1. [Association Rule Mining on Titanic Data](#association-rule-mining-on-titanic-data)
    - [Ready Up](#ready-up)
    - [Data Visualization with Plots](#data-visualization-with-plots)
    - [Analysis - Methodology](#analysis---methodology)
    - [Gender Analysis](#gender-analysis)
    - [Gender Result](#gender-result)
    - [Title Analysis](#title-analysis)
    - [Title Result](#title-result)
1. [Algorithm Evaluation](#algorithm-evaluation)        
1. [References](#references)
{: .contentBorder .txt-pad}


# Introduction
---

In real world, We deal with various types of data for example <mark>date</mark>, <mark>currency</mark>, <mark>stock rate</mark>, 
<mark>categories</mark> and <mark>rank</mark>. These are all not same data types and also not easy to associate these all in single 
line information. There are lot of methods in **Data Mining** to extract the association or information from the complex data. Some methods are,

- Classification 
- Estimation 
- Prediction 
- Affinity Grouping or Association Rules 
- Clustering 
- Anomaly Detection

In this post, I tried to explain the data mining process on **Nominal Data Set**.  
The technique to extract the interesting information from Nominal data or Categorical data
is **Association Rule Mining**. 
---

# Association Rules Mining

### Algorithms:
---

- Apriori
- FP Growth

---

### Parameters:
---

1. **Support**
    - Ratio of the particular Object observation count to the total count.
    - In another words, the percentage of a object strength in total strength.   
    - Range \[0 - 1]
 
    $$  
        Support(B) = {Observations containing (B) \over Total Observations }
    $$
    
1. **Confidence**
    - How much confident association has with its pair.
    - Range \[0 - 1] 

    $$
        Confidence(A→B) = { Observations containing both (A and B)) \over (Observations containing A)}
    $$
    
1. **Lift**
    - How much likely associated than individually occurred.
    - Range \[0 - inf]
    - if <mark>lift > 1</mark> means, It is an **interesting scenario** to consider.

    $$
    Lift(A→B) = {Confidence (A→B) \over Support (B)}
    $$
        
1. **Leverage**
    - Range  \[-1, 1]
    - If <mark>leverage =0 </mark> means, Both are independent.
    
    $$
    L (A → B) =  {S (A→B) \over S (A) * S (B)}
    $$
        
1. **Conviction**
    - It is the metric to find the dependency on **premise** by the **consequent**.    
    - Range \[0 - inf]
    - If <mark>conviction = 1</mark>, items are independent.
    - High Confident with Lower support. That means it is mostly **depends** on the another product.
    
    $$
    C (A -> B) = {1 - S (B) \over 1 - Confidence (A → B)}
    $$   

---

# Association Rule Mining on Titanic Data
---
### Ready Up
---

- **Algorithm :** Apriori
- **Language  :** Python 2.7.15
- **Data Set  :** Titanic Data From Kaggle - [<button class="goToBtn">
                                             <i class="fa fa-download" aria-hidden="true"></i>
                                             Download Csv
                                             </button>](https://www.kaggle.com/c/titanic/download/test.csv)

---

### Import Packages
---

```python
import matplotlib.pyplot as plt
import pandas as pd
from mlxtend.preprocessing import TransactionEncoder
from mlxtend.frequent_patterns import apriori, association_rules

import warnings
warnings.filterwarnings("ignore")
import seaborn as sns
```

### Loading Data-set
---


```python
titanic = pd.read_csv('train.csv')
nominal_cols = ['Embarked','Pclass','Age', 'Survived', 'Sex']
cat_cols = ['Embarked','Pclass','Age', 'Survived', 'Title']
titanic['Title'] = titanic.Name.str.extract('\, ([A-Z][^ ]*\.)',expand=False)
titanic['Title'].fillna('Title_UK', inplace=True)
titanic['Embarked'].fillna('Unknown',inplace=True)
titanic['Age'].fillna(0, inplace=True)
# Replacing Binary with String
rep = {0: "Dead", 1: "Survived"}
titanic.replace({'Survived' : rep}, inplace=True)
```

### Binning Age Column
---


```python
## Binning Method to categorize the Continous Variables
def binning(col, cut_points, labels=None):
  minval = col.min()
  maxval = col.max()
  break_points = [minval] + cut_points + [maxval]
  if not labels:
    labels = range(len(cut_points)+1)
  colBin = pd.cut(col,bins=break_points,labels=labels,include_lowest=True)
  return colBin

cut_points = [1, 10, 20, 50 ]
labels = ["Unknown", "Child", "Teen", "Adult", "Old"]
titanic['Age'] = binning(titanic['Age'], cut_points, labels)
in_titanic = titanic[nominal_cols]
cat_titanic = titanic[cat_cols]
```

The data type of the **Age column** is converted from *Number* to *Categorical* using the method <mark>Binning</mark>.
The data **Set** of the age column is <mark>["Unknown", "Child", "Teen", "Adult", "Old"]</mark> and also ensured that
all the columns are only have nominal data. The data set is separated into two types. They are,

- Gender Data
- Title Data

### Gender Data
---


```python
in_titanic.head()
```
 
<br>
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Embarked</th>
      <th>Pclass</th>
      <th>Age</th>
      <th>Survived</th>
      <th>Sex</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>S</td>
      <td>3</td>
      <td>Adult</td>
      <td>Dead</td>
      <td>male</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C</td>
      <td>1</td>
      <td>Adult</td>
      <td>Survived</td>
      <td>female</td>
    </tr>
    <tr>
      <th>2</th>
      <td>S</td>
      <td>3</td>
      <td>Adult</td>
      <td>Survived</td>
      <td>female</td>
    </tr>
    <tr>
      <th>3</th>
      <td>S</td>
      <td>1</td>
      <td>Adult</td>
      <td>Survived</td>
      <td>female</td>
    </tr>
    <tr>
      <th>4</th>
      <td>S</td>
      <td>3</td>
      <td>Adult</td>
      <td>Dead</td>
      <td>male</td>
    </tr>
  </tbody>
</table>
</div>

### Title Data
---

```python
cat_titanic.head()
```
<br>
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Embarked</th>
      <th>Pclass</th>
      <th>Age</th>
      <th>Survived</th>
      <th>Title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>S</td>
      <td>3</td>
      <td>Adult</td>
      <td>Dead</td>
      <td>Mr.</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C</td>
      <td>1</td>
      <td>Adult</td>
      <td>Survived</td>
      <td>Mrs.</td>
    </tr>
    <tr>
      <th>2</th>
      <td>S</td>
      <td>3</td>
      <td>Adult</td>
      <td>Survived</td>
      <td>Miss.</td>
    </tr>
    <tr>
      <th>3</th>
      <td>S</td>
      <td>1</td>
      <td>Adult</td>
      <td>Survived</td>
      <td>Mrs.</td>
    </tr>
    <tr>
      <th>4</th>
      <td>S</td>
      <td>3</td>
      <td>Adult</td>
      <td>Dead</td>
      <td>Mr.</td>
    </tr>
  </tbody>
</table>
</div>

### Data Visualization with Plots
---

```python
for x in ['Embarked', 'Pclass','Age', 'Sex', 'Title']:
    sns.set(style="whitegrid")
    ax = sns.countplot(y=x, hue="Survived", data=titanic)
    plt.ylabel(x)
    plt.title('Survival Plot')
    plt.show()
```


![png](/images/ds/arm/Association_Ruels_Mining_On_Titanic_Dataset_12_0.png)



![png](/images/ds/arm/Association_Ruels_Mining_On_Titanic_Dataset_12_1.png)



![png](/images/ds/arm/Association_Ruels_Mining_On_Titanic_Dataset_12_2.png)



![png](/images/ds/arm/Association_Ruels_Mining_On_Titanic_Dataset_12_3.png)



![png](/images/ds/arm/Association_Ruels_Mining_On_Titanic_Dataset_12_4.png)
---

## Analysis - Methodology
---

1. Gender Wise
1. Title Wise

Because title is also a keyword which shows the **Gender type** of a person. Analysing these both fields
together will cause for the results with **100%** association with both fields. 

#### Example:
---
- (Mr.) always associated with Male.
- (Mrs.) always associated with Female.

Putting these two fields together does not make any sense. So that the analysis split into two types.

---

### Gender Analysis
---

```python
dataset = []
for i in range(0, in_titanic.shape[0]-1):
    dataset.append([str(in_titanic.values[i,j]) for j in range(0, in_titanic.shape[1])])
# dataset = in_titanic.to_xarray()

oht = TransactionEncoder()
oht_ary = oht.fit(dataset).transform(dataset)
df = pd.DataFrame(oht_ary, columns=oht.columns_)
print df.head()
```

### Output:
---

<div class="output">
       1      2      3  Adult      C  Child   Dead    Old      Q      S  \
0  False  False   True   True  False  False   True  False  False   True   
1   True  False  False   True   True  False  False  False  False  False   
2  False  False   True   True  False  False  False  False  False   True   
3   True  False  False   True  False  False  False  False  False   True   
4  False  False   True   True  False  False   True  False  False   True   

   Survived   Teen  Unknown  female   male  
0     False  False    False   False   True  
1      True  False    False    True  False  
2      True  False    False    True  False  
3      True  False    False    True  False  
4     False  False    False   False   True
</div>

## All Nominal Values
---


```python
print oht.columns_
```

### Output:
---

['1', '2', '3', 'Adult', 'C', 'Child', 'Dead', 'Old', 'Q', 'S', 'Survived', 'Teen', 'Unknown', 'female', 'male']
{: .output}


## Implementing Apriori Algorithm:
---

```python
output = apriori(df, min_support=0.2, use_colnames=oht.columns_)
print output.head()
```

idx support itemsets
0  0.242697      (1)
1  0.206742      (2)
2  0.550562      (3)
3  0.528090  (Adult)
4  0.615730   (Dead)
{: .output}

### Rules Configuration
---

```python
config = [
    ('antecedent support', 0.7),
    ('support', 0.5),
    ('confidence', 0.8),
    ('conviction', 3)
]

for metric_type, th in config:
    rules = association_rules(output, metric=metric_type, min_threshold=th)
    if rules.empty:
        print 'Empty Data Frame For Metric Type : ',metric_type,' on Threshold : ',th
        continue
    print rules.columns.values
    print '-------------------------------------'
    print 'Configuration : ', metric_type, ' : ', th
    print '-------------------------------------'
    print (rules)

    support=rules.as_matrix(columns=['support'])
    confidence=rules.as_matrix(columns=['confidence'])

    plt.scatter(support, confidence, edgecolors='red')
    plt.xlabel('support')
    plt.ylabel('confidence')
    plt.title(metric_type+' : '+str(th))
    plt.show()
```

**Output : Config 1: antecedent support = 0.7**

<div class="output">['antecedents' 'consequents' 'antecedent support' 'consequent support'
 'support' 'confidence' 'lift' 'leverage' 'conviction']
-------------------------------------
Configuration :  antecedent support  :  0.7
-------------------------------------
   antecedents                consequents  antecedent support  \
0          (S)                     (male)            0.723596   
1          (S)              (Adult, Dead)            0.723596   
2          (S)  (female, Adult, Survived)            0.723596   
3          (S)               (male, Dead)            0.723596   
... 
</div>

![png](/images/ds/arm/Association_Ruels_Mining_On_Titanic_Dataset_20_1.png)

---

**Output : Config 2: antecedent support = 0.7**

<div class="output">
['antecedents' 'consequents' 'antecedent support' 'consequent support'
 'support' 'confidence' 'lift' 'leverage' 'conviction']
-------------------------------------
Configuration :  support  :  0.5
-------------------------------------
  antecedents consequents  antecedent support  consequent support   support  \
0      (male)      (Dead)            0.647191            0.615730  0.524719   
1      (Dead)      (male)            0.615730            0.647191  0.524719   

   confidence      lift  leverage  conviction  
0    0.810764  1.316752  0.126224    2.030636  
1    0.852190  1.316752  0.126224    2.386905  
</div>

![png](/images/ds/arm/Association_Ruels_Mining_On_Titanic_Dataset_20_3.png)

---

**Output : Config 3: confidence: 0.8**

<div class="output">
['antecedents' 'consequents' 'antecedent support' 'consequent support'
 'support' 'confidence' 'lift' 'leverage' 'conviction']
-------------------------------------
Configuration :  confidence  :  0.8
-------------------------------------
               antecedents consequents  antecedent support  \
0              (1, female)  (Survived)            0.105618   
1            (Adult, Dead)         (S)            0.319101   
2                (2, male)      (Dead)            0.121348   
3                (2, Dead)      (male)            0.108989   
...
</div>

![png](/images/ds/arm/Association_Ruels_Mining_On_Titanic_Dataset_20_5.png)

---

**Output : Config 4: conviction: 3**

<div class="output">
['antecedents' 'consequents' 'antecedent support' 'consequent support'
 'support' 'confidence' 'lift' 'leverage' 'conviction']
-------------------------------------
Configuration :  conviction  :  3
-------------------------------------
   antecedents consequents  antecedent support  consequent support   support  \
0  (1, female)  (Survived)            0.105618            0.384270  0.102247   
1    (2, Dead)      (male)            0.108989            0.647191  0.102247   
... 
</div>


![png](/images/ds/arm/Association_Ruels_Mining_On_Titanic_Dataset_20_7.png)

---

## Gender Result
---

## Interesting Information: Gender Analysis
---

- Persons Who are Sex: female       With  PcClass: 1, have 96.80 % Confidence Survived : True
- Persons Who are PcClass: 2        With  Survived: False, have 93.81% Confidence Sex: Male

## Common Information:
---

- Persons Who are Survived : False  With  Age : UnKnown , have 81.88 %  Confidence  PcClass : 3
- Persons Who are Age : Adult       With  PcClass : 2   , have 90.2 %   Confidence Embarked : S
- Persons Who are Survived: False   With  Age : Adult and PcClass : 3, have 86.36% Confidence Embarked: S

---

### Title Analysis
---


```python
dataset = []
in_titanic=cat_titanic
for i in range(0, in_titanic.shape[0]-1):
    dataset.append([str(in_titanic.values[i,j]) for j in range(0, in_titanic.shape[1])])
# dataset = in_titanic.to_xarray()

oht = TransactionEncoder()
oht_ary = oht.fit(dataset).transform(dataset)
df = pd.DataFrame(oht_ary, columns=oht.columns_)
print df.head()
```

### Output:
---

<div class="output">
       1      2      3  Adult      C  Capt.  Child   Col.   Dead   Don.  \
0  False  False   True   True  False  False  False  False   True  False   
1   True  False  False   True   True  False  False  False  False  False   
2  False  False   True   True  False  False  False  False  False  False   
3   True  False  False   True  False  False  False  False  False  False   
....
[5 rows x 30 columns]
</div>

## All Nominal values:
---

```python
print oht.columns_
```

### Output:
---

<div class="output">
['1', '2', '3', 'Adult', 'C', 'Capt.', 'Child', 'Col.', 'Dead', 'Don.', 'Dr.', 'Jonkheer.', 'Lady.', 'Major.', 'Master.', 'Miss.', 'Mlle.', 'Mme.', 'Mr.', 'Mrs.', 'Ms.', 'Old', 'Q', 'Rev.', 'S', 'Sir.', 'Survived', 'Teen', 'Title_UK', 'Unknown']
</div>

### Implementing Apriori Algorithm:
---

```python
output = apriori(df, min_support=0.2, use_colnames=oht.columns_)
print output.head()
```

   support itemsets
0  0.242697      (1)
1  0.206742      (2)
2  0.550562      (3)
3  0.528090  (Adult)
4  0.615730   (Dead)
{: .output}

---

### Rules Configuration
---

```python
config = [
    ('antecedent support', 0.7),
    ('confidence', 0.8),
    ('conviction', 3)
]

for metric_type, th in config:
    rules = association_rules(output, metric=metric_type, min_threshold=th)
    if rules.empty:
        print 'Empty Data Frame For Metric Type : ',metric_type,' on Threshold : ',th
        continue
    print rules.columns.values
    print '-------------------------------------'
    print 'Configuration : ', metric_type, ' : ', th
    print '-------------------------------------'
    print (rules)

    support=rules.as_matrix(columns=['support'])
    confidence=rules.as_matrix(columns=['confidence'])

    plt.scatter(support, confidence, edgecolors='red')
    plt.xlabel('support')
    plt.ylabel('confidence')
    plt.title(metric_type+' : '+str(th))
    plt.show()
```

**Output : Config 1: antecedent support = 0.7**

<div class="output">
    ['antecedents' 'consequents' 'antecedent support' 'consequent support'
     'support' 'confidence' 'lift' 'leverage' 'conviction']
    -------------------------------------
    Configuration :  antecedent support  :  0.7
    -------------------------------------
       antecedents         consequents  antecedent support  consequent support  \
    0          (S)       (Adult, Dead)            0.723596            0.319101   
    1          (S)               (Mr.)            0.723596            0.579775   
    2          (S)              (Dead)            0.723596            0.615730   
    3          (S)             (Adult)            0.723596            0.528090 
    ...   
</div>

![png](/images/ds/arm/Association_Ruels_Mining_On_Titanic_Dataset_28_1.png)

---

**Output : Config 2: confidence: 0.8**

<div class="output">
Empty Data Frame For Metric Type :  support  on Threshold :  0.5
['antecedents' 'consequents' 'antecedent support' 'consequent support'
 'support' 'confidence' 'lift' 'leverage' 'conviction']
-------------------------------------
Configuration :  confidence  :  0.8
-------------------------------------
           antecedents consequents  antecedent support  consequent support  \
0        (Adult, Dead)         (S)            0.319101            0.723596   
1             (3, Mr.)      (Dead)            0.357303            0.615730   
2             (S, Mr.)      (Dead)            0.446067            0.615730   
3         (Mr., Adult)         (S)            0.328090            0.723596   
...  
</div>

![png](/images/ds/arm/Association_Ruels_Mining_On_Titanic_Dataset_28_3.png)

**Output : Config 3: conviction: 3**

<div class="output">['antecedents' 'consequents' 'antecedent support' 'consequent support'
 'support' 'confidence' 'lift' 'leverage' 'conviction']
-------------------------------------
Configuration :  conviction  :  3
-------------------------------------
   antecedents consequents  antecedent support  consequent support   support  \
0     (3, Mr.)      (Dead)            0.357303             0.61573  0.316854   
1  (S, Mr., 3)      (Dead)            0.275281             0.61573  0.244944      
   confidence      lift  leverage  conviction  
0    0.886792  1.440229  0.096851    3.394382  
1    0.889796  1.445107  0.075445    3.486891  
</div>

![png](/images/ds/arm/Association_Ruels_Mining_On_Titanic_Dataset_28_5.png)

---

## Title Result
---

## Interesting Information - Title Analysis:

- Persons Who are Title : Mr.  With  Class : 3 and Embarked : S, have 88.9796 %  Confidence  Survived : Dead

---

## How to filter ? - A simple Demo
---

```python
rules[rules['confidence']==rules['confidence'].min()]
rules[rules['confidence']==rules['confidence'].max()]
```

### Output Tables:
---

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>antecedents</th>
      <th>consequents</th>
      <th>antecedent support</th>
      <th>consequent support</th>
      <th>support</th>
      <th>confidence</th>
      <th>lift</th>
      <th>leverage</th>
      <th>conviction</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8</th>
      <td>(True)</td>
      <td>(female)</td>
      <td>0.38427</td>
      <td>0.352809</td>
      <td>0.261798</td>
      <td>0.681287</td>
      <td>1.931035</td>
      <td>0.126224</td>
      <td>2.030636</td>
    </tr>
  </tbody>
</table>
</div>
<br>
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>antecedents</th>
      <th>consequents</th>
      <th>antecedent support</th>
      <th>consequent support</th>
      <th>support</th>
      <th>confidence</th>
      <th>lift</th>
      <th>leverage</th>
      <th>conviction</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>12</th>
      <td>(1, female)</td>
      <td>(True)</td>
      <td>0.105618</td>
      <td>0.38427</td>
      <td>0.102247</td>
      <td>0.968085</td>
      <td>2.519286</td>
      <td>0.061661</td>
      <td>19.292884</td>
    </tr>
  </tbody>
</table>
</div>
<br>

---

```python
rules = association_rules (output, metric='support', min_threshold=0.1)
rules[rules['confidence'] == rules['confidence'].min()]
rules[rules['confidence'] == rules['confidence'].max()]
```

### Output Tables:
---

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>antecedents</th>
      <th>consequents</th>
      <th>antecedent support</th>
      <th>consequent support</th>
      <th>support</th>
      <th>confidence</th>
      <th>lift</th>
      <th>leverage</th>
      <th>conviction</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>274</th>
      <td>(S)</td>
      <td>(True, Adult, female)</td>
      <td>0.723596</td>
      <td>0.14382</td>
      <td>0.103371</td>
      <td>0.142857</td>
      <td>0.993304</td>
      <td>-0.000697</td>
      <td>0.998876</td>
    </tr>
  </tbody>
</table>
</div>
<br>

<div>

<table style="width:50%" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>antecedents</th>
      <th>consequents</th>
      <th>antecedent support</th>
      <th>consequent support</th>
      <th>support</th>
      <th>confidence</th>
      <th>lift</th>
      <th>leverage</th>
      <th>conviction</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>55</th>
      <td>(1, female)</td>
      <td>(True)</td>
      <td>0.105618</td>
      <td>0.38427</td>
      <td>0.102247</td>
      <td>0.968085</td>
      <td>2.519286</td>
      <td>0.061661</td>
      <td>19.292884</td>
    </tr>
  </tbody>
</table>
</div>
---

# Algorithm Evaluation
---

Use this <mark>Python script</mark> to evaluate the algorithms <mark>Apriori</mark> and <mark>FP Growth</mark>.

[<button class="goToBtn">
<i class="fa fa-code" aria-hidden="true"></i>
Go to Code
</button>](https://github.com/Bhanuchander210/Learn_MachineLearning/blob/master/04.Data_Mining/Association_rule_mining/evaluate_algorithms.py){: .btn .link}

The evaluation output would be like,

<div class="output">For Data Matrix          :  891  x  5
Number of Individuals    :  15
Apriori                  :  0.872148990631
FP-Algorithm             :  0.0637619495392
--------------------------
For Data Matrix          :  17999  x  5
Number of Individuals    :  25
Apriori                  :  0.493063926697
FP-Algorithm             :  0.621915102005
--------------------------
For Data Matrix          :  35998  x  5
Number of Individuals    :  25
Apriori                  :  0.990983963013
FP-Algorithm             :  1.18582415581
</div>

# Conclusion:
---

In terms of reading process, the algorithms **Apriori** and **FP Growth** differs. According to that 
FP Growth is more efficient than apriori for bigger data because it reads only two times a file. But for me both are 
working in same manner and almost consumes same time for a specific data. It may be differ with respect to the data and 
nominal value count. Any way before implementing these algorithm, once check with <mark>Algorithm-Evaluation</ark> as 
said before and find the suitable algorithm for your work.


Also published in [Kaggle](https://www.kaggle.com/bhanuchanderu/data-mining-a-demo-with-titanic-data).  

# References:
---

Thanks to the Sources,
    - [Apriori](http://pbpython.com/market-basket-analysis.html)
    - [FP Growth](https://pypi.org/project/pyfpgrowth/)
    - [Association Rule Mining Via Apriori Algorithm in python](https://stackabuse.com/association-rule-mining-via-apriori-algorithm-in-python/)
    - [Mining Frequent Items using apriori algorithm](https://www.analyticsvidhya.com/blog/2017/08/mining-frequent-items-using-apriori-algorithm/)
    - [Finding Frequent Patterns](https://rasbt.github.io/mlxtend/user_guide/frequent_patterns/apriori/)
    - [Efficient - Apriori - Python 3.6](https://pypi.org/project/efficient-apriori/)
    - [Data mining with apriori](http://intelligentonlinetools.com/blog/tag/apriori-algorithm-in-data-mining/)
{: .refbox}
