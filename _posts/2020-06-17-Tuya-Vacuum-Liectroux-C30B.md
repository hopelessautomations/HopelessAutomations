---
layout: post
title: "Liectroux C30B"
subtitle: "Tuya WiFi Vacuum Cleaner"
tags: [Smarthome, Tuya, Liectroux, noesp8266]
share-img: /assets/img/Liectroux_C30B.jpg
thumbnail-img: /assets/img/Liectroux_C30B.jpg
---

<div class="alert alert-info">
  <strong>Info!</strong> The post is not complete yet.
</div>

The Vacuum Cleaner:
![C30B](/assets/img/Liectroux_C30B.jpg)

WiFi module:
![C30B](/assets/img/Liectroux_C30B1.jpg)
![C30B](/assets/img/Liectroux_C30B2.jpg)

PCB:
![C30B](/assets/img/Liectroux_C30B3.jpg)
![C30B](/assets/img/Liectroux_C30B4.jpg)
![C30B](/assets/img/Liectroux_C30B5.jpg)
![C30B](/assets/img/Liectroux_C30B6.jpg)
![C30B](/assets/img/Liectroux_C30B7.jpg)
![C30B](/assets/img/Liectroux_C30B8.jpg)
![C30B](/assets/img/Liectroux_C30B9.jpg)
![C30B](/assets/img/Liectroux_C30B10.jpg)

Unfortunately the WR3 is RTL8710BN and not a ESP8266 therefor flashing Tasmota is not going to be possible.
I have connected my FTDI device to it and used the Tuya APP and I could clearly see Tuya protocol on my console which leads me to believe we might be able to swamp the wifi module with a ESP8266 already flashed with Tasmota and try to operate the vacuum from there.
I have ordered a cable with the same ports as the stock one so I can make a adapter for ESP8266 and can swamp between one and the other awhile necessary so more testing to be done when that arrives.