---
title: "How to control WiFi in you micropython@Ameba"
description: ""
category: tutorial
project: micropython_ameba
tags: [python, rtl8195a, micropython, ameba]
---

You can control your micropython@Ameba's WiFi in few lines.

<!--more-->

Station mode and AP mode are available in RTL8195A, but AP mode has not implement yet. (Maybe couple weeks later)

Here's an example for station mode. Note that when connection is failed, it will raise an OSError exception.

``` python
>>> from wireless import WLAN
>>> wifi = WLAN(mode=WLAN.STA)
>>> my_ssid = "MY-AP-SSID"
>>> my_auth = (WLAN.WPA2_AES_PSK, "MY-AP-PASSWORD")
>>> try:
...     wifi.connect(my_ssid, my_auth)
... except OSError as e:
...     print("wifi connection failed")
...     print(e)
```

The reason why authenication fail may be the wrong ssid, wrong password or the wrong authenication type.

Here's the list of supported security type list, when you are connecting to an AP, be sure you choose the right type.

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

Also, there's some object method you can use.

Like you can get the mac address.

``` python
>>> from wireless import WLAN
>>> wifi = WLAN(mode=WLAN.STA)
>>> wifi.mac()
'28:c2:dd:dd:42:7d'
```

You can scan networks nearby. WLAN.scan() will return a list of dictionaries.

``` python
>>> from wireless import WLAN
>>> wifi = WLAN(mode=WLAN.STA)
>>> for i in range(10):
...     ap_list = wifi.scan()
...     for ap in ap_list:
...           print("ssid = %s, bssid = %s, rssi = %d, channel = %d" % (ap.ssid, ap.bssid, ap.rssi, ap.channel))
```

Get the RSSI value only when you are connected to the AP.

``` python
>>>  wifi.rssi()
-51
```

### DHCP or static IP? ###

After AP authentication, microptyhon@Ameba will not help you to query the IP via DHCP.

_You need to do it self, use `network` module_

``` python
>>> import network 
>>> local_ip = network.ip()
>>> try:
...     local_ip.dhcp_request(100)
... except OSError as e:
...     print("DHCP failed")
```

Or you might want to use static IP, the default ip is `192.168.3.2/24` and the gateway is `192.168.3.1`.

If you are not sure what your IP is, just print the ip object.

``` python
>>> import network 
>>> local_ip = network.ip()
>>> print(local_ip)
```

For more informations, you could check this [url](http://cwyark.github.io/mpiot/rtl8195a/modules/wireless_wlan.html).
