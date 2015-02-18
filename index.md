---
layout: page
title: Cwyark
tagline: Never give up =)
---
{% include JB/setup %}


Hi, I'm Chester. I'm a software enginner with my regular job. Currently, I deal with some problems in LAN switch no matter L2 Protocols or basic components like MAC/PHY/CPU/Flash/RAM. Except for my regular job, I also learn Python scripting and web site development (HTML/CSS/Javascript). I alsoe have some experience with several PaaS platform like Heroku, Google App Engine(Google Cloud Platform) and OpenShift.

Here's my posts list.

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



