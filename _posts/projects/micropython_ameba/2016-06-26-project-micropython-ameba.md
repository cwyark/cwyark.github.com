---
title: "[Project] Micropython@RTL9105A ports"
tagline: "A novel way to develope application on RTL8195A"
description: "A novel way to develop application on RTL8195A"
category: projects
tags: [ameba, micropython, python, rtl8195a]
---

Ameba board is based on Realtek RTL8195A SoC. RTL8195A features in WiFi, NFC, and other peripherals like GPIO, SPI, I2C, ADC, DAC, PWM, SDIO and H/W crypto engine.

![MicroPython@RTL8195A](/images/projects/mp_rtl8195a/project_mp_rtl8195a.png)

<!--more-->

Ameba board supports Arduino SDK, however, when I'm developing an application, I often compile, program, console printf, compile, program and console printf .... that is really waste of time. So I start to port micropython to Ameba board. By the help of micropython@RTL9105A, developers can facilitate developing applications instead of trouble shooting with compiled language.

Check the full document here: [mpiot/RTL8195A](http://cwyark.github.io/mpiot/rtl8195a/install.html)

And the forked repository is in here , please feel free to leave you comments or pull request: [github](https://github.com/cwyark/micropython)

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
