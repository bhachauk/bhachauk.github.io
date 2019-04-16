### Optical Networks basics and Common words
---

<kbd class="imgtitle">Contents</kbd>

- [Getting Started](#getting-started) <br>
- [Architecture of Network](#architecture-of-network)<br>
- [Properties of a Good Optical Network](#properties-of-a-good-optical-network)<br>
- [Multi Technology Network Elements ](#multi-technology-network-elements)<br>
- [Optical Network Ports](#optical-network-ports)<br>
- [Equipment Modelling](#equipment-modelling)<br>
- [Roles of Management System](#roles-of-management-system)<br>
- [Transmission Technologies and signals](#transmission-technologies-and-signals)<br>
- [Signal vs Rate Table](#signal-table)<br>
- [Communication Interface](#communication-interfaces-in-optical-lines)<br>
- [OverAll Network Map](#overall-network-map)<br>
{: .contentBorder .txt-pad}


### Getting Started
---


###### How it would be?
---

All Optical Network links are connected to the internet through the <mark>MPLS Multi Protocol Lable switching</mark>. 
So that would be the gateway to the internet for optical lines. Which is also has <mark>Session Initiation Protocol - SIP</mark> with it. 
The figure shown below explains the connectivity.

###### Normal Blocks of an Optical Network 
---

<kbd class="imgtitle">Optical Network Block</kbd>

![ems](/images/first.jpg)
{: .imgbrd}

###### Links Associated with the above shown Image

- Optical lines
- ADSL (Asynchronous Digital Synchronous Link)
- EFM links (Ethernet Fiber Modem Link)

<mark>SIP</mark> will helps for the functions shown below,

###### Functions

<p class="noteHeader">1. User Registration</p> 
- It collects the user locations and details who are participating.

<p class="noteHeader">2. User Availability</p> 
- It determine the user availability whether they will answer call.

<p class="noteHeader">3. Session Setup</p> 
- It controls the end point telephone to be ring or not.

<p class="noteHeader">3. Session Management</p> 
- It has total control to manage the calls like changing into 3 way calls conference, call termination, Transfer call, etc.,

###### What MPLS does?

- It encapsulates packets of various network protocols.
- It supports the technologies like T1/E1, ATM, Frame Relay, and DSL.
- Due to the switching methods like ASIC, TCAM and CAM its goal to increase speed is no longer relevant.
- It is confined by the limited traffic engineering.

### Architecture of Network

<hr>
Due to this connection environment, The network looks like <mark>N number</mark> of spanning trees are conncted 
to the main end point of the network which manages the totoal network.

<kbd class="imgtitle">Basic Architecture of an Optical Network</kbd>

![ems](/images/second.jpg)
{: .imgbrd}

###### MSTP

<mark>Multiple Spanning Tree Protocol</mark> is the protocol which is used in this optical Transportation environment. 
This is commonly known in the <mark>Synchronous digital hierarchy - SDH</mark> topology.


### Properties of a Good Optical Network

<hr>

It should have,

1. SDH - Synchronous Digital Hierarchy (or) SONET Synchronous Optical Hierarchy
2. DWDM - Dense Wavelength Division Multiplexing
3. Fault Management and Rout Cause Analysis
4. Northbound and Southbound Interfaces
	1. CORBA
	2. MTOSI
	3. OSS/J
5. PTP Physical Terminal Point
6. CTP Connection Terminal Point
7. ME Managed Element (view by the NMS System)
8. SNC Sub-network Connection
	1. aEnd
	2. zEnd

### Multi Technology Network Elements

<hr>

It is widely manages and supports the management of these technologies: 

- SONET/SDH, 
- PDH, Plesiochronous Digital Hierarchy
- DWDM, 
- Ethernet, 
- DSL, Digital Subscriber Link
- ATM, Asynchronous Transfer Mode 
- Frame Relay, and Control Plane management.


###### SDH/SONET

- Synchronous clock operation followed in the network elements. It is better than PDH.
- SDH is the only key to use multi point networking. 

###### PDH

- <mark>Plesiochronous</mark> means variable clocks are followed in multiplexing areas. Due to that  each node will differ within tolerance of few clock periods.
- PDH is not suitable for growing network Traffic.

### Optical Network Ports

<hr>

###### PTP

- This is the <mark>Physical Terminal Point</mark> of a network where clients exists.
- Physical Terminal Point contains more or one CTP.

###### CTP

- <mark>Connection Terminal Port</mark> communicates through the PTP.
- This is the actual end of the client where the service ends.
- CTP Associated with PTP by <mark>STM-4 (Synchronous Transport Module - 4)</mark> prototype.


### Equipment Modelling
---

###### Network Elements
---

These can be separated as shown below,

* **Manageable Components**

    - Circuit Pack/Field replaceable unit
    - Card
    - Fan Unit
    - Power Supply

* **UnManageable Components**

    - Rack
    - Shelf
    - Slot
    - Sub_Slot

Normally the port is the end of the network that can be derived by,

<span class="left"><kbd class="lang">Port Name</kbd></span>
<span class="right"><kbd class="lang">text</kbd></span>

```
    Port    =          /rack=1/shelf=1/slot=1/sub_slot=1/port=2
```

###### Path of the Circuit to the Cross connection

<span class="left"><kbd class="lang">Link between Objects</kbd></span>
<span class="right"><kbd class="lang">Graph</kbd></span>

```
Service/ Circuit ---->  SNC_n ----> Route_n ----> CC_n
```

<p class="noteHeader">Note: All components above are interconnected by their own siblings</p>

### Roles of Management System
<hr>

<kbd class="imgtitle">Element Management System</kbd>

![ems](/images/ems.jpg)
{: .imgbrd}

##### CC_n
 
Cross Connection is the bridge between two <mark>CTP</mark>. It can be protected. It allows the connection which is in active.

##### PGP

Pretty Good Privacy consists of,

- Compatibility
- Confidentiality
- Digital signatures
- Web of trust
- Certificates

Above shown Multi-level check has been done for the privacy through the PGP.

### Transmission Technologies and Signals
---

###### Technologies
---

- PDH	
- ETHERNET 
- SDH	
- OTN
	
###### Signal
---

- E1, E2, E3, E4
- Ethernet
- STM_1, STM_4, STM_16, STM_64
- OTU_1, OTU_2, OTU_3, OTU_4 

###### Bandwidth
---

- 2 - 140 (2, 8, 34, 140 Mbps)
- 1-10 Gbps
- 0.155, 0.622, 2.5, 10 Gbps
- 2.5, 10, 40, 100 Gbps


### Signal Table
---

<style>
table.info {
    font-family: arial, sans-serif;
    border-collapse: collapse;
    width: 100%;
}

td.info, th {
    border: 1px solid #000000;
    text-align: left;
    padding: 8px;
}

th{
     font-weight:bold;
     color: #902f3f;
}
</style>

<center>
<p align="center">
<table style="width:50%" class="info">
  <tr>
    <th>Signal Type</th>
    <th>Rate</th> 
  </tr>
  <tr>
    <td class="info">E1</td>
    <td class="info">2 Mbps</td> 
  </tr>
  <tr>
    <td class="info">E2</td>
    <td class="info">8 Mbps</td> 
  </tr>
    <tr>
    <td class="info">E3</td>
    <td class="info">32 Mbps</td> 
  </tr>
  <tr>
    <td class="info">E4</td>
    <td class="info">140 Mbps</td> 
  </tr>
  <tr>
    <td class="info">Ethernet</td>
    <td class="info">1-10 Gbps</td> 
  </tr>
  <tr>
    <td class="info">STM_1</td>
    <td class="info">0.155 Gbps</td> 
  </tr>
  <tr>
    <td class="info">SMT_4</td> 
    <td class="info">0.622 Gbps</td>
  </tr>
  <tr>
    <td class="info">STM_16</td>
    <td class="info">2.5 Gbps</td> 
  </tr>
    <tr>
    <td class="info">STM_64</td>
    <td class="info">10 Gbps</td> 
  </tr>
  <tr>
    <td class="info">OTU_1</td>
    <td class="info">2.5 Gbps</td> 
  </tr>
    <tr>
    <td class="info">OTU_2</td>
    <td class="info">10 Gbps</td> 
  </tr>
  <tr>
    <td class="info">OTU_3</td>
    <td class="info">40 Gbps</td> 
  </tr>
  <tr>
    <td class="info">OTU_4</td>
    <td class="info">100 Gbps</td> 
  </tr>
</table>
</p>
</center>


##### Communication interfaces in Optical lines

---

- Northbound Interface (Low level element to High level element)
- Southbound Interface (High level element to Low level element)


##### OverAll Network Map

<hr>
---

<embed src="/assets/pdf/Bhanu_OTNMS.pdf" type="application/pdf" height="500px" width="100%"/>

###### Reference
---

For further information see also : <a class="link" href="http://www.rfwireless-world.com/Terminology/PDH-vs-SDH.html">RF-wireless-world</a>
- https://www.juniper.net/documentation/en_US/junos/topics/concept/interface-security-t1-and-e1-understanding.html

