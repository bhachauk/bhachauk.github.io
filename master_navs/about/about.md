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
    <b>Software Development | AWS | Aruba | TMForum Certified</b><br><br>
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
<li>Having <b><span id="experience"></span> of experience</b> in software development.</li>
<li>Domains familiar with: Network Access Control (NAC), Network Management System (NMS),  Microservices, Machine Learning and Deep Learning.</li>
</ul>
<br>
<div style="display: flex; justify-content: space-between;">
<img width="60" height="60" src="https://img.icons8.com/fluency/60/java-coffee-cup-logo.png" alt="java-coffee-cup-logo" title="Java"/>
<img width="60" height="60" src="https://img.icons8.com/color/60/python.png" alt="python" title="Python"/>
<img width="60" height="60" src="https://img.icons8.com/color/60/spring-logo.png" title="Spring boot"/>
<img width="60" height="60" src="https://img.icons8.com/officel/60/react.png" title="React"/>
<img width="60" height="60" src="https://img.icons8.com/color/144/flutter.png" title="Flutter"/>
</div>
<br>
<div style="display: flex;">
<img width="60" height="60" src="https://img.icons8.com/nolan/60/apache-kafka.png" title="Kafka"/>
<img width="60" height="60" src="https://img.icons8.com/color/144/mysql-logo.png" title="MySQL"/>
<img width="60" height="60" src="https://img.icons8.com/color/144/oracle-logo.png" title="Oracle"/>
<img width="60" height="60" src="https://img.icons8.com/color/144/postgreesql.png" title="Postgres"/>
<img width="60" height="60" src="https://img.icons8.com/color/60/splunk.png" title="Splunk"/>
<img width="60" height="60" src="https://img.icons8.com/color/60/amazon-web-services.png" title="AWS"/>
<img width="60" height="60" src="https://img.icons8.com/color/60/google-cloud.png" title="GCP"/>
</div>
<br>
<div style="display: flex;">
<img width="60" height="60" src="https://img.icons8.com/color/60/docker.png" title="Docker"/>
<img width="60" height="60" src="https://img.icons8.com/color/60/kubernetes.png" title="K8s"/>
<img width="60" height="60" src="https://img.icons8.com/color/60/tensorflow.png" title="Tensorflow"/>
<img width="60" height="60" src="https://img.icons8.com/material/60/keras.png" title="Keras"/>
<img width="60" height="60" src="https://img.icons8.com/material-sharp/60/django.png" title="Django"/>
<img width="60" height="60" src="https://img.icons8.com/color/60/jira.png" title="Jira"/>
</div>
<br>
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
        months = "+"
    }
    document.getElementById('experience').textContent = `${years}+ years`;
</script>


{% for job in site.data.profile.industry %}
<div class="profileCard1 profile show " style="display:none; margin: 5%;">
<table class="xptable">
<tr>
<td style="width: 20%; text-align: center;border-right: 1px dotted gray;"><a href="{{job.link}}"><img src="{{job.logo}}"/></a><br><b>{{job.location}}</b></td>
<td style="width: 50%;"><h6>{{job.designation}}</h6><br><p>{{job.teams}}</p></td>
<td style="width: 30%;"><p>{{job.period}}</p></td>
</tr>
</table>
<div class="content" style="display: none;">
<b>{{job.location}}</b>
<br>
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
