---
shiny: patch
---

### Basics of Patch Antenna and Observations
<hr>

<kbd class="imgtitle">Contents</kbd>

1. **[Patch Antenna - Intro](#introduction)**
1. **[Patch Antenna - Various Feeding Techniques](#various-feeding-techniques)**
1. **[Patch Antenna - How to design](#how-to-design)**
1. **[Patch Antenna - Measurement](#measurement)**
1. **[Patch Antenna - Important of Dielectrics](#importants-of-dielectrics)**
1. **[Patch Antenna - Multilayer Approach](#multilayer-approach)**
1. **[Patch Antenna - Patch Sensor](#concept-of-patch-sensor)**
{: .contentBorder .txt-pad}

<br>

### Introduction
---

A mircrostrip patch antenna in its simplest configuration consists of a radiating patch on one side of a dielectric substrate, which has a ground plane on the side. The patch conductors usually made of copper or gold can be virtually assumed to be of any shape. However, conventional shapes are normally used to simplify analysis and performance prediction. The radiating element and the feed lines are usually photo etched on the dielectric substrate.
There are various types of patch antennas using in various applications depends upon their performances. Some basic types are,
- Rectangle
- Square			  
- Dipole		
- Elliptical			
- Disc sector		
- Ring sector	
- Slotted-patch
- Circular
- Triangular
- Circular ring

### Advantages
---

- Low weight and low volume
- Easy to design 
- Simple structure to understand the working principle
- Low fabrication cost
- Easy to integrate with microwave circuits
- Normally patch antennas are efficient radiators
- Easy to test under the experimental setup

### Rectangular Patch Antenna
---

Rectangular patch antenna is a simple type of patch antenna most commonly used for analysing purposes. As per the name this patch has a rectangle shape with a feeder line as per shown in figure. This rectangular patch is placed on a dielectric substrate which has a ground plane below.


<kbd class="imgtitle">Diagram of a Normal rectangular patch antenna</kbd>

![Patch](/images/norm.png)
{: .imgbrd }

### Various Feeding Techniques
---

- Inset feed
- Aperture feed
- Coaxial feed
- Quarter wavelength feed
- Coupled Feed

### Observation
---

From many source of analysis references, It conclued that inset feed technique provides better performance compared to other feeding techniques.

### Inset Feed Technique
---

Inset feed technique is used to decrease the input impedance of the patch antenna by moving the feeder line into the patch antenna. Patch has higher impedance at the edge can be realized from the given below figure.

<kbd class="imgtitle">Image of Inset Feed Technique in Patch antenna</kbd>

![Inset-Patch](/images/patch.png)
{: .imgbrd }


<kbd class="imgtitle">Image of Voltage (V), current (I), impedance (Z) curve along the length of patch</kbd>

![Plot](/images/inset.png)
{: .imgbrd }

So that moving the feeder line inside the patch will vary the input impedance of the patch antenna as per the equation shows below,

```math

    Z(yin)  =    Z0 * [cos]^2  (πl/yin)
```
<mark>Z (yin) -	Input impedance at the length yin</mark>

<mark>Z0      -	Input impedance at the edge</mark>


For getting lower input impedance, feeder should be placed in ¼th of the patch length. When <mark>yin = l/4</mark>,

```math

    Z(yin)  = Zo / 2
```
 
It will reduce the impedance up to <mark>50%</mark> of its edge impedance. After this length again impedance will increase as per shown above figure. By this way we can tune the input impedance by changing the inset length. In this project work I have analysed the patch antenna with this inset feed technique which is designed as per above discussed manner.

### How To Design
---

Designing a patch antenna is mainly depends on,
- Resonant frequency	(Fr)
- Height of the substrate (h)
- Dielectric constant of the Substrate (ɛ)

###### Design Equation Document :
---

<embed src="/assets/pdf/formula.pdf" type="application/pdf" height="500px" width="100%"/>

---

A simple online tool to design a patch antenna has been developed in <mark>R Shiny</mark> environment and
available in this <a class="link"> Online link</a> and the source code is shared in **GitHub** as 
<a class="link" href="https://github.com/Bhanuchander210/patchdesign_shiny">patchdesign_shiny</a>.

<kbd class="imgtitle">Patch Antenna Design - R shiny</kbd>

[![img](https://raw.githubusercontent.com/Bhanuchander210/patchdesign_shiny/master/www/patch-design.gif)](https://bhanuchander.shinyapps.io/patch/)
{: .center .imgbrd} 

### Measurement
---

Antenna is a one port device. so only we can calculate <mark>S11 parameter</mark>. A network analyzer is always used to measure the S parameters in RF circuits. After completing the calibration process with network analyzer, Antenna should be connected to that. In frequency domain, the point in S11 curve at where S11 gets minimum value, that means maximum radiation occurs at antenna is the resonant frequency of the patch antenna.

<kbd class="imgtitle">One Port Reflection Co-efficient</kbd>

![Reflection Coefficient](/images/s11.png)
{: .imgbrd }

###### Importance Of Dielectrics
---

The cavity model equation explains us the importance of this dielectrics in patch antenna. Further explanations and the equations related to the dielectrics attached below.

<embed src="/assets/pdf/cavity.pdf" type="application/pdf" height="500px" width="100%"/>

### Multilayer Approach
---

The multi dielectric cavity is created by adding <mark>N number</mark> of layers in to a single cavity shown in given below figure.
 
<kbd class="imgtitle">Single and Multiple dielectric cavities cross section</kbd>

![Multi-dielectric](/images/multi.png)
{: .imgbrd}

In multiple dielectric cavity has <mark>N number</mark> of single dielectric cavities with the same magnetic walls of their own cavity and electric walls are varied depends on their places with combination of another dielectric effects.
So, each dielectric materials has various dielectric constants and effect of each cavity is accepted by another all cavities. 

<p class="noteHeader">So what is happening exactly inside the cavity?</p>

<kbd class="imgtitle">Single layer cavity fringing effect</kbd>

![Single-dielectric-cavity](/images/normfield.png)
{: .imgbrd}


<kbd class="imgtitle">Multi layer cavity increasing fringing effect</kbd>

![Multi-dielectric-cavity](/images/fringing.png)
{: .imgbrd}

The fringing fields affected by the multiple dielectric materials was theoretically shown and this is called as <mark>Fringing effect</mark>. 
Electric fields getting narrower when it crosses higher dielectric constant substrates and ends up with ground plane. In each dielectric the electrical and magnetic components should vary and the field density also vary due to this scenario.
The above mentioned cavity model equation states that each cavity resonate in various frequencies and having various electric walls results in complex effects in the antenna. The difference between the dielectric constant that matters for the change in performance. 

<kbd class="imgtitle">Equivalent Model For Multi-Layer Cavity</kbd>

![Eq-Multi-dielectric-cavity](/images/equivalent.png)
{: .imgbrd}

This multi dielectric cavity can be replaced by an equivalent one dielectric cavity without any performance variation derived from references. Above shown figure shows that the equivalent model for multi dielectric cavity. 

> Further details about the derivation of these equivalent model approach attached in this [<button class="goToBtn">Document</button>](/assets/pdf/eq.pdf)

This is the equivalent dielectric constant equation for the multiple dielectric layers in a single cavity. The equivalent dielectric constant is depending up on the added dielectric constant and thickness of the material.	

### Concept of Patch Sensor
---

From the cavity model resonant frequency equation, we can realize that the relative permittivity of the dielectric is indirectly proportional to resonant frequency. So that multi dielectric layer patch antenna should have shift in the resonant frequency with respect to the equivalent dielectric constant 

<kbd class="imgtitle">Resonant frequency vs. dielectric constant curve for a 5.8 GHz patch</kbd>

![Resonance-dielectric-curve](/images/curve.png)
{: .imgbrd}

Impact of varying dielectric materials inside the patch on frequency is shown above figure. This curve was get from the <mark>5.8GHz Resonant Frequency</mark> patch antenna physical parameters which was designed by dielectric material <mark>FR_4</mark> having dielectric constant <mark>4.4</mark>. It has relation with the resonant frequency and dielectric constant equations which are discussed above is used to plot the curve. When the cavity is replaced dielectric with lower relative permittivity, the resonant frequency should be shifted to a higher value and vice versa. 
So that, this curve is used to determine the unknown dielectric constant of a material.