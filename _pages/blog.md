---
layout: default
title: Blog Archive
permalink: /blog/
---
# Blog Archive
<hr />

{% for post in site.posts %}
	{% capture currentyear %}
    {{ post.date | date: "%Y"}}
  {% endcapture %}
{% if currentyear != year %}
  {% unless forloop.first %}
  </ul>
  {% endunless %}
  <h3> {{ currentyear }}</h3>
  <ul>
  	{% capture year %}{{currentyear}}{% endcapture %}
{% endif %}
  <li>
    <a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
  </li>
{% endfor %}

