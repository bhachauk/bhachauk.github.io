
<kbd class="imgtitle">Contents</kbd>

1. **[Wireless Transceiver - An Introduction](#introduction)**
1. **[Important Blocks in a Transceiver](#important-blocks)**
1. **[Duplexer](#duplexer)**
1. **[Transmitter section](#transmitter-section)** 
1. **[Receiver section](#receiver-section)**
1. **[Link Budget](#link-budget)**
1. **[Amplifiers](#amplifiers)**
{: .contentBorder .txt-pad}


## Introduction
---

A combined structure of Transmitter and Receiver is commonly known as <mark>Transceiver</mark>. 
This structure shares a single Antenna node for both transmission and reception purpose. 
Satellites are the well known example for a transceiver. That receives and transmits the signal 
simultaneously using a same antenna but in various frequency bands (uplink and downlink).

<kbd class="imgtitle">Satellite Link</kbd>

![Gain](/images/sat.jpg)
{: .imgbrd}

## Important Blocks
<hr>

A Wireless Transceiver should have this basic important blocks,

- Antenna or Antenna array
- Duplexer
- Transmitter section
- Receiver section

<kbd class="imgtitle">Basic Wireless Transceiver Block Diagram</kbd>

![Gain](/images/trans.png)
{: .imgbrd}

## Duplexer
<hr>

For <mark>Bi-directional</mark> communication in a single path, These are implemented by isolating one section from another 
which are connected in a single point. Normally, In transceivers the transmitter path is isolated from the receiver section. 
So that the transmitted signal does not interfere with the receiver section.

<kbd class="imgtitle">Junction Point of Antenna, Transmitter, Receiver</kbd>

![Gain](/images/junc.png)
{: .imgbrd}


These following implementations with RF circuit over the junction point in above shown figure will isolate the transmitter and receiver section.

- Increase the Attenuation between the transmitter and receiver signal
- Circulators used to separate the transmitter and receiver link.
- Some times RF circuit switches also used.

## Transmitter Section
---

In this section, the base band signal converted in to the transmission signal for successive wireless transmission requirements. Mostly modulation, carrier mixing, encoding are the basic process should be done before the transmission. Power Amplifier is used to increase the transmission signal power. After amplifying the signal power it transmitted by the transmitter antenna.
  
## Receiver Section
---

To get the base band message signal, Demodulation and decoding process should be taken. Receiver section has receiver antenna, Low Noise Amplifier, Demodulator and decoder. The received signal should be has a required SNR value. Due to the various effects in transmission, the transmitted signal SNR value getting decreases. Receiver section should be designed to maintain a required SNR by implementing the desired Noise generating RF circuits.

## Link Budget
---

###### What is Link Budget?
---

Before going to <mark>Link Budget</mark> just we can discuss about budgeting. Normally, we do budgeting for journeys, works and etc., For example if you do budget for your journey, you should be followed the steps shown below.

- Initially allocated Money for total expense
- Approx. Spend for Journey
- Approx. Spend for Food
- Approx. Spend for Purchase
- Money saved after all journey

So these are process, you should do while preparing for a journey. Like this, In Wireless transceiver design the transmission signal must spend some power at the transmission medium, each and every devices associated with transceiver due to the losses. Before establishing the link, We need to ensure the reliable receptioin even losses happen. Link Budget is just finding the Pr (Received Signal Power) from the Pt (Transmitted Signal Power) and LL (Link Loss).

###### Equation :

$$
    Received Power (Pr)  =  Transmitted Power (Pt) - Link Loss (LL)
$$ 

where,

**Link Loss** is equals to the Total Loss through the entire link like Free space loss, Attenuation Loss, Thermal Noise and etc.

## Amplifiers
---

The details about the Amplifiers such as like <mark>why ?</mark> and <mark>How ?</mark> are
 detailed in these sections,

- Importance with receiver sensitivity
- Role of an Amplifier
- Amplifier Design Consideration
 
**Types :**
- LNA (Low Noise Amplifier)
- PA (Power Amplifier)

###### Importance with Receiver Sensitivity :
---

From this pre-plane we can check with the required receiver input power with link reception signal power. 
If the ***Pr*** is not sufficient for Receiver, The message signal cannot be detected or received in the receiver. 
Otherwise we can say that the established link is a waste. So that the **Receiver Sensitivity** is the important parameter that plays a important role in Wireless Transceiver Design.

<kbd class="imgtitle">Losses in a Wireless Transceiver link - An example</kbd>

![Gain](/images/ll.png)
{: .imgbrd}

The above shown figure shows the various losses Associated with the link and distributed over the distance 
between the transmitter and receiver. So the final signal power received in the receiver need to meet the 
requirement level called the <mark>Receiver Sensitivity</mark>.

###### Role of an Amplifier
---

We already known that amplifiers are implemented to make some gain in transmission signal considered with 
the wireless transceivers design.Some times the received signal power getting lower than the receiver 
sensitivity. Amplifiers provide some gain to the signal and helps to increase the signal power for receiver 
requirement.

<kbd class="imgtitle">Importance of amplifier</kbd>

![Gain](/images/gain.png)
{: .imgbrd}


###### Amplifier Design Consideration
<hr>

<kbd class="imgtitle">Intercept Points in Amplifier's Output Power Vs Input Power Graph</kbd>

![Plot-Power](/images/pow.png)
{: .imgbrd}

To design a Amplifier, below shown parameters need to considered for better design.

- **Operating Frequency band**
- **Gain**
- **Noise Figure**
- **Output Power 1 dB Compression Point**
- **Output Third Order Intercept Point (OIP3)**
- **Input and Output VSWR**
<br>

The above shown image and parameters explains us that the amplifier gain is saturated after some input power. 
This can be notified by the parameter <mark>1 dB Compression Point</mark>. The intercept point <mark>OIP3</mark> is also a important to 
be notified for amplifier dynamic range. We also know that input and output <mark>VSWR</mark> should be reduced to near **1** value.

- For More details see this [Notes](/assets/pdf/amplifiers.pdf){: .link}

###### Low Noise Amplifier
---

These are used in receiver section to provide gain with focused noise figure. All RF equipments generate <mark>noise figure</mark>, but to maintain the required <mark>SNR</mark> in receiver, The Noise figure of the amplifier need to be noted. Because the amplifer provides greater gain, there is a possibility if it has higher noise figure, it can be amplified through the channel. 
It leads to the higher impact of poor reception in receiver section.
 
###### Power Amplifier
---

This amplifier are focused to meet the requirement of power which is going to be the transmitted power of the antenna. 
By which we can measure the coverage area for particular receivers. This only focused on the output power of the Total transmitter section and what power needed to be transmitted over the antenna.

<p class="noteHeader">This only covers the basics of design considerations of a wireless transceiver. More formulae and discussions still there to be discussed for know more about the design.</p>