---
author: zoxvijawofijasodfij
category:
  - automation
  - domotics
date: "2022-02-11T20:44:20+00:00"
guid: http://itty.nl/?p=1
tag:
  - automation
  - domotics
  - home-automation
title: Automating your central heating
url: /automating-your-central-heating/

---
For some time I was looking for a solution to make my boiler "smart" without modifying the thermostat to support [OpenTherm](https://nl.wikipedia.org/wiki/OpenTherm).

While browsing the interwebz on a lazy Sunday I stumbled upon the [EMS-ESP32](https://github.com/emsesp/EMS-ESP32) project, which fit my needs perfectly, as it hooks into the [EMS bus](https://bbqkees-electronics.nl/how-does-it-work/) and talks with the thermostat in the propietary [Nefit](https://www.nefit-bosch.nl/) signal, without modifying anything.
