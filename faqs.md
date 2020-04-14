---
layout: page
title: FAQs
subtitle: All you ever wanted to know about HACC.
---

{% include toc.html html=content class=toc h_min=2 h_max=2 ordered=true %}

## What devices are compatible with HACC?

The following table lists *known working devices* that can run HACC.


| Manufacturer | Model  | OS             | Notes | Links                                                 |
|--------------|--------|----------------|-------|-------------------------------------------------------|
| Victbing     | V0010W | Android GO 8.1 |       | [Amazon](https://www.amazon.com/dp/B07S68Q35H/)       |

## How do I prevent my tablet from going to sleep?

You can prevent your Android-based tablet from going to sleep *as well as* protect the screen from wear and tear by using a ***kiosk browser***.

I recommend [Fully Kiosk Browser](https://www.ozerov.de/fully-kiosk-browser/), however there are many alternatives.

I like Fully Kiosk because it:

* Can turn off the screen after a period of time
* Can turn off the screen if the lights in the room go off
* Can turn on the screen if motion is detected by the camera
* Locks the tablet from use (no homescreen / settings / power access)
    * Can be unlocked with a PIN and you can then access the main Android homescreen
* Can publish device sensor data via MQTT - great for Home Assistant!

Some of these features are restricted to "Plus", but it's only &euro;6.90 / $7.50 one-time to unlock.