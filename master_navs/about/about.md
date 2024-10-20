---
permalink: /about/
title: About me
---

<br>
<link href="https://languages.abranhe.com/logos.css" rel="stylesheet">

<div class="column1">
<img src="/images/bhanuchander_udhayakumar.jpeg">
<div class="txt-center">
    <h2>Bhanuchander Udhayakumar</h2>
    <b>Software Developer | AWS | Aruba | TMForum Certified</b><br><br>
    <!-- <a href="https://twitter.com/Bhanuchander_U?ref_src=twsrc%5Etfw" class="twitter-follow-button" data-size="large" data-show-count="true">Follow @Bhanuchander_U</a><script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>-->
    <a class="github-button" href="https://github.com/bhachauk" data-size="large" data-show-count="true" aria-label="Follow @bhachauk on GitHub">Follow @bhachauk</a>
    <!--<script src="https://apis.google.com/js/platform.js"></script>
    <div class="g-ytsubscribe" data-channelid="UC2JbRYaC-USnGgzEi2uiaqQ" data-layout="default" data-theme="dark" data-count="default"></div>-->
    <!--[![Downloads](https://i1.wp.com/stackoverflow.com/users/flair/8331235.png)](https://stackoverflow.com/users/8331235/bhanuchander-udhayakumar)-->
</div>
<div class="wrapper-svg">
    <div class="svgBox">
      {% include svg-icons.html %}
    </div>
</div>
</div>

<div class="column2">
<div class="abtBtnContainer" style="margin-bottom: 50px;">
<button onclick="toggle(event,'summary')" class="cmnBtn currentBtn">Summary</button>
<button onclick="toggle(event,'profile')" class="cmnBtn">Experience</button>
<button onclick="toggle(event,'moocs')" class="cmnBtn">Moocs</button>
</div>
<br>

<div class="show summary" style="margin: 0px 50px 100px 50px; font-size: 40;">
<ul>
<li>Completed my <b>Master's Degree</b> in <b>Wireless Technologies</b> at <b>Anna University - MIT Campus.</b></li>
<li>Having <b><span id="experience"></span> of experience</b> in the software development industry.</li>
<li>Domains familiar with: Network Access Control (NAC), Network Management System (NMS),  Microservices, Machine Learning and Deep Learning.</li>
</ul>
<br>
<div style="display: flex;">
<a href="https://www.tmforum.org/training-certification/certification-listing/"><img src="https://www.tmforum.org/wp-content/uploads/2020/06/AIDM-badge.png" width="75"/></a>
<a href="https://bhachauk.github.io/images/aws_ccp.png"><img src="https://images.credly.com/images/00634f82-b07f-4bbd-a6bb-53de397fc3a6/image.png" width="75"/></a>
</div>
</div>

<script>
    const joiningDate = new Date('2017-07-01');
    const currentDate = new Date();
    let years = currentDate.getFullYear() - joiningDate.getFullYear();
    let months = currentDate.getMonth() - joiningDate.getMonth();
    if (months < 0) {
        years--;
        months += 12;
    }
    if (months > 0) {
        months = `and ${months} months`;
    } else {
        months = "+";
    }
    document.getElementById('experience').textContent = `${years} years ${months}`;
</script>


{% for job in site.data.profile.industry %}
<div class="profileCard profile show " style="display:none; margin: 5%;">


<table style="display: flex;">
<tr><td>
<div style="margin-right: 30px; min-width: 30%; min-height: 70%;text-align: center;"><a href="{{job.link}}"><img src="{{job.logo}}"/></a></div>
</td>
<td>
<div>
<h4>{{job.designation}}</h4>
<b>{{job.company}}, {{job.location}}</b>
<p >{{job.teams}}</p>
<p style="color: #699">{{job.period}}</p>
</div>
</td></tr>
</table>
</div>
{% endfor %}

<script>
var coll = document.getElementsByClassName("collapsible");
var i;

for (i = 0; i < coll.length; i++) {
  coll[i].addEventListener("click", function() {
    this.classList.toggle("active");
    var content = this.nextElementSibling;
    if (content.style.display === "block") {
      content.style.display = "none";
    } else {
      content.style.display = "block";
    }
  });
}
</script>

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
</div>
