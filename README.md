# busy_box
Simple do-not-disturb indicators


With everyone stuck at home, the wife wanted a passive way for me to let her know I was busy in a conference call. Thus, the busy_box was created.

It's a simple box with a button and two LEDs connected to a ESP8266. The ESP is programmed with Tasmota and configured to be connected to Home Assistant. A couple of Automations in Home Assistant make them work. See the YouTube video below:

#TODO

The Tasmota Module Configuration is set to:
Module Type: Generic (0)
D4 GPIO2: Button1 (17)
D2 GPIO4: Relay1 (21)
D1 GPIO5: Relay2 (22)

Then, obviuosly, setup Tasmota for WiFi and MQTT.

There were a couple of options I turned on:
SetOption19 1 #Turn on Home Assistant auto-discovery
SetOption13 1 #Turn off multi-button press and hold

I then added the following Automations to Home Assistant:

- id: '1585062349930'
  alias: Caitlin Busy
  description: ''
  trigger:
  - entity_id: switch.dnd_caitlin
    from: 'off'
    platform: state
    to: 'on'
  condition: []
  action:
  - device_id: b056a5c648694034b962a23a63d5ed0a
    domain: switch
    entity_id: switch.sonoff2
    type: turn_on
- id: '1585062499850'
  alias: Caitlin Not Busy
  description: ''
  trigger:
  - entity_id: switch.dnd_caitlin
    from: 'on'
    platform: state
    to: 'off'
  condition: []
  action:
  - device_id: b056a5c648694034b962a23a63d5ed0a
    domain: switch
    entity_id: switch.sonoff2
    type: turn_off
- id: '1585062714384'
  alias: Joe Busy
  description: ''
  trigger:
  - entity_id: switch.dnd_joe
    from: 'off'
    platform: state
    to: 'on'
  condition: []
  action:
  - device_id: 855ddbe90cf643f49df91904968ed479
    domain: switch
    entity_id: switch.sonoff2_2
    type: turn_on
- id: '1585062796113'
  alias: Joe Not Busy
  description: ''
  trigger:
  - entity_id: switch.dnd_joe
    from: 'on'
    platform: state
    to: 'off'
  condition: []
  action:
  - device_id: 855ddbe90cf643f49df91904968ed479
    domain: switch
    entity_id: switch.sonoff2_2
    type: turn_off
