---
layout: tocpage
title: Using HACC
subtitle: The defninitive user guide.
---

## Welcome!

Welcome to *Home Assistant Command Center*! You're just a few steps away from supercharging your home with an awesome wall tablet experience.

If you have not installed HACC yet (either via *Docker* or as a *Supervisor Add-on*), please refer to the **[Installation Guide](/install)** first!

## Initial Setup

After installing and starting up your HACC instance for the first time, you'll be presented with the system setup page.

You'll need to fill out your **Home Assistant Base URL** and generate yourself a **Long-Lived Access Token**.

![system-setup](/img/setup.png)

**Base URL**: (*For Non-Supervisor/Addon Installations Only*) This is your Home Assistant URL. It can be a publicly accessible URL, or a private URL as long as HACC (your tablet device) can reach it over the local network at that IP address or DNS name.

**Long-Lived Access Token**: Generate this via the following instructions:
1. Navigate to Home Assistant > Your User Account (very bottom link in the sidebar, your username)
1. Scroll to the very bottom and find the *Long-Lived Access Tokens* section  
   ![access tokens](/img/llat.png)
1. Click **Create Token**
1. Give it a descriptive name, like **HA Command Center**. (The name can be whatever you'd like.)
1. Copy and paste the token value into HACC.

**(*Optional*) Override Asset Base URL**: If you use a private or non-standard network setup, in some cases, HACC may not be able to load images or other
public assets from your Home Assistant instance. Set this value to a base URL that HACC can reach (such as your public hostname / URL for Home Assistant) if images aren't loading correctly.

After pressing **Save Settings**, you can now proceed to create some pages and tiles!

## Pages

Pages are a way to group related tiles, and are exactly what the name implies &ndash; different web pages that you can navigate between.

When you first load HACC, or you upgrade HACC from a previous version that did not support Pages, HACC automatically generates a "Default" first page for you.

![pages 1](/img/guide-1.png)

### Page Properties

Each page has the following settings:

| Setting                      | Description   |
|------------------------------|---------------|
| **Page ID**                  | The ID of the page. Must be unique. This is used as the navigation URL for the page, for example, if your page ID is "scenes", the URL for the page will be `/d/scenes`. |
| **Page Name**                | A friendly name for the page. Only visible in the admin area. |
| **Set as Default Page**      | Only one page can be set as the default. Whichever page is set as the default, when the dashboard is opened with no page ID (with just the URL `/d/`), then the default page will load. Think of it like a homepage. |
| **Navigation Auto Return**   | If greater than 0, specifies the number of seconds after which this page will automatically navigate back to the default page (homepage). Set to 0 to disable auto return. |

![pages 2](/img/guide-2.png)

### Navigating Between Pages

A new tile type called the *Navigation Tile* has been added.

![nav tile](/img/navtile.png)

This tile has 3 modes of operation:

* **Home:** When pressed, the dashboard will navigate to the defualt / home page.
* **Navigate:** When pressed, the dashboard will navigate to the specified page (see below).
* **Refresh:** Whe pressed, the current page will reload. (If applicable, the *Navigation Auto Return* timer is also reset.)

![pages 3](/img/guide-3.png)

If the *navigation mode* is set to *navigate*, you can specify the page to navigate to using the **Target Page** setting.

![pages 4](/img/guide-4.png)

## Layout

Each page specifies its layout, which is the dimensions of the screen (assuming HACC is running full-screen), as well as tile size and spacing settings.

With the introduction of pages, each page can have totally different layout and tile settings, so you can use one HACC instance for multiple different tablet devices!

![layout](/img/layout.png)

| Setting                      | Description   |
|------------------------------|---------------|
| **Device Width (px)**        | Specify the width of your device's screen, in pixels. This can be smaller than your device if you want to have padding on either side (the HACC dashboard interface is rendered horizontally centered). |
| **Device Height (px)**      | Specify the height of your device's screen, in pixels. If this value is set too high, you might have a vertical scrollbar. |
| **Base Tile Size (px)**      | Specify the size of a 1x1 tile. A good value is 100. Use a number that is divisible by 2. |
| **Tile Spacing (px)**        | Specify the spacing, in pixels, between each tile and around the outer edge of the dashboard. A good number is 6. Use a number that is divisible by 2. |

Getting the correct settings can be tricky, and will likely take some trial and error. You can try using [Device Mode in Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/device-mode){:target="_blank}{:rel="nofollow"} to simulate your tablet's screen size as well.

### Layout Example

Take the following example:

![layout sample](/img/layoutsample.png)

If my device is 536x854 (or can scale to that resolution), I can fit 8 rows and 5 columns of tiles because:

* **5** &times; (100 + 6) + 6 = 536
* **8** &times; (100 + 6) + 6 = 854

(In the example above, replace *100* with your tile size and *6* with your tile spacing.)

Play around with the values until you find something that works for you and your tablet device!

<div class="alert alert-warning" role="alert">
    <p><b>Set your Layout Settings First!</b></p>
    <p>If you change your Layout Settings after you have already positioned some tiles, it is possible your tiles might go past the edge of the screen, and the drag and drop feature that automatically slides tiles around may not function correctly.</p>
</div>

### Tile Layout

Once you have your device width, height, and tile sizes all set correctly, you can use the right-hand side of the screen to drag and drop your tiles where you want them to be on your dashboard.

<div class="alert alert-success" role="alert">
    <p><b>Don't forget to press "Save Layout" when you're finished!</b></p>
</div>

#### Reset Layout

If you have a bunch of new tiles (and they are all stacked on top of each other in the first position), or this is the first time you're laying out this page, you can press the "Reset Layout" button which will cause the tile layout engine to automatically (and somewhat **randomly**) place each tile where it thinks it fits best.

<div class="alert alert-warning" role="alert">
    <p><b>Layout Reset Warning</b></p>
    <p>Pressing the "Reset Layout" button will move ALL of your tiles, even ones that you placed by hand. If you don't want to lose your existing layout, don't use "Reset Layout" (or just don't press "Save Layout" to save your changes).</p>
</div>

## Tiles

Now that you've configured your first page, and you have your layout all set up,  it's time to add some tiles!

On the "Pages" screen, click the "**Manage *n* Tiles**" button to open the tile list for that page.

![tile list](/img/tilelist.png)

Click **"Add Tile"** to add your first tile.

Select the tile type you want to add. The entities which are supported by that tile are listed on each card.

<div class="alert alert-info" role="alert">
    <p><b>Tip</b></p>
    <p>The Date Tile is a good first tile to add! It displays the current date and time.</p>
</div>

### Tile Types

Here is a brief listing of all of the types of tiles we support.

#### Home Assistant Tiles

| Tile Name | Supported Entities | Description |
|---|---|---|
| State    | *All Types* | Displays an entity's current state text. Contains options for overriding on/off text and rounding decimal values. |
| Weather  | `sensor` | Displays a formatted weather tile. Recommended minimum size is 2x2. (*Note: The `weather` entity type is not supported, you must supply separate sensors for each value.*) |
| Switch   | `switch`, `group`, `cover`, `fan`, `remote`, `media_player`, `input_boolean` | Toggles the switch on and off by calling the respective `turn_on` or `turn_off` service. |
| Light    | `light` | Turns lights on and off. (*A future update will allow for brightness and limited color control.*) |
| Person   | `person`, `device_tracker` | Displays the person's entity picture and their current location / state value. |
| Camera   | `camera` | Displays a camera feed. |
| Scene    | `scene` | Activates a scene. |
| Media    | `media_player` | Displays the media image preview, and optionally, overlays the device name and media title. |
| Calendar | `calendar` | Displays upcoming events. Only supports Google Calendar at this time. (*Note: Not supported in Supervisor Add-on mode due to API limitations.*) |

#### Utility Tiles
| Tile Name | Description |
|---|---|
| Navigation | Allows navigation between pages, and refreshing of the current page. |
| Blank      | A spacer tile. Does not render anything, but can push other tiles down (or over) since the layout engine does not allow for arbitrary vertical space between tiles. |
| Label      | A tile that renders plain text. Useful for "title tiles". Use the custom CSS property box to change the font, color, size, or other attributes of the text. |
| Date       | Displays the current date and time. Date and time formatting can be customized / localized, and a timezone can be selected. |