---
title: "Micropython ports for Ameba board has kicked off !"
description: ""
category: tutorial
tags: [python, rtl8195a, micropython, ameba]
---

#### What's Ameba board ? ####

Ameba board is based on RTL8195A SoC by Realtek. RTL8195A features in WiFi, NFC and other peripherals like GPIO, SPI, I2C, ADC, PWM and H/W crypto engine... Developers(or called Makers) can make their own wireless product by using Arduino SDK(Realtek support).

Though Arduino SDK is suffcient for most applications, it still need compiled every time when you upload your code, even you just want to change one line of your code. For me, it's quite inconvenient. That's the reason why I need a novel way to interface the SoC.

#### Why MicroPython ? ####

Micropython is a lightwight python interperter specific for microcontroller. Developer can write their python script instead of C language. Obviously, python is much easier than C language, so developers can fouce on their application, not spending lots of time trouble shooting. Micropython also provides REPL to help developers accessing API directly instead of compile, program, console printf, compile, program, console printf ......

#### Feature list ####

* Python 3 syntax (not all Python features compatible, don't ask me Django is support or not ...)
* GPIO and external pin interrupt (ISR)
* I2C MASTER
* SPI MASTER/SLAVE (not ready)
* ADC (not ready)
* PWM (not ready)
* RTC and sec/msec/usec delay
* Watchdog
* WiFi Station mode  (AP mode is not ready)
* NFC (not ready)
* Lwip stack
    * echo ping request
    * DHCP or static IP
    * posix like TCP/UDP Server/Client socket 
* SSL (not ready)
* Internal flash filesystem (FatFS with 500KB)
* Standard file open/read/write/close, ex:

``` python
>>> f = open("test.txt", "w")
>>> f.write("test string")
>>> f.close()
```

* Internal FTP server to access internal filesystem

Check the full document here: [mpiot](http://cwyark.github.io/mpiot)

And the forked repository is in here , please feel free to leave you comments or pull request: [github](https://github.com/cwyark/micropython)
