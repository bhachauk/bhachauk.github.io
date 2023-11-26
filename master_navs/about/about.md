---
permalink: /about/
title: About me
---

<br>

![me](/images/bhanuchander_udhayakumar.jpeg)
###### Bhanuchander Udhayakumar
{: .txt-center}
**Data Science | Full Stack | AWS Certified | TMForum Certified**
{: .txt-center}
<div class="txt-center">
    <a href="https://twitter.com/Bhanuchander_U?ref_src=twsrc%5Etfw" class="twitter-follow-button" data-size="large" data-show-count="true">Follow @Bhanuchander_U</a><script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
    <a class="github-button" href="https://github.com/bhachauk" data-size="large" data-show-count="true" aria-label="Follow @bhachauk on GitHub">Follow @bhachauk</a>
    <script src="https://apis.google.com/js/platform.js"></script>
    <div class="g-ytsubscribe" data-channelid="UC2JbRYaC-USnGgzEi2uiaqQ" data-layout="default" data-theme="dark" data-count="default"></div>
    <!--[![Downloads](https://i1.wp.com/stackoverflow.com/users/flair/8331235.png)](https://stackoverflow.com/users/8331235/bhanuchander-udhayakumar)-->
</div>
<div class="wrapper-svg">
    <div class="svgBox">
      {% include svg-icons.html %}
    </div>
</div>

<br>

<br>

<div class="abtBtnContainer">
<button onclick="toggle(event,'summary')" class="cmnBtn currentBtn">Summary</button>
<button onclick="toggle(event,'profile')" class="cmnBtn">Industry</button>
<button onclick="toggle(event,'skills')" class="cmnBtn">Skills</button>
<button onclick="toggle(event,'timeline')" class="cmnBtn">Time Line</button>
<button onclick="toggle(event,'moocs')" class="cmnBtn">Moocs</button>
<button onclick="toggle(event,'personal')" class="cmnBtn">Personal</button>
</div>


<br><br>


Hi there, I am currently working as a **Senior Software Engineer** in chennai. I love to develop full stack applications using <mark>Python</mark>,
<mark>Java</mark>, <mark>Groovy</mark>, <mark>R</mark> and <mark>JavaScript</mark>. I am working on **Artificial Intelligence** based projects mostly around **Sequence models** and **Computer Vision** for both
Cloud environment and EDGE device.
Also familiar with **docker**, **kubernetes** for developing cloud natured full stack application (**GCP**, **AWS** and **Azure**).
I like to use text editor <mark>sublime</mark>, also the **IDE**s <mark>PyCharm</mark> and <mark>IntelliJ</mark>.
<br>
<br>
During my academics, worked as an graduate intern for the **Automotive Embedded Wireless** based projects and designed few **Patch Antennas** and **RF filters** by
familiarized with the advanced tools such as [ADS](https://www.keysight.com/in/en/products/software/pathwave-design-software/pathwave-advanced-design-system.html) and [CST](https://www.3ds.com/products-services/simulia/products/cst-studio-suite/).
<br>
<br> 
In my free time, I do blogging and developing **github pages** from my random ideas and also like to play MOBA games such as [Dota 2](https://www.dota2.com/). Also as a master degree graduate in **Wireless technology**,
I love to contribute in the open source software development for **Machine Learning**, **Antennas / RF Design**, and **Visualization* areas.
{: .show .summary style="margin: 0px 50px 100px 50px; font-size: 40;"}


<div class="profileCard personal show txt-center" style="display:none;">
<h6>Inspired Fictional Characters</h6>
{% for char in site.data.personal.inspired_chars %}          
        <a href="{{char.link}}" style="align:left;display:inline-block;">
            <img src="{{ site.baseurl }}{{char.logo}}" style="width:50px;height:auto;"/>
        </a>
{% endfor %}
</div>


<div class="profileCard personal show txt-center" style="display:none;">
<h6>Favourite Games</h6>
{% for game in site.data.personal.games %}          
        <a href="{{game.link}}" style="align:left;display:inline-block;">
            <img src="{{ site.baseurl }}{{game.logo}}" style="width:50px;height:auto;"/>
        </a>
{% endfor %}
</div>


{% for job in site.data.profile.industry %}
<div class="profileCard profile show " style="display:none; margin: 5%;">
<a href="{{job.link}}"><img src="{{job.logo}}" align= "right"/></a>
<h4>{{job.company}}</h4>
<b>{{job.location}}</b>
<br>
<h6>{{job.designation}}</h6>
<p >{{job.teams}}</p>
<p style="color: #699">{{job.period}}</p>
<table>
<tr><td style="font-weight:bold">Domain :</td><td style="padding-left: 15px;">{{job.domain}}</td></tr>
</table>
<h6>Languages</h6>
{% for lang in job.languages %}
{% for master in site.data.skills.languages %}
{% if master.name == lang %}
<div class="inline-block" style="margin: 15px;">
<table>
<tr><td align="center"><i class="{{master.code}} fa-3x"></i></td></tr>
<tr><td align="center">{{lang}}</td></tr>
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
<tr><td><i class="{{info.code}} fa-3x"></i></td></tr>
<tr><td class="txt-center"> {{info.name}}</td></tr>
</table></div>
{% endfor %}
</div></div>
{% endfor %}

{% for tl in site.data.timeline %}
<div class="timeline show">
    <div class="profileCard">
        <h6>{{tl.title}}</h6>
        {% for year in tl.years.year %}
        <p>{{year.title}}</p>
        <ul>
        {% for work in year.works %}
            {% if work.link %}
                <li><a href="{{work.link}}">{{work.note}}</a></li>
            {% else %}
                <li><p>{{work.note}}</p></li>
            {% endif %}
            {% if work.info %}
                <p class="refbox">{{work.info}}</p>     
            {% endif %}     
        {% endfor %}
        </ul>
        {% endfor %}
    </div>
</div>
{% endfor %}

<div class="slideshow-container moocs show">
  {% for link in site.data.moocs.links %}
  <div class="mySlides fade">
    <img src="{{link}}" style="width:70%">
  </div>
  {% endfor %}
  <a class="prev" onclick="plusSlides(-1)">&#10094;</a>
  <a class="next" onclick="plusSlides(1)">&#10095;</a>
</div>
<div style="text-align:center" class="moocs show">
  {% assign i = 0 %}
  {% for link in site.data.moocs.links %}
    {% assign i = i | plus:1 %}
    <span class="dot" onclick="currentSlide({{i}})"></span>
  {% endfor %}
</div>
<script>plusSlides(1);plusSlides(-1)</script>
<br>