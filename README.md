# Smart irrigation expansion board
Expansion board for garden irrigation, with 7 differents triacs controlling solenoid valvs and one relay for the water pump.
This board should be attached to the [Esp energy monitor](https://github.com/zioCristia/esp-energy-monitor-v2) board.

Should one not need the power monitor, the board could be constructed by eliminating all components related to current measurement, thus leaving only the power supply and esp32.

The board's design allows it to be inserted into the rail of the home's breaker box by printing a 3D component.

The card can be divided into three sub-parts:
* The control of the 24V ac irrigation solenoid valves.
* The control of the water pump (maximum relay 16A).
* The control of the house electric gate from 12V dc.
  
## Table of contents
* [Hardware](#hardware)
* [Software](#software)
* [Pcb](#pcb)
* [Contribution](#contribution)

# Hardware
Each part of the card is independent of the others and can be omitted during construction if there is no need for it.
Similarly, you have the option of controlling 7 irrigation solenoid valves, but you can use a smaller number if you wish.
In this way, the price can vary (in particular reduce) drastically.

A complete list of all the components with a link to aliexpress could be found [here](https://docs.google.com/spreadsheets/d/1A_0oTcwCHzUrwPyKvZikXxDFFEQyVeJslgch1jBqpY8/edit?usp=sharing). The price is very indicative because if you already have components such as resistors or capacitors, it is drastically reduced.

# Software
Esp32 was programmed using EspHome to enable its integration with [Home Assistant](https://www.home-assistant.io). To control solenoid valves, as well as the water pump and gate, simply add the following lines in the EspHome generic code for an esp32.
This will create them as switches in Home Assistant.

For more information, see the example code on the [energy monitor v2](https://github.com/zioCristia/esp-energy-monitor-v2/tree/main#software) or the [EspHome documentation](https://esphome.io).

```
switch:
  - platform: gpio
    name: "Cancello grande interruttore"
    pin: 
      number: GPIO19
      #inverted: true
    id: rele_cancello
    on_turn_on:
    - delay: 500ms
    - switch.turn_off: rele_cancello
    
  - platform: gpio
    pin: GPIO18
    name: "Pompa acqua"
    id: water_pump_switch
    #inverted: true
    restore_mode: ALWAYS_OFF
    
  - platform: gpio
    pin: GPIO15
    name: "irr1"
    id: irr1_switch
    inverted: true
    restore_mode: ALWAYS_OFF
    
  - platform: gpio
    pin: GPIO4
    name: "irr2"
    id: irr2_switch
    inverted: true
    restore_mode: ALWAYS_OFF
    
  - platform: gpio
    pin: GPIO16
    name: "irr3"
    id: irr3_switch
    inverted: true
    restore_mode: ALWAYS_OFF
    
  - platform: gpio
    pin: GPIO17
    name: "irr4"
    id: irr4_switch
    inverted: true
    restore_mode: ALWAYS_OFF
    
  - platform: gpio
    pin: GPIO14
    name: "irr5"
    id: irr5_switch
    inverted: true
    restore_mode: ALWAYS_OFF
    
  - platform: gpio
    pin: GPIO5
    name: "irr7"
    id: irr7_switch
    inverted: true
    restore_mode: ALWAYS_OFF
```

# Pcb
You can find the whole eagle project in [this folder](./irrigation_control_unit).
![alt text](/images/schematics.png)
![alt text](/images/pcb.png)

# Contribution

Feel free to report any bugs or feature requests.
