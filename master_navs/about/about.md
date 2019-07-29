---
permalink: /about/
title: About me
---

<br>

![me](/images/bhanuchander_udhayakumar.jpeg)
###### Bhanuchander Udhayakumar
{: .txt-center}
**RF Design | Wireless | Optical Network | Data Science**
{: .txt-center}
<div class="txt-center">
    <a class="github-button" href="https://github.com/bhanuchander210" data-size="large" data-show-count="true" aria-label="Follow @bhanuchander210 on GitHub">Follow @bhanuchander210</a>
</div>
<div class="wrapper-svg">
    <div class="svgBox">
      {% include svg-icons.html %}
    </div>
</div>

<br>

<br>

<div class="abtBtnContainer">
<button onclick="toggle(event,'timeline')" class="cmnBtn currentBtn">Time Line</button>
<button onclick="toggle(event,'profile')" class="cmnBtn">Industry</button>
<button onclick="toggle(event,'skills')" class="cmnBtn">Skills</button>
</div>

{% for job in site.data.profile.industry %}
<div class="profileCard profile show " style="display:none; margin: 5%;">
<a href="{{job.link}}"><img src="{{job.logo}}" align= "right"/></a>
<h4>{{job.company}}</h4>
<b>{{job.location}}</b>
<br>
<h6>{{job.designation}}</h6>
<p>{{job.teams}}</p>
<p style="color: #699">{{job.period}}</p>
<table>
<tr><td style="font-weight:bold">Domain</td><td style="padding-left: 15px">{{job.domain}}</td></tr>
</table>
<h6>Languages</h6>
{% for lang in job.languages %}
{% for master in site.data.skills.languages %}
{% if master.name == lang %}
<div class="inline-block" style="margin: 15px;">
<table>
<tr><td><i class="{{master.code}} fa-3x langicon"></i></td></tr>
<tr><td class="txt-center">{{lang}}</td></tr>
</table></div>
{% endif %}
{% endfor %}
{% endfor %}
</div>
{% endfor %}

{% for prof in site.data.skills %}
<div class="profileCard skills show" style="display:none;margin-top: 5%">
<h6>{{ prof[0] | capitalize }}</h6>
<div class="txt-center">
{% for info in prof[1] %}
<div class="inline-block" style="margin: 15px;">
<table>
<tr><td class="txt-center"><i class="{{info.code}} fa-3x langicon"></i></td></tr>
<tr><td class="bold txt-center">{{info.name}}</td></tr>
</table></div>
{% endfor %}
</div></div>
{% endfor %}

###### Now
{: .timeline .show}

- Currently Learning more about machine learning and deep learning also implementing in required areas with various platforms
 such as Java / Groovy, Python and R.
- Doing some fun works such as,
    - **[Naruto Eye Classifier using Deep Learning - Live](https://bhanuchander210.github.io/naruto_eyes_classification)**
\...
{: .timeline .show}

###### 2017
{: .timeline .show}

- Joined in **[NMSWorks Pvt Ltd](http://nmsworks.co.in)**, IITM Research Park, Chennai.
- Worked as a Graduate Technical Intern at **[Visteon Technical and Service Center, Chennai](http://www.visteon.com/).**
- Did Intern-Project in visteon and submitted the thesis titled as **[Integration of Bluetooth Wireless Stack for Automotive INVANET Communication](http://ijesc.org/upload/0937dc48f9d484fb58073aea2fbeccfd.Integration%20of%20Bluetooth%20Wireless%20Stack%20for%20Automotive%20INVANET%20Communication.pdf)**.
- Graduated in M.E (Wireless technology) from **[Anna University – MIT Campus](http://www.mitindia.edu/en/)**. 
- Started to learn and write about **[Groovy](https://github.com/Bhanuchander210/Learn_Groovy), [Mysql](https://github.com/Bhanuchander210/Mysql), [Python](https://github.com/Bhanuchander210/my_python_tutorial_1), [Optical Tx Networks](https://github.com/Bhanuchander210/Learn_Optical)**.
{: .timeline .show}

###### 2016
{: .timeline .show}

- Did a interdisciplinary project work with Automobile Engineering funded by **[CTDT- Anna University](http://ctdt.annauniv.edu/)** which is titled as Analysis On Efficient Bio-diesel Dual Fuel Engine With EPFIS.
- Some of the other works related to the academic discipline such as, 
    1. Design And Analysis Of Inset Feed Rectangular Patch Antenna With Multiple Dielectric Layers.
    2. Measurement Of Material Dielectric Constant Using A Rectangular Cavity Patch <mark>Sensor</mark>.
    3. Protocol Analysis on <mark>In-Vanet</mark> Communication Using NS2.
{: .timeline .show}

###### 2015
{: .timeline .show}

- Graduated in B.E (Electronics and Communication Engineering) from **[Government College of Engineering, Tirunelveli](http://www.gcetly.ac.in/)** with the thesis submission on Railway Security System with Wireless Communication.
{: .timeline .show}

###### 2014
{: .timeline .show}

- Did Initial-Level Projects related Automated Vehicle Using <mark>Arduino</mark> and submitted as a mini-project.
{: .timeline .show}

###### 2013
{: .timeline .show}

- Got ASOC Restricted Grade <mark>Ham Radio</mark> Certification from the **[WPC Wing](http://www.wpc.dot.gov.in/)**, Ministry of Communications - India.
- Did some work with the project Solar Flier, a mini-plane powered by solar panels. 
{: .timeline .show}

###### 2011
{: .timeline .show}

- Completed Higher Secondary Schools on Bio-Maths at Devangar Higher Secondary School, Aruppukottai with score 93.75 %.
{: .timeline .show}

###### 2009
{: .timeline .show}

- Completed SSLC at Devangar Higher Secondary School, Aruppukottai with score 94.4 %.
- Completed Visharadh Poorvardh a Hindi literacy Examination organized by <mark>Dakshina Bharat Hindi Prachar Sabha</mark>.
{: .timeline .show}