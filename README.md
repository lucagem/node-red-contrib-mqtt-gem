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
  - Protocol version (3, 4, 5)

## Installation

Install via Node-RED Palette Manager or run:
```bash
npm install node-red-contrib-mqtt-gem
```

## Original files
https://github.com/node-red/node-red/blob/master/packages/node_modules/%40node-red/nodes/core/network/