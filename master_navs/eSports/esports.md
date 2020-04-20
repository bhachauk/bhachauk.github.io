---
permalink: /esports
title: E-Sports
---

<h1 class="gitHubTitle">{{ page.title}}</h1>
<div class="txt-center">
<ul class="cell cellGh">
  {% for proj in site.data.esports %}
  <a href="{{proj.link}}" target="_blank">
  <li>
    <img src="{{proj.img}}"/>
    <p>ID: {{ proj.id}}</p>
  </li></a>
  {% endfor %}
</ul>
</div>
<br>