---
title: "How to control WiFi in you micropython@Ameba"
description: ""
category: tutorial
project: micropython_ameba
tags: [python, rtl8195a, micropython, ameba]
---

You can control your MicroPython@Ameba's WiFi in few lines.

<!--more-->

!!New content updated in 2016-09-18!!

Station mode and AP mode are available in RTL8195A's low level driver, and MicroPython@Ameba is also supported.

**Station mode example**

Here's an example for station mode. Note that when connection is failed, it will raise an OSError exception.

``` python
>>> from wireless import WLAN
>>> wifi = WLAN(mode=WLAN.STA)
>>> my_ssid = "MY-AP-SSID"
>>> my_auth = (WLAN.WPA2_AES_PSK, "MY-AP-PASSWORD")
>>> try:
...     wifi.connect(ssid=my_ssid, auth=my_auth, dhcp=True)
... except OSError as e:
...     print("Connect to %s failed" % my_ssid)
...     print(e)
```

Authenication fail may caused by the wrong ssid, wrong password or the wrong authenication type.

Here's the list of supported security type list, when you are connecting to an AP, be sure you choose the right security type.

* WLAN.SECURITY_OPEN

Password will be ignored in WLAN.SECURITY_OPEN

``` python
>>> auth = (WLAN.SECURITY_OPEN, "PASSWORD-WILL-BE-IGNONRE")
```

* WLAN.SECURITY_WEP_PSK
* WLAN.SECURITY_WEP_SHARED
* WLAN.SECURITY_WPA_TKIP_PSK
* WLAN.SECURITY_WPA_AES_PSK
* WLAN.SECURITY_WPA2_TKIP_PSK
* WLAN.SECURITY_WPA2_AES_PSK
* WLAN.SECURITY_WPA_MIXED_PSK
* WLAN.SECURITY_WPA_WPA2_MIXED
* WLAN.SECURITY_WPS_OPEN
* WLAN.SECURITY_WPS_SECUR

**AP mode example**

Here's the AP mode example. It's quite simple, doesn't it?

``` python
>>> from wireless import WLAN
>>> wifi = WLAN(mode=WLAN.AP)
>>> my_ssid = "MY-AP-SSID"
>>> my_auth = (WLAN.WPA2_AES_PSK, "MY-AP-PASSWORD")
>>> wifi.start_ap(ssid=my_ssid, auth=my_auth)
```

**Station/AP hybrid mode example**

If you need hybrid mode (STA_AP mode), not problem.

``` python
>>> from wireless import WLAN
>>> sta, ap = WLAN(mode=WLAN.STA_AP)
# It will return a tuple containing sta and ap when mode=WLAN.STA_AP
>>> ap_ssid = "TARGET-AP-SSID"
>>> ap_auth = (WLAN.WPA2_AES_PSK, "TARGET-AP-PASSWORD")
>>> sta.connect(ssid=target_ssid, auth=target_auth, dhcp=True)

Like you can get the mac address of your NIC.

``` python
>>> from wireless import WLAN
>>> wifi = WLAN(mode=WLAN.STA)
>>> wifi.mac()
'28:c2:dd:dd:42:7d'
```
You can Scan networks nearby. WLAN.scan() will return a list of dictionaries.

``` python
>>> from wireless import WLAN
>>> wifi = WLAN(mode=WLAN.STA)
>>> for i in range(10):
...     ap_list = wifi.scan()
...     if len(ap_list) != 0:
...         for ap in ap_list:
...             print("ssid = %s, bssid = %s, rssi = %d, channel = %d" % (ap.ssid, ap.bssid, ap.rssi, ap.channel))
```

Get the RSSI  only when you are connected to the AP.

``` python
>>>  wifi.rssi()
-51
```

### Dynamic IP (DHCP client) or static IP? ###

In station mode, after AP authentication, MicroPython@Ameba will help you to fetch the IP from DHCP server by assigning the `dhcp=True` argument.

``` python
>>> from wireless import WLAN
>>> wifi = WLAN(mode=WLAN.STA)
>>> my_ssid = "MY-AP-SSID"
>>> my_auth = (WLAN.WPA2_AES_PSK, "MY-AP-PASSWORD")
... wifi.connect(ssid=my_ssid, auth=my_auth, dhcp=True) # assign argument dhcp=True
```

Alternatively, you can do this on your own.

``` python
>>> from wireless import WLAN
>>> wifi = WLAN(mode=WLAN.STA)
>>> my_ssid = "MY-AP-SSID"
>>> my_auth = (WLAN.WPA2_AES_PSK, "MY-AP-PASSWORD")
>>> wifi.connect(ssid=my_ssid, auth=my_auth)
>>> wifi_netif = wifi.getnetif()
>>> wifi_netif.dhcp_request(100)
>>> print(wifi_netif)
```

Or you might want to use static IP, the default ip is `192.168.3.2/24` and the gateway is `192.168.3.1`.

If you are not sure what your IP is, just print the netif object.

For more informations, please check this [url](http://cwyark.github.io/mpiot/rtl8195a/modules/wireless_wlan.html).
