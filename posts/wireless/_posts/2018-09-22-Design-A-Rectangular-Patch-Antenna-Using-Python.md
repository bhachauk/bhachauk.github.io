---
github: patch-antenna
---

{: .txt-center}

<kbd class="imgtitle">Contents</kbd>

1. [Introduction](#1-introduction)
1. [Antenna Parameters](#-2-calculate-patch-antenna-parameters)
1. [Antenna Simulator](#3-antenna-simulator---live)
1. [References](#4-references)
{: .contentBorder .txt-pad}

### 1. Introduction
---

Designing a patch antenna has some concepts and mathematical equations. I suggest you to view this [Patch antenna concept](/Patch-Antenna-Concepts){: .link} post,
 If you are a novice to patch antenna design. In this post, I tried to use python utils and libs for designing a patch antenna.


Normally Python design requires these three important parameter values (As said in suggested post),
 
- Resonant Frequency (freq)
- Dielectric Constant of the Cavity Material (Er)
- Height of the Dielectric Thickness (h)


I have moved my python codes to the Repo : [Patch Antenna](https://github.com/Bhanuchander210/patch-antenna) and packaged as **patch_util**.


### 2. Calculate Patch Antenna Parameters
---
    
Lets us calculate the patch antenna parameters to resonate at **2.4 GHz** with the dielectric material 
having dielectric constant **4.4** and height **1.6 mm**. You can find the sample design code for this example in my repo as 
[design_patch.py](https://github.com/Bhanuchander210/patch-antenna/blob/master/design_patch.py).
 

The parameters are,


- [Width and Length](#-width-and-length-)
- [Conductance](#-getting-g1-g12)
- [Input Impedance](#-input-impedance)
- [Optimal Inset Feed Position](#-optimal-inset-feed-position)
- [Directivity](#-directivity)


##### Initialize source code

Clone the repository [Patch antenna](https://github.com/Bhanuchander210/patch-antenna) and update your python path by running the command,

```text
export PYTHONPATH=$PYTHONPATH:/path/to/patch_util
```

##### Python script

Then modify [design_patch.py](https://github.com/Bhanuchander210/patch-antenna/blob/master/design_patch.py) or write your own
python code as shown below. 

Import the **patch_util** package and initialize the your parameters to its variables such as frequency, dielectric constant and thickness of the cavity.
 
```python
from patch_util.patch import design_patch, input_impedance, inset_feed_position, get_directivity, patch_eh_plane_plot, surface_plot, getGs
freq = 2.4e9
Er = 4.4
h = 1.6* 10 ** -3
```

##### Width and Length :
---

To Find the Patch antenna Length (L) and Width (W)

```python
W, L = design_patch(Er, h, freq)
```

Rectangular Microstrip Patch Design
Frequency: 2400000000.0
Dielec Const, Er : 4.4
Patch Width,  W: 0.03803628871563654m
Patch Length,  L: 0.029442361217936117m
Patch Height,  h: 0.0016m
{: .output}

##### Getting G1, G12
---
  
```python
G1, G12 = getGs(freq, W, L)
print('G1 : ', G1)
print('G12 : ', G12)
```

G1 :  0.000969285496339
G12 :  0.00058591164371
{: .output}

##### Input Impedance
---

Input impedance of the patch antenna at the edge of the patch where <mark>feeder</mark> connected.

<br>

```python
Rin = input_impedance(freq, W, L)
```

Input Impedance: 321.502648844 ohms
{: .output}

<br>

##### Optimal Inset Feed position
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
print('Inset Feed Position : '+ insetFeedPosition(Rin, L))
```

Inset Feed Position :  0.0109221252235
{: .output}

<br>

##### Directivity
---

Directivity is the metric which explains about the <mark>Radiation Pattern</mark> of the antenna.
Directivity is the ratio of the maximum radiation intensity of a particular direction to the normalized radiation intensity 
of all direction.

<kbd class="imgtitle">Example Radiation Pattern</kbd>

![Plot](/images/patch/radiation-pattern.png)
{: .imgbrd }

*Image Source : [Research Gate](https://www.researchgate.net/figure/Normalized-radiation-patterns-of-the-conformal-patch-antenna-array-and-its-conformal_fig12_281027053){: .link}*

According to the reference **Antenna Theory: Analysis and Design by Constantine A. Balanis : Chapter 14.2.3**,
There are two kind of equations (*14-53a*, *14-55a*) which is used to calculate the value <mark>I</mark> for different cases <mark>single slot</mark> and <mark>two slot</mark>. 

![Single slot](https://raw.githubusercontent.com/Bhanuchander210/patch-antenna/master/resource/patch_i1.png)
![Two slot](https://raw.githubusercontent.com/Bhanuchander210/patch-antenna/master/resource/patch_i2.png)

<br>
So that we can get two different directivity values as <mark>d1</mark> and <mark>d2</mark> calculated from <mark>i1</mark>, <mark>i2</mark> respectively.
The script to calculate <mark>i1</mark> value has been implemented as method <mark>get_i1()</mark> when the other one <mark>i2</mark> skipped because of complexity.
  
```python
i1 = get_i1(W, freq)
print("The value for equation (14-53a) : ", i1)
``` 

The value for equation (14-53a) :  1.1479757280698542
{: .output}

Then the second value **i2** assumed here which is need to be calculated manually from the equation **14-55a**. The directivity
calculation methods are,

```python
d1 = get_directivity(W, freq, L)
print('Directivity : ', d1, ' dB')

# Let's assume the value i2
i2 = 2
d2 = get_directivity_two_slot(W, freq, i2)
print("Directivity (two-slot) : ", d2, ' dB')
```

Directivity :  5.9869953652616035  dB
Directivity (two-slot) :  7.59055858259433  dB
{: .output}

<br>



##### Fields of Electric and Magnetic Plane - Plot
---

```python
fields = patch_eh_plane_plot(freq, W, L, h, Er)
```
<p class="txt-center">
<img style="width:30rem;" src="/images/patch/eh-plot.png"/>
</p>

##### Surface Plot - 3D
---

```python
surface_plot(fields)
```

{% include 3dplot.html %}


### 3. Antenna Simulator - Live
---

Also i have migrated these thing into <mark>Javascript</mark> to make a live demo to the viewer.

[![demo](https://raw.githubusercontent.com/Bhanuchander210/patch-antenna/master/resource/anim.gif)](https://bhanuchander210.github.io/patch-antenna/)

This app still in development and I am always updating it due to the nature of the post :P

### 4. References
---

Thanks to the sources,
    - [Antenna Theory: Analysis and Design by Constantine A. Balanis](https://www.academia.edu/11205305/Antenna_Theory_Analysis_and_Design_3rd_Edition_by_Balanis)
    - [Antenna Theory](http://www.antenna-theory.com/)
    - [Antenna patch Post-1 ](https://medium.com/@johngrant/antenna-arrays-and-python-square-patch-element-6bd3445f39d5)
    - [Antenna patch Post-2](https://medium.com/python-pandemonium/antenna-arrays-and-python-calculating-directivity-84a2cfea0739)
    - [Patch-antenna GitHub Repository](https://github.com/Bhanuchander210/patch-antenna.git)
{: .refbox}



**Update 1 : 23/02/2020**
Source code of python moved as package [patch_util](https://github.com/Bhanuchander210/patch-antenna/tree/master/patch_util) from normal python file and the post re-organized.
{: .refbox}


**Update 2 : 25/02/2020**
Directivity related equations and codes updated in post and also in package [patch_util](https://github.com/Bhanuchander210/patch-antenna/tree/master/patch_util) from normal python file and the post re-organized.
{: .refbox}