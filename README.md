# node-red-contrib-mqtt-gem

MQTT nodes for Node-RED with environment variables support for dynamic enable and parameters.

## Features

This is an enhanced version of the standard Node-RED MQTT nodes that allows:

- **Dynamic broker configuration** using environment variables
- **Enable/Disable MQTT connection** via the `autoConnect` parameter
- **Environment variables support** for:
  - Port number
  - Auto-connect (true/false)
  - TLS usage (true/false)
  - Protocol version (3, 4, 5): "3"=MQTT V3.1 (legacy); "4"=MQTT V3.1.1; "5"=MQTT V5
    (This section adds the voice "Custom..." to the list of selectable  Protocols. If choosed a text-box appear and allow to write an environment variable. The selection is saved in 2 values "custom" and the environment variable. When the flow starts eventually if the "node-config-input-protocolVersion-custom" contains a right value it override the selection withou change the values saved)

## Installation

Install via Node-RED Palette Manager or run:
```bash
npm install node-red-contrib-mqtt-gem
```

## Original files
https://github.com/node-red/node-red/blob/master/packages/node_modules/%40node-red/nodes/core/network/