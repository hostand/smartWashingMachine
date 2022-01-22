# From Dumb to Smart Washing Machine - Home Assistant

![dumb-washing-machine](wm.png)

Use a power plug with an energy consumption monitor and Home Assistant to transform your dumb washing machine into a "smart" one with a bunch of informative features. Basically, we will use the measurements of power drawn by the washing machine connected in a smart plug (WIFI) with power monitoring. Depending on power drawn we can determine with some accuracy the status of the washing machine and automate some stuff.

![eu-br-power-plug](powerplug.jpg)

Before start you will need this:

- A Washing Machine (Serious dude!?)
- :electric_plug: A Smart Power Plug (WIFI) Tuya/SmartLife Compatible (photo above)
  - https://a.aliexpress.com/_mLoZBgY (EU Socket Compatible) :european_union: - The one I used!
  - https://pt.aliexpress.com/item/1005003106242894.html (Brazilian Socket - thanks Dilma!) :brazil:
- [Home Assistant](https://www.home-assistant.io/) using [HACS](https://hacs.xyz/) to install:
  - [Local Tuya Integration](https://github.com/rospogrigio/localtuya) - yes! The offical Tuya integration still don't have the power monitoring entities support.
  - [Card-mod](https://github.com/thomasloven/lovelace-card-mod) - to create our fancy button on lovelace dashboard
  - [Custom Button Card](https://github.com/custom-cards/button-card) - to create our fancy button on lovelace dashboard
