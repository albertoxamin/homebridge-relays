# Homebridge Relays Stateless

> TLDR: In my house I have relays that send a pulse to invert the current state of the light. And since homekit only has switches, this automatically reports the switch as off after 2 seconds, so the next time it is pressed it will invert the state. (this only happens if you set duration_ms)

Controls 4 channel relays with a Raspberry Pi using HomeKit.

## Hardware

The hardware is quite simple to construct.

1. A Raspberry Pi 
2. Relay module pins are connected to 4 GPIO pins (GPIO-17, 27, 22, 05).

The raspberry pi can then control the state of the relays

## Installation

1. Install homebridge using: `sudo npm install --unsafe-perm -g homebridge`
2. Install this plugin using: `sudo npm install -g --unsafe-perm homebridge-relays-stateless`
3. Update your configuration file. See `config-sample.json` in this repository for a sample.

## Sample Configuration

    {
      "bridge": {
        "name": "RelayServer",
        "username": "CC:22:3D:E3:CE:FA",
        "port": 51826,
        "pin": "031-45-155"
      },

      "description": "4 Channel Relay",

      "accessories": [
        {
          "accessory": "Relay-Stateless",
          "name": "Relay-1",
          "pin": 11
          "invert": true,
          "default_state": false,
          "duration_ms": 1000
        },
        {
          "accessory": "Relay-Stateless",
          "name": "Relay-2",
          "pin": 13
          "invert": false,
          "default_state": false,
          "duration_ms": 3600000
        },
        {
          "accessory": "Relay-Stateless",
          "name": "Relay-3",
          "pin": 15
        },
        {
          "accessory": "Relay-Stateless",
          "name": "Relay-4",
          "pin": 29
        }
      ],

      "platforms": []
    }

## Accessory Configuration Options

| Name            | Meaning                                                                                                                                                         |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `accessory` | Accessory type. `Relay` (REQUIRED)                                                                                                                              |
| `name` | Default name for the accessory.(REQUIRED)                                                                                                                       |
| `pin` | Which pin number to use for this accessory.(REQUIRED)                                                                                                           |
| `invert` | If true, output on pin is `LOW` for `ON` , and `HIGH` for `OFF` .(Default: false)                                                                                 |
| `default_state` | State to set on start of homebridge. `true` for `ON` , `false` for `OFF` .(Default: `false` / `OFF` )                                                              |
| `duration_ms` | If given, accessory will stay ON for this many milliseconds, then turn OFF. Timer resets if accessory is turned ON again while it is still ON.(Default: 0/None) |
