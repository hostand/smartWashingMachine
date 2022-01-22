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

## Initial Steps

First of all, I will consider that you _already_ added your smart plug as a switch under the Local Tuya Integration. If you don't know how to do it, I recommend this [video](https://www.youtube.com/watch?v=vq2L9c5hDfQ). As I said, the official Tuya integration doesn't provide the information we need (until the day I'm writing it) and Local Tuya is awesome since it don't rely on Tuya Cloud. So, on my setup the entity id is **switch.lt_lava_roupa** - see the power monitoring entity attributes on developer tools (image below)

![lava_roupa_entity](entity.JPG)

- current
- current consumption
- voltage

Create the entities from the attributes adding this code to you **configuration.yaml** (or wherever you put it on your home assistant files)

```yaml
 - platform: template
   sensors:
      washingmachine_powerdraw:
        value_template: '{{ state_attr("switch.lt_lava_roupa", "current_consumption") }}'
        unit_of_measurement: 'W'
      washingmachine_current:
        value_template: '{{ state_attr("switch.lt_lava_roupa", "current") }}'
        unit_of_measurement: 'mA'
      washingmachine_voltage:
        value_template: '{{ state_attr("switch.lt_lava_roupa", "voltage") }}'
        unit_of_measurement: 'V'
```


## Staring your washing machine and Tuya/SmartLife app

Yes, now it's time to study your washing machine behaviour. (By the way, you can use this approach in order to transform other dumb devices into smart just analyzing the power consumption). Open you SmartLife/Tuya app (I use SmartLife) - select your smart plug and under **Electric** option you will see this: 

![electric](electric.jpg)

The important measurement is the **_Power_** in W (current consumption)! Now you will set some washing program on your machine, stare it and make notes about the consumption/action behaviour. In my case during the Washing the power value is above 2000 but during Rinse its just 300. Make note about every change to make the more accurate automations. 

## Washing Machine state and automations

Now we need to create an input_select entity to keep the washing machine state. You can add as many states you want in the options depending on your machine and how accurate were the power variations that define your machine's actions. So, go to your **configuration.yaml** and add the code below.

```yaml
input_select:
  state_washingmachine:
    name: Washing Machine state
    options:
      - Switched Off 
      - Powered Down
      - Idle
      - Rinse / Spin
      - Wash
    icon: mdi:washing-machine
```


