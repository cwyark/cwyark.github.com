---
title: "How GPIO works in MicroPython Ameba ?"
description: ""
category: tutorial
tags: [python, rtl8195a, micropython, ameba]
---

It's quite simple to handle a GPIO pin in micropython.

```python
>>> from hardware import Pin
>>> a = Pin("PA_5", dir=Pin.OUT)
>>> a.toggle()
>>> a.value(1)
>>> a.value(0)
```
When you call the method a.toogle(), PA_5 will reverse it's IO status. a.value(x) is to directly to set the IO value. (0 or 1 is available)

Here's my little experiment to see how fast I can to toggle the GPIO ... (The tested pin is PA_5, if you don't know the pin name, check this [url](http://cwyark.github.io/mpiot/rtl8195a/intro.html#realtek-ameba-board))

```python
>>> from hardware import Pin
>>> a = Pin("PA_5", dir=Pin.OUT)
>>> for i in range(100):
....    a.toggle()
>>>
```

![gpio toggle](/images/2016-03-19/gpio_toggle.PNG)

As you can see, each interval between edges are about 26us, which means the interval between every a.toggle() is 26us. I think it's sufficient to simulate a PWM by GPIO, even SPI or I2C signals.

And there's something you should know: the voltage range is `0 ~ 3.3V`. I'not sure it can tolerate `0 ~ 5V`.

For more informations, you could check this [url](http://cwyark.github.io/mpiot/rtl8195a/modules/hardware.html).
