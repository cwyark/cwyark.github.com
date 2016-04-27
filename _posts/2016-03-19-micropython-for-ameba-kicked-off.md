---
title: "Micropython ports for Ameba board had kicked off !"
description: ""
category: tutorial
tags: [python, rtl8195a, micropython, ameba]
---

#### What's Ameba board ? ####

Ameba board is based on RTL8195A which is introducted by Realtek. RTL8195A is featured in WiFi, NFC and other peripherals like GPIO, SPI, I2C. Developer can build their own wireless product by using Arduino SDK. Though Arduino SDK is suffcient for most applications, but it still need compiled every time when you want to upload your firmware.

Micropython is a lightwdight python interperter specific for microcontroller. Developer can write their python script instead of C lang. As far as I know, python is much easier than C lang, so developer can fouce on their application, not spending lots of time trouble shooting. So that's the reason I port the micropython on Ameba dev board.

#### Why MicroPython ? ####

Check the full document here [mpiot](http://cwyark.github.io/mpiot)

And the forked repository here [github](https://github.com/cwyark/micropython)
