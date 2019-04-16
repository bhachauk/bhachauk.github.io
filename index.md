---
layout: default
---
<div class="tab">
    {% for cats in site.categories %}
    {% if cats[0] != site.postpath %}
    {% assign title = cats[0] | replace: '-',' '| replace: '_', ' '| capitalize %}
    <button class="tablinks" onclick="openTab (event, '{{cats[0]}}', 'tabcontent')">
        {{title}}
    </button>
    {% assign title = nil %}
    {% endif %}
    {% endfor %}
</div>
{% for cats in site.categories %}
{% if cats[0] != site.postpath %}
<div id="{{cats[0]}}" class="tabcontent">
  <div class="txt-center slogan">
     {% for slogs in site.data.catdescription %}
     {% if cats[0] == slogs.name %}
        <h6>{{slogs.text}}</h6>
      {% endif %}
     {% endfor %}
  </div>
  <div class="indexContainer">
  <h3>{{ cats[0] | replace: '-',' '| replace: '_', ' '| capitalize }}</h3>
  <div class="posts">
    {% for post in cats[1] %}
        {% include index-link.html %}
    {% endfor %}
  </div></div>
</div>
{% endif %}
{% endfor %}
{% include welcomenote.html %}

<br>