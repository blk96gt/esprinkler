# esprinkler Irrigation Controller
Based on esphome sprinkler component - https://esphome.io/components/sprinkler/
## Hardware
- Waveshare esp32-s3 8 Channel WiFi Relay Module - https://www.waveshare.com/esp32-s3-eth-8di-8ro-c.htm
- Existing 24VAC valves
- 24VAC Power Supply (used the existing supply from old controller)

## Overview
### `hardware/relay_switches.yaml`
Set up the switches for the relays which will activate the valves.  These should not be exposed to the front end.
```Yaml
switch:
  - platform: gpio
    id: lawn_valve_sw0
    pin: GPIO17
  - platform: gpio
    id: lawn_valve_sw1
    pin: GPIO18
  ...
```

### `controller/controller.yaml`
More controller options available here: https://esphome.io/components/sprinkler/#configuration-variables
```Yaml
sprinkler:
  - id: lawn_sprinkler_ctrlr
    main_switch: "Lawn Sprinklers"
    auto_advance_switch: "Lawn Sprinklers Auto Advance"
    multiplier_number: "Lawn Sprinkler Multiplier"
    repeat_number: "Repeat Schedule"
    # VERIFY THIS IS SUFFICENT
    valve_open_delay: 5s
    # standby_switch: 
    valves:
      - valve_switch: "Zone 1"
        enable_switch: "Enable Zone 1"
        run_duration_number: 
          id: z1_run_duration_number
          name: "Zone 1 Run Duration"
          initial_value: 30
        valve_switch_id: lawn_valve_sw0
  ...
```
Add more docs
