---
layout: page
title: Cwyark
tagline: Never give up =)
---
{% include JB/setup %}


Hi, I'm Chester. I'm a software enginner in my regular job. So far I deal with problems in LAN switch protocols, RTOS(Embedded Linux) or basic components' driver and develope diagnostic code.

Except for my regular job, I also learn Linux, Python scripting language and website development. Also,I have some experience with web crawler(spider) and several PaaS platforms like Heroku, Google App Engine (Google Cloud Platform).

If you are interesting with what I've done, please go to `Archives` page to know me more.

Here's my posts list.

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



