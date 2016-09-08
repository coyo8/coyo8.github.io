---
layout: default
permalink: /projects/
---

<div class="project-container">
<!-- Sort pages based on their weights -->
{% assign c_list = site.categories | sort:"weight"  %}
{{c_list}}
{% for category in c_list %}
  <div class="box-item">
      <a href="{{ category.url }}">
        <p> {{category.title}} </p>
      </a>
  </div>
{% endfor %}


