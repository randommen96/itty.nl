---
author: David der Nederlanden
category:
  - homelab
  - hypervisors
  - networking
date: "2024-06-03T20:37:01+00:00"
guid: https://itty.nl/?p=179
tag:
  - it
  - networking
  - proxmox
  - pve
title: My homelab infrastructure
url: /my-homelab-infrastructure/

---
Something very easily overlooked is what my homelab looks like, as it mostly just works!

It is a well thought out combination of fit for purpose hardware, without becoming "work", so while I do have a preference for specific hardware, I still have the freedom to build it differently than I would do at my day job. It consists of the following parts:

- [Netgate](https://www.netgate.com/) SG-4860-1U as a pfSense firewall and router;
- Juniper Networks EX2200-C-12P for switching, running as a VC (virtual chassis);
- Unifi NanoHD as WiFi Accesspoins;
- A small server running Proxmox, built within a Fractal design node 304 case:
  - Intel i7-8700k cpu;
  - 64GB DDR4 Crucial memory;
  - Asus Prime H310I-Plus motherboard;
  - Google Coral m.2 TPU;
  - Sonoff Zigbee dongle P as a Zigbee router for Home Assistant.
- [Flexoptix](https://www.flexoptix.net/) optics for terminating my fiber internet.

While I like to automate at scale, I tend to like to get hands on at times in which my homelab gives great opportunities to test and try out new things, but also run mission-critical services to support my personal needs.

I monitor my homelab with [Zabbix](https://www.zabbix.com/) and [UptimeRobot](https://uptimerobot.com/), both notify me via Telegram when something goes south.

In Zabbix I created a detailed map which draws out critical network connections and displays their status:

![](/wp-content/uploads/2024/06/image-1024x612.png)

Feel free to reach out to me when you feel the need!
