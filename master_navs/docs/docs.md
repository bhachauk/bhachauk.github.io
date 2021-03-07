---
permalink: /docs
title: Docs
---

<body>
<h1 class="gitHubTitle">{{ page.title}}</h1>
<div class="txt-center">
<ul class="cell cellGh">
  {% for proj in site.data.docs %}
  <a href="{{proj.link}}" target="_blank">
  <li>
    <img src="{{proj.img}}"/>
    <h3>{{ proj.name }}</h3>
    <p>{{ proj.desc}}</p>
  </li></a>
  {% endfor %}
</ul>
</div>
<br>
</body>