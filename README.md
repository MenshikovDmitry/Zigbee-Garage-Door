# Zigbee Garage Door Opener
This is a DIY Zigbee garage door opener, designed for use with Home Assistant and [Zigbee2MQTT](https://www.zigbee2mqtt.io/).
It supports any dry-contact operated garage door or other device. The maximum number of doors / dry contacts it can support is 2.

**!! This repository is currently under development, stay tuned !!**

Disclaimer: This project is provided as is. The author is not responsible for any damage caused by the project. Wiring might be dangerous due to high voltage and must be done by a professional.

![Alt Text](img/lovelace.gif)
![Alt Text](img/controller_1.jpg)

## Power Supply
A single PCB supports three options:
1. **HLK-PM01** for 220v input
2. **Mini560 Pro 5v** for 6-32v input
3. Directly solder the power supply to the **+** and **GND** pads for 3.3v-12v input. In this case, voltage step-down will be done by the built-in linear voltage regulator **AMS1117-3.3V**.
![Alt Text](img/ac_in.png) ![Alt Text](img/dc_in.png) 



## Firmware
The firmware is based on the [PTVO](https://ptvo.info/) project. Please consider supporting the author.
### Flashing
You will need a CC Debugger (Google it) and [SmartRF Flash Programmer](https://www.ti.com/tool/FLASH-PROGRAMMER) **_V1_** to flash the firmware. Refer to the user manual [here](https://ptvo.info/how-to-select-and-flash-cc2530-144/).
## Pairing
Option 1: Reflash the device and it will boot in pairing mode  
Option 2: Press and hold the only button on the device for 10 seconds, until the LED starts blinking every 1 second.

When the device is paired, the LED will blink every 5 seconds.
## Lovelace card
So far there are 2 separate binary sensors and two switches for each door, so I created a simple buttons that indicate the state. Click calls the switch that triggers the relay.  
![Alt Text](img/lovelace.gif)
```yaml
type: horizontal-stack
cards:
  - show_name: true
    show_icon: true
    type: button
    tap_action:
      action: call-service
      service: switch.toggle
      target:
        entity_id: switch.garage_door_l1
      data: {}
    show_state: true
    icon_height: 60px
    name: Garage
    entity: binary_sensor.door_garage_contact
  - show_name: true
    show_icon: true
    type: button
    tap_action:
      action: call-service
      service: switch.toggle
      target:
        entity_id: switch.garage_door_l2
    entity: binary_sensor.door_gate_contact
    show_state: true
    icon_height: 60px
    name: Gate

```
## Wiring
**Attention:** This project involves high voltage wiring. It must be done by a professional.  

![Alt Text](img/wiring.drawio.png)

## Contributing
Contributions are welcome.
- [ ] Custom firmware, z2m converter.
- [ ] Lovelace card
- [ ] PCB design
## Support / Buy
- Consider buying coffee to the authors of [PTVO](https://ptvo.info/) or [Zigbee2MQTT](https://www.zigbee2mqtt.io/).
- Buy this device at Tindie (coming soon) 