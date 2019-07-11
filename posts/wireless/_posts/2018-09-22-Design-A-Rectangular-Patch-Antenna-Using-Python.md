---
github: patch-antenna
---

*Last Update : 24 Jun 2019* 
{: .txt-center}

<kbd class="imgtitle">Contents</kbd>

1. [Introduction](#1-introduction)
1. [Antenna Parameters](#-2-patch-antenna-parameters)
1. [Antenna Simulator](#3-antenna-simulator---live)
1. [References](#4-references)
{: .contentBorder .txt-pad}

### 1. Introduction
---

Designing a patch antenna has some concepts and mathematical equations. I suggest you to view this [Patch antenna concept](/Patch-Antenna-Concepts){: .link} post,
 If you are a novice to patch antenna design. In this post, I tried to use python utils and libs for designing a patch antenna.
 
##### Imports

```python
import math
import matplotlib.pyplot as plt
import numpy as np
from math import cos, sin, sqrt, atan2, acos, pi, log10
import plotly
from plotly.offline import init_notebook_mode
import plotly.graph_objs as go
plotly.offline.init_notebook_mode(connected=True)
import scipy.integrate
```

Normally Python design requires these three important parameter values (As said in suggested post),
 
- Resonant Frequency (freq)
- Dielectric Constant of the Cavity Material (Er)
- Height of the Dielectric Thickness (h)


##### Assumption
    
Here for example Resonant frequency **2.4 GHz**, dielectric constant **4.4** and the height of the cavity
substrate **1.6 mm** used. The velocity of the EM Wave (V) is **3 * 10^8 m/s**.

So the python code initiated with the assumptions like shown below,


```python
# velocity of light constant
v = 3 * 10 ** 8 

freq = 2.4e9
Er = 4.4
h = 1.6* 10 ** -3
v = 3 * 10 ** 8
```


### 2. Patch Antenna Parameters
---

- [Width and Length](#-width-and-length-)
- [Conductance](#-getting-g1-g12)
- [Input Impedance](#-input-impedance)
- [Optimal Inset Feed Position](#-optimal-inset-feed-position)
- [Directivity](#-directivity)


All Parameter equations are converted as python methods to calculate and view the outcomes.

##### Width and Length :
---

To Find the Patch antenna Length (L) and Width (W)

```python
def DesignPatch (Er, h, Freq):    
    Eo = 8.854185e-12
    lambd = 3e8 / Freq
    lambdag = lambd / sqrt(Er)
    W = (3e8 / (2 * Freq)) * sqrt(2 / (Er + 1))
    temp = 1 + 12*(h/W)
    Ereff = ((Er + 1) / 2) + ((Er - 1) / 2) * temp ** -0.5                              
    F1 = (Ereff + 0.3) * (W / h + 0.264)                                                
    F2 = (Ereff - 0.258) * (W / h + 0.8)
    dL = h * 0.412 * (F1 / F2)
    lambdag = lambd / sqrt(Ereff)
    L = (lambdag / 2) - 2 * dL
    print('Rectangular Microstrip Patch Design')
    print("Frequency: " + str(Freq))
    print("Dielec Const, Er : " + str(Er))
    print("Patch Width,  W: " + str(W) + "m")
    print("Patch Length,  L: " + str(L) + "m")
    print("Patch Height,  h: " + str(h) + "m")
    return W, L
W, L = DesignPatch (Er, h, freq)
```

Patch Width,  W: 0.0380362887156m
Patch Length,  L: 0.0294423612179m
Patch Height,  h: 0.0016m
{: .output}

##### Getting G1, G12
---
  
```python
def S_i(a):
    temp=scipy.integrate.quad(lambda x:sin(x)/x,0,a)
    return temp[0]
def J0(s):
    temp=scipy.integrate.quad(lambda x:cos(s*sin(x)),0,pi)
    temp=(1/pi)*temp[0]
    return temp
## Getting Conductance params
def getK0 (f):
    lamda_0 = v/f
    k0 = (2*pi)/lamda_0
    return k0
def getG1 (W, f):
    k0 = getK0 (f)
    X = k0 * W
    I1 = -2 + cos(X) + X*S_i(X) + sin(X)/X
    G1 = I1 / ( 120 * pi**2 )
    return G1
def getG12 (W, k0, L):
    temp=scipy.integrate.quad(lambda x:(((sin(k0*W*cos(x)/2)/cos(x))**2)*J0(k0*L*sin(x))*sin(x)**3),0,pi)
    G12=(1/(120*pi**2))*temp[0]
    return G12
def getGs(f, W, L):
    G1 = getG1(W, f)
    k0 = getK0(f)
    G12 = getG12(W, k0, L)
    return G1, G12
G1, G12 = getGs(freq, W, L)
print ('G1 : '+ G1)
print ('G12 : '+ G12)
```

G1 :  0.000969285496339
G12 :  0.00058591164371
{: .output}

##### Input Impedance
---

Input impedance of the patch antenna at the edge of the patch where <mark>feeder</mark> connected.

<br>

```python
def inputImpedance (f, W, L, h, epsilon):
    global v
    k0 = getK0 (f)
    G1, G12 = getGs(f, W, L)
    Rin=1/(2*(G1+G12))
    print ("Input Impedance:" + Rin + "ohms")
    return Rin

Rin = inputImpedance(freq, W, L, h, Er)
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
def insetFeedPosition(Rin, L):
    R=50.0
    y0=(L/pi)*(math.acos(sqrt(R/Rin)))
    return y0
    
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

```python
I1=1.863
I2=3.59801

def getDirectivity(G1, G12, W, f, I1, I2):
    global v
    lamda_0 = v/f
    g_12=G12/G1
    D_AF=2/(1+g_12)
    D0=((2*pi*W)/lamda_0)**2*(1/I1)
    D2=D0*D_AF
    DIR_1 = 10*log10(D2)
    I2=3.59801
    D_2=((2*pi*W)/lamda_0)**2*(pi/I2)
    DIR_2 = 10*log10(D_2)
    return DIR_1, DIR_2

d1, d2 = getDirectivity(G1, G12, W, freq, I1 , I2)                            
print 'Directivity : ', d1, ' dB'
print 'Directivity : ', d2, ' dB'
``` 

Directivity :  3.88419387395  dB
Directivity :  5.04023487871  dB
{: .output}

<br>



##### Utils for plotting EH Plane
---

```python
def sph2cart1(r, th, phi):
  x = r * cos(phi) * sin(th)
  y = r * sin(phi) * sin(th)
  z = r * cos(th)
  return x, y, z
   
def cart2sph1(x, y, z):
  r = sqrt(x**2 + y**2 + z**2) + 1e-15
  th = acos(z / r)
  phi = atan2(y, x)
  return r, th, phi

def PatchFunction(thetaInDeg, phiInDeg, Freq, W, L, h, Er):
    lamba = 3e8 / Freq
    theta_in = math.radians(thetaInDeg)
    phi_in = math.radians(phiInDeg)
    ko = 2 * math.pi / lamba
    xff, yff, zff = sph2cart1(999, theta_in, phi_in)
    xffd = zff
    yffd = xff
    zffd = yff
    r, thp, php = cart2sph1(xffd, yffd, zffd)
    phi = php
    theta = thp
    if theta == 0:
        theta = 1e-9     
    if phi == 0:
        phi = 1e-9
    Ereff = ((Er + 1) / 2) + ((Er - 1) / 2) * (1 + 12 * (h / W)) ** -0.5        
    F1 = (Ereff + 0.3) * (W / h + 0.264)                                        
    F2 = (Ereff - 0.258) * (W / h + 0.8)
    dL = h * 0.412 * (F1 / F2)
    Leff = L + 2 * dL
    Weff = W                                                                    
    heff = h * sqrt(Er)
    Numtr2 = sin(ko * heff * cos(phi) / 2)
    Demtr2 = (ko * heff * cos(phi)) / 2
    Fphi = (Numtr2 / Demtr2) * cos((ko * Leff / 2) * sin(phi))
    Numtr1 = sin((ko * heff / 2) * sin(theta))
    Demtr1 = ((ko * heff / 2) * sin(theta))
    Numtr1a = sin((ko * Weff / 2) * cos(theta))
    Demtr1a = ((ko * Weff / 2) * cos(theta))
    Ftheta = ((Numtr1 * Numtr1a) / (Demtr1 * Demtr1a)) * sin(theta)
    rolloff_factor = 0.5                                                       
    theta_in_deg = theta_in * 180 / math.pi                                          
    F1 = 1 / (((rolloff_factor * (abs(theta_in_deg) - 90)) ** 2) + 0.001)      
    PatEdgeSF = 1 / (F1 + 1)                                                    
    UNF = 1.0006                                                               
    if theta_in <= math.pi / 2:
        Etot = Ftheta * Fphi * PatEdgeSF * UNF                                   
    else:
        Etot = 0
    return Etot

def GetPatchFields(PhiStart, PhiStop, ThetaStart, ThetaStop, Freq, W, L, h, Er):
    fields = np.ones((PhiStop, ThetaStop))                                     
    for phiDeg in range(PhiStart, PhiStop):
            for thetaDeg in range(ThetaStart, ThetaStop):                       
                eField = PatchFunction(thetaDeg, phiDeg, Freq, W, L, h, Er)    
                fields[phiDeg][thetaDeg] = eField                               
    return fields                                                                                              
```

##### Fields of Electric and Magnetic Plane - Plot
---

```python
def PatchEHPlanePlot(Freq, W, L, h, Er, isLog=True):
    fields = GetPatchFields(0, 360, 0, 90, Freq, W, L, h, Er)                                                   
    Xtheta = np.linspace(0, 90, 90)                                                                             
    if isLog:                                                                                                   
        plt.plot(Xtheta, 20 * np.log10(abs(fields[90, :])), label="H-plane (Phi=90)")                          
        plt.plot(Xtheta, 20 * np.log10(abs(fields[0, :])), label="E-plane (Phi=0)")
        plt.ylabel('E-Field (dB)')
    else:
        plt.plot(Xtheta, fields[90, :], label="H-plane (Phi=90)")
        plt.plot(Xtheta, fields[0, :], label="E-plane (Phi=0)")
        plt.ylabel('E-Field')
    plt.xlabel('Theta (degs)')                                                                                 
    plt.title("EH Plane - Theta ")
    plt.ylim(-40)
    plt.xlim((0, 90))
    start, end = plt.xlim()
    plt.xticks(np.arange(start, end, 5))
    plt.grid(b=True, which='major')
    plt.legend()
    plt.show()                                                                                                  
    return fields

fields = PatchEHPlanePlot(freq, W, L, h, Er)
```
<p class="txt-center">
<img style="width:30rem;" src="/images/patch/eh-plot.png"/>
</p>

##### Surface Plot - 3D
---

```python
def SurfacePlot(Fields, Freq, W, L, h, Er):
    phiSize = Fields.shape[0]                                                                                   
    thetaSize = Fields.shape[1]
    X = np.ones((phiSize, thetaSize))                                                                           
    Y = np.ones((phiSize, thetaSize))
    Z = np.ones((phiSize, thetaSize))
    for phi in range(phiSize):                                                                                  
        for theta in range(thetaSize):
            e = Fields[phi][theta]
            xe, ye, ze = sph2cart1(e, math.radians(theta), math.radians(phi))                                   
            X[phi, theta] = xe                                                                                  
            Y[phi, theta] = ye
            Z[phi, theta] = ze                                                                       
    surface = go.Surface(x=X, y=Y, z=Z)
    data = [surface]
    layout = go.Layout(
        title='Surface Plot of EH Plane',
        scene=dict(
            xaxis=dict(
                gridcolor='rgb(255, 255, 255)',
                zerolinecolor='rgb(255, 255, 255)',
                showbackground=True,
                backgroundcolor='rgb(230, 230,230)'
            ),
            yaxis=dict(
                gridcolor='rgb(255, 255, 255)',
                zerolinecolor='rgb(255, 255, 255)',
                showbackground=True,
                backgroundcolor='rgb(230, 230,230)'
            ),
            zaxis=dict(
                gridcolor='rgb(255, 255, 255)',
                zerolinecolor='rgb(255, 255, 255)',
                showbackground=True,
                backgroundcolor='rgb(230, 230,230)'
            )
        )
    )
    fig = go.Figure(data=data, layout=layout)
    plotly.offline.plot(fig)
    
SurfacePlot(fields, freq, W, L, h, Er)
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
