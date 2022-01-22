# From Dumb to Smart Washing Machine - Home Assistant

![dumb-washing-machine](wm.png)

Use a power plug with an energy consumption monitor and Home Assistant to transform your dumb washing machine into a "smart" one with a bunch of informative features. Basically, we will use the measurements of power drawn by the washing machine connected in a smart plug (WIFI) with power monitoring. Depending on power drawn we can determine with some accuracy the status of the washing machine and automate some stuff.

![eu-br-power-plug](powerplug.jpg)

## Before start

What do I need?

- A Washing Machine (Serious dude!?)
- :electric_plug: A Smart Power Plug (WIFI) Tuya/SmartLife Compatible (photo above)
  - https://a.aliexpress.com/_mLoZBgY (EU Socket Compatible) :european_union: - The one I used!
  - https://pt.aliexpress.com/item/1005003106242894.html (Brazilian Socket)) :brazil:
- [Home Assistant](https://www.home-assistant.io/) using [HACS](https://hacs.xyz/) and install:
  - [Local Tuya Integration](https://github.com/rospogrigio/localtuya) - yes! The offical Tuya integration still don't have the power monitoring attributes support.
  - [Card-mod](https://github.com/thomasloven/lovelace-card-mod) - to create our fancy button on lovelace dashboard
  - [Custom Button Card](https://github.com/custom-cards/button-card) - to create our fancy button on lovelace dashboard

First of all, I will consider that you already added your smart plug as a switch under the Local Tuya Integration. If you don't know how to do it, I recommend this [video](https://www.youtube.com/watch?v=vq2L9c5hDfQ). On my setup the entity id is **switch.lt_lava_roupa** - see the entity properties on developer tools (image below)

![lava_roupa_entity](entity.jpg)


