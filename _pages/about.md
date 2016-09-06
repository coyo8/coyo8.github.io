---
layout: default
title: About me
permalink: /about/
---

## About me

<img class="profile-picture" src="{{ site.url }}/assets/images/profile.jpg">


Welcome to my virtual realm! I make softwares, teach students and help lazy brain grow. I like everything about computers and science behind learning.

I am currently a course manager at [Udacity][udacity] leading [Full Stack Nanodegree][fsnd] program. I am also a member of [Python Software Foundation][PSF]. I’ve worked at [The Walt Disney Company][disney] and [CMU][cmu] as a Software Engineer and HCI Researcher respectively.

To get updated with my newest projects, go straight to my [GitHub][github] account. Apart form these if you would like to stumble upon my older writings which still reside in my [medium][medium] blog.

The site name, Rudrakos (pronounced “roo d-ruh kohs”) is a combination of two sanskrit words i.e. [Rudra][rudra] (mightiest of mighty) and Kosa (pocket), meaning container of omnipotent.

Still haven't found what you are looking for or want to meet for a coffee? Feel free to contact me.

<div class="social-icon"><a id="pdf-ic" href="{{ site.url }}/assets/pdf/cv.pdf" target="_blank">
    <i class="fa fa-file-pdf-o social-icon"></i> Download CV
  </a>
</div>

---

## Contact me

* Email: [rahul@rudrakos.com](mailto:rahul@rudrakos.com)

* Phone: [+91-9819737113](tel:+91-9819737113)

---

## Follow me
<div class="social-icon">
  {% if site.trivium.social.twitter %}
  <a id="twitter-ic" href="https://twitter.com/{{ site.trivium.social.twitter }}" target="_blank">
    <i class="fa fa-twitter fa-lg"></i>
  </a>
  {% endif %}
  {% if site.trivium.social.github %}
  <a id="git-ic" href="https://github.com/{{ site.trivium.social.github }}" target="_blank">
    <i class="fa fa-github-square fa-lg"></i>
  </a>
  {% endif %}
  {% if site.trivium.social.facebook %}
  <a id="fb-ic" href="https://facebook.com/{{ site.trivium.social.facebook }}" target="_blank">
    <i class="fa fa-facebook-square fa-lg"></i>
  </a>
  {% endif %}
  {% if site.trivium.social.gplus %}
  <a id="gplus-ic" href="https://plus.google.com/{{ site.trivium.social.gplus }}" target="_blank">
    <i class="fa fa-google-plus-square fa-lg"></i>
  </a>
  {% endif %}
  {% if site.trivium.social.medium %}
  <a id="medium-ic" href="https://medium.com/@{{ site.trivium.social.medium }}" target="_blank">
    <i class="fa fa-medium fa-lg"></i>
  </a>
  {% endif %}
</div>


[github]: <https://github.com/{{ site.trivium.social.github }}>
[medium]: <https://medium.com/@{{ site.trivium.social.medium }}>
[udacity]: <https://udacity.com>
[fsnd]: <https://www.udacity.com/course/full-stack-web-developer-nanodegree--nd004>
[PSF]: <https://www.python.org/psf>
[rudra]: <https://en.wikipedia.org/wiki/Rudra>
[cmu]: <https://www.hcii.cmu.edu/>
[disney]: <http://www.disneyinteractive.com/>
