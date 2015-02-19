---
layout: page
title: Cwyark
tagline: Never give up =)
---
{% include JB/setup %}


Hi, I'm Chester. I'm a software enginner in my regular job. So far I deal with some problems in LAN switch like L2 Protocols, RTOS(Embedded Linux) or basic components' driver(MAC/PHY/CPU/Flash/RAM). Except for my regular job, I also learn Linux, Python scripting language and website development (HTML/CSS/Javascript).

I also have some experience with web crawler development and several SaaS based in multiple PaaS platforms like Heroku, Google App Engine(Google Cloud Platform) and OpenShift. If you are interesting with what I've done, please go to `Archives` page to know me more.

Here's my posts list.

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



