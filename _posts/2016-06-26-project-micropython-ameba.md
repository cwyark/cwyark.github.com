---
title: "[Project]Micropython@Ameba ports"
tagline: "A novel way to develope application on RTL8195A"
description: "A novel way to develop application on RTL8195A"
category: projects
tags: [ameba, micropython, python, rtl8195a]
---

Ameba board is based on Realtek RTL8195A SoC. RTL8195A features in WiFi, NFC, and other peripherals like GPIO, SPI, I2C, ADC, PWM and H/W crypto engine. Ameba board supports Arduino SDK, however, when I'm developing an application, I often compile, program, console printf, compile, program and console printf .... so I start to port micropython to Ameba board. By the help of micropython@Ameba, developers can facilitate developing applications instead of trouble shooting with compiled language.

<!--more-->

Related posts

<ul>
    {% for post in site.posts %}
        {% if post.project contains "micropython_ameba" %}
            <li>
                <a href="{{ post.url }}">{{ post.title }}</a>
            </li>
        {% endif %}
    {% endfor %}
</ul>
