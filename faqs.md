---
layout: faq
title: FAQs
subtitle: All you ever wanted to know about HACC.
---

## What devices are compatible with HACC?

The following table lists *known working devices* that can run HACC.

| Manufacturer | Model  | OS             | Notes | Links                                                                                                 |
|--------------|--------|----------------|-------|-------------------------------------------------------------------------------------------------------|
| Victbing     | V0010W | Android GO 8.1 |       | <i class="fab fa-amazon"></i> [Amazon](https://www.amazon.com/dp/B07S68Q35H/){:target="_blank"}       |

<p></p>
<div class="alert alert-info" role="alert">
    <p><b>Are you successfully using HACC on a device not listed here?</b></p>
    <p><a class="alert-link" href="https://github.com/qJake/hacc.dev/issues/new?assignees=qJake&labels=device+compatibility&template=device-compatibility-report.md&title=New+HACC+Compatible+Device" target="_blank">Please let us know!</a> We will add your device to this list!</p>
    <p><em>(Or, if you know what you're doing, send us a <a class="alert-link" href="https://github.com/qJake/hacc.dev/compare" target="_blank">pull request</a> with your device added to this page.)</em></p>
</div>

## How do I prevent my Android tablet from going to sleep?

You can prevent your Android-based tablet from going to sleep *as well as* protect the screen from wear and tear by using a ***kiosk browser***.

I recommend [Fully Kiosk Browser](https://www.ozerov.de/fully-kiosk-browser/){:target="_blank"}, however there are many alternatives.

I like Fully Kiosk because it:

* Can turn off the screen after a period of time
* Can turn off the screen if the lights in the room go off
* Can turn on the screen if motion is detected by the camera
* Locks the tablet from use (no homescreen / settings / power access)
    * Can be unlocked with a PIN and you can then access the main Android homescreen
* Can publish device sensor data via MQTT - great for Home Assistant!

Some of these features are restricted to "Plus", but it's only &euro;6.90 / $7.50 one-time to unlock.

## How do I prevent my iPad from going to sleep?

Refer to [this excellent article by HowToGeek](https://www.howtogeek.com/252670/how-to-put-an-ipad-into-kiosk-mode-restricting-it-to-a-single-app/){:target="_blank"} for the
various options available to iOS users for restricting an iOS-based device to a single app.

Current options include:

* Guided Access
* Apple Configurator (requires a Mac device)

You may need to [add a website icon to your home screen](https://support.apple.com/guide/iphone/bookmark-favorite-webpages-iph42ab2f3a7/ios#iph4f9a47bbc){:target="_blank"} first.