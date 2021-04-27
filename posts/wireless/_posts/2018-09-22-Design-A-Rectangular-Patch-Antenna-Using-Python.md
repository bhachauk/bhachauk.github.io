---
github: patch-antenna-util
---


**Update 1 : 23/02/2020**
Source code of python moved as package [patch-antenna-util](https://github.com/Bhanuchander210/patch-antenna-util/) from normal python file and the post re-organized.
{: .refbox}


**Update 2 : 25/02/2020**
Directivity related equations and codes updated in post and also in package [patch-antenna-util](https://github.com/Bhanuchander210/patch-antenna-util/) from normal python file and the post re-organized.
{: .refbox}


**Update 3 : 25/06/2020**
Released as python package [patch_antenna](https://pypi.org/project/patch-antenna/) in pypi and the post organized.
{: .refbox}


**Update 4 : 05/08/2020**
Gerber facility added for both python package and live demo.
{: .refbox}

{: .txt-center}

<kbd class="imgtitle">Contents</kbd>

1. [Introduction](#1-introduction)
1. [Design antenna](#2-design-antenna)
1. [Description](#3-description)
1. [Other Parameters](#4-other-parameters)
1. [Antenna Simulator](#5-antenna-simulator---live)
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



### 2. Design Antenna
---


Especially for rectangular patch antenna the python package : [patch-antenna](https://pypi.org/project/patch-antenna/) created. Please follow below steps / guidelines for the usage.


###### Installation

Install the required packages <mark>scipy</mark> and <mark>patch_antenna</mark> as shown below.

```
pip install scipy
pip install patch_antenna
```
    
Lets us calculate the patch antenna parameters to resonate at **2.4 GHz** with the dielectric material 
having dielectric constant **4.4** and height **1.6 mm**.


Define your values in appropriate unit as shown below example code : [simple_design.py](https://github.com/Bhanuchander210/patch_antenna/blob/master/examples/simple_design.py)

<br>

```python
import json
import patch_antenna as pa
# resonant frequency in Hz
freq = 2.4 * 10 ** 9
# dielectric constant
er = 4.4
# thickness of the cavity in meter
h = 1.6 * 10 ** -3
result = pa.design(freq, er, h)
# pretty printing
print(json.dumps(result, indent=4))
```

##### Output

The output of the code is just pretty printed using package <mark>json</mark>. All calculated results are in their base unit such as,
- frequency in <mark>Hz</mark>
- impedance in <mark>ohm</mark>
- All design lengths are in <mark>meter</mark>.

{
    "frequency": 2400000000.0,
    "patch_width": 0.0380099749575278,
    "patch_length": 0.0294215930843705,
    "feeder_width": 0.015203989983011122,
    "feeder_length": 0.015449608708025277,
    "inset_gap_width": 0.007601994991505561,
    "inset_length": 0.010914409094654586,
    "ground_length": 0.05447120179239577,
    "ground_width": 0.06281396494053892,
    "input_edge_impedance": 321.50075290241097
}
{: .output}


##### Gerber facility

The design can be stored as <mark>gerber</mark> file, which is commonly required for cnc fabrication. 

- Normal feed

```python
pa.write_gerber(freq, er, h, 'patch_design_normal_2.4GHz_4.4_er_1.6_h.gbr', 'normal')
```

- Inset feed

```python
pa.write_gerber(freq, er, h, 'patch_design_inset_2.4GHz_4.4_er_1.6_h.gbr', 'inset')
```


### 3. Description
---

##### Patch Antenna Feed Types

There are multiple types of feeding to patch antenna. This design output is used for these two types shown below,

<kbd class="imgtitle">Patch antenna feeding types</kbd>


![types](/images/patch/patch_antenna_types.png)
{: .imgbrd}

##### Optimal Inset Feed position (inset_length)

Optimal inset feed length calculated to reduce the input impedance of feeding point to the patch.
This optimal point can be calculated from the standard impedance <mark> 50 Ohm </mark> and length of the designed patch
antenna.

<br>

<kbd class="imgtitle">Image of Voltage (V), current (I), impedance (Z) curve along the length of patch</kbd>

![Plot](/images/inset.png)
{: .imgbrd }

**Note:**

> Basic design steps and related details are completed here. Hope you got your antenna design. 
Following contents use another development github repository **Patch-antenna-util**. If you wish to know more about this, 
proceed the following.

 
### 4. Other Parameters
---

Other parameters such as **directivity**, **EHPlane** and **Surface plot** are organized in the another 
repository [Patch antenna util](https://github.com/Bhanuchander210/patch-antenna-util). Follow below steps if the above
discussed details required otherwise skip this.


##### Initialize source code

Clone the repository [Patch antenna util](https://github.com/Bhanuchander210/patch-antenna-util) and update your python path by running the command,


git clone https://github.com/Bhanuchander210/patch-antenna-util.git
cd patch-antenna-util
export PYTHONPATH=$PYTHONPATH:/path/to/patch_util
{: .output}

##### Python script

Then modify [design_patch.py](https://github.com/Bhanuchander210/patch-antenna/blob/master/design_patch.py) or write your own
python code as shown below. 

Import the **patch_util** package and initialize the your parameters to its variables such as frequency, dielectric constant and thickness of the cavity.
 
```python
from patch_util.patch import get_directivity, patch_eh_plane_plot, surface_plot, get_i1
freq = 2.4e9
er = 4.4
h = 1.6* 10 ** -3
```


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
patch_width = result['patch_width']
i1 = get_i1(patch_width, freq)
print("The value for equation (14-53a) : ", i1)
``` 

The value for equation (14-53a) :  1.1479757280698542
{: .output}

Then the second value **i2** assumed here which is need to be calculated manually from the equation **14-55a**. The directivity
calculation methods are,

```python
d1 = get_directivity(patch_width, freq, patch_length)
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


### 5. Antenna Simulator - Live
---

Also i have migrated these thing into <mark>Javascript</mark> to make a live demo to the viewer and also the design can be downloaded as gerber file <mark>.gbr</mark> for fabrication. 

[![demo](https://raw.githubusercontent.com/Bhanuchander210/patch-antenna/master/resource/anim.gif)](https://bhanuchander210.github.io/patch-antenna-util/)

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
