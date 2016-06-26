---
title: "[Project]Micropython@Ameba ports"
tagline: "A novel way to develope application on RTL8195A"
description: "A novel way to develop application on RTL8195A"
category: projects
tags: [ameba, micropython, python, rtl8195a]
---

<!--more-->

<ul>
    {% for post in site.posts %}
        {% if post.project contains "micropython_ameba" %}
            <li>
                <a href="{{ post.url }}">{{ post.title }}</a>
            </li>
        {% endif %}
    {% endfor %}
</ul>
