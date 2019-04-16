---
github: patch-antenna
---

<kbd class="imgtitle">Contents</kbd>

1. [Introduction](#1-introduction)
1. [Python Source Code](#2-source-code)
1. [Design](#3-design)
1. [Antenna Parameters](#4-antenna-parameters)
1. [Antenna Simulator](#5-antenna-simulator---live)
1. [References](#6-references)
{: .contentBorder .txt-pad}

### 1. Introduction
---

Designing a patch antenna has some concepts and equations. Initially To view about the design, Find my previous post 
[Patch antenna concept](/Patch-Antenna-Concepts){: .link} for the basics. Here, 
this post is to explain the same using <mark>Python libraries</mark> shown below.

import math
import matplotlib.pyplot as plt
import numpy as np
from math import cos, sin, sqrt, atan2, acos, pi, log10
from mpl_toolkits.mplot3d import Axes3D
import scipy.integrate
{: .output}

### 2. Source Code
---

All Parameter equations are converted as python methods to design and view the outcomes.
You can use the source code attached below, for the further process, which contains the Basic Methods 
for this design operation.

[<button class="goToBtn">
 <i class="fa fa-download" aria-hidden="true"></i>
 Download patch.py
 </button>](/contents/patch.py "Patch-Design.py")
 
<br>

### 3. Design
---

Use relative import of the downloaded source code as shown below.


```python

import os
import sys
scriptpath = "/home/bhanuchander/Desktop/patch.py"
sys.path.append(os.path.abspath(scriptpath))
from patch import DesignPatch, inputImpedance, insetFeedPosition, getDirectivity, PatchEHPlanePlot, SurfacePlot, getGs
```

Normally designing a patch antenna have these following steps.

- **[Pre-requisite](#pre---requisite)**
- **[Width and Length](#width-and-length)**
- **[Input Impedance](#input-impedance)** 
- **[Optimal Inset Feed position](#optimal-inset-feed-position)**

<br>

###### Pre-requisite
---

Designing the Patch antenna for the Given parameters,
- Resonant Frequency (freq)
- Dielectric Constant of the Cavity Material (Er)
- Height of the Dielectric Thickness (h)
    
Here for example Resonant frequency **2.4GHz**, dielectric constant **4.4** and the height of the cavity
substrate **1.6 mm** used. The velocity of the EM Wave (V) is **$$ 3 \times \mathrm{10}\,8  \ m/s $$**.

freq = 2.4e9
Er = 4.4
h = 1.6* 10 ** -3
v = 3 * 10 ** 8 
{: .output}

###### Width and Length :
---

To Find the Patch antenna Length (L) and Width (W)

```python
W, L = DesignPatch(Er, h, freq)
```

Patch Width,  W: 0.0380362887156m
Patch Length,  L: 0.0294423612179m
Patch Height,  h: 0.0016m
{: .output}

###### Input Impedance
---

Input impedance of the patch antenna at the edge of the patch where <mark>feeder</mark> connected.

<br>
  
```python
Rin = inputImpedance(freq, W, L, h, Er)
```

Input Impedance: 321.502648844 ohms
{: .output}

<br>

###### Optimal Inset Feed position
---

Optimal inset feed length calculated to reduce the input impedance of feeding point to the patch.
This optimal point can be calculated from the standard impedance <mark> 50 Ohm </mark> and length of the designed patch
antenna.

<br>

<kbd class="imgtitle">Image of Voltage (V), current (I), impedance (Z) curve along the length of patch</kbd>

![Plot](/images/inset.png)
{: .imgbrd }

The Input impedance and length of the patch antenna decides the optimal input impedance point. According to that,
the length can be obtained from the method <mark>insetFeedPosition()</mark> like shown below.

<br>

```python
print 'Inset Feed Position : ', insetFeedPosition(Rin, L)
```

Inset Feed Position :  0.0109221252235
{: .output}

### 4. Antenna parameters
---

###### Getting G1, G12
---

```python
G1, G12 = getGs(freq, W, L)
print 'G1 : ', G1
print 'G12 : ', G12
```

G1 :  0.000969285496339
G12 :  0.00058591164371
{: .output}

<br>

###### Directivity
---

Directivity is the metric which explains about the <mark>Radiation Pattern</mark> of the antenna.
Directivity is the ratio of the maximum radiation intensity of a particular direction to the normalized radiation intensity 
of all direction.

<kbd class="imgtitle">Example Radiation Pattern</kbd>

![Plot](/images/patch/radiation-pattern.png)
{: .imgbrd }

*Image Source : [Research Gate](https://www.researchgate.net/figure/Normalized-radiation-patterns-of-the-conformal-patch-antenna-array-and-its-conformal_fig12_281027053){: .link}*

```python
I1=1.863
I2=3.59801

d1, d2 = getDirectivity(G1, G12, W, freq, I1 , I2)                            
print 'Directivity : ', d1, ' dB'
print 'Directivity : ', d2, ' dB'
``` 

Directivity :  3.88419387395  dB
Directivity :  5.04023487871  dB
{: .output}

<br>

###### Fields of Electric and Magnetic Plane - Plot
---

```python
fields = PatchEHPlanePlot(freq, W, L, h, Er)
```

<kbd class="imgtitle">Plot of EH Plane</kbd>

![Plot](/images/patch/eh-plot.png)
{: .imgbrd }


###### Surface Plot - 3D
---

```python
SurfacePlot(fields, freq, W, L, h, Er)
```

{% include 3dplot.html %}


### 5. Antenna Simulator - Live
---

Also i have migrated these thing into <mark>Javascript</mark> to make a live demo to the viewer.

[![demo](https://raw.githubusercontent.com/Bhanuchander210/patch-antenna/master/resource/anim.gif)](https://bhanuchander210.github.io/patch-antenna/)

This app still in development and I am always updating it due to the nature of the post :P

### 6. References
---

Thanks to the sources,
    - [Antenna Theory](http://www.antenna-theory.com/)
    - [Antenna patch Post-1 ](https://medium.com/@johngrant/antenna-arrays-and-python-square-patch-element-6bd3445f39d5)
    - [Antenna patch Post-2](https://medium.com/python-pandemonium/antenna-arrays-and-python-calculating-directivity-84a2cfea0739)
    - [Patch Antenna Design and Simulator - Live](https://bhanuchander210.github.io/patch-antenna/)
    - [Patch-antenna GitHub](https://github.com/Bhanuchander210/patch-antenna.git)
{: .refbox}
