# node-red-contrib-mqtt-gem

[![npm version](https://badge.fury.io/js/node-red-contrib-mqtt-gem.svg)](https://www.npmjs.com/package/node-red-contrib-mqtt-gem)
[![Node-RED](https://img.shields.io/badge/Node--RED-%23AA2837?style=flat&logo=nodered)](https://nodered.org)

> Add little features to Standard MQTT nodes for Node-RED using environment variables support and dynamic configuration capabilities.

**Library extension developed by [GEM srl](https://www.gemsrl.it) - Sant'Agata sul Santerno (RA), Italy** derived from [Original Node-red core library](https://github.com/node-red/node-red/blob/master/packages/node_modules/%40node-red/nodes/locales/en-US/network/)

![Params](./docs/node-red-contrib-mqtt-gem%20params.png)

## 🚀 Features

**node-red-contrib-mqtt-gem** extends the standard Node-RED MQTT nodes with powerful dynamic configuration capabilities:

### ✅ **Dynamic Broker Control**
- **Enable/Disable connections** dynamically via environment variable (use "Auto connect" to enable/disable)
- Automatic connection management based on runtime configuration
- Visual status indicators (disabled nodes show "disabled" in gray)

### 🌍 **Environment Variables Support**
- **Port Configuration**: Use any environment variable for port numbers
- **Auto-Connect Control**: Dynamic connection behavior via custom variable names
- **TLS Configuration**: Runtime TLS enablement via any environment variable
- **Protocol Version**: Support for custom MQTT protocol versions (3.1, 3.1.1, 5.0)
- **Complete Broker Settings**: All broker parameters can be configured via **any** environment variable names

### 🔧 **Enhanced Protocol Support**
- **MQTT v3.1** (legacy)
- **MQTT v3.1.1** (standard)
- **MQTT v5.0** (latest)
- **Custom Protocol Selection**: Text input for environment variable-based protocol selection

### 🎯 **Smart Node Behavior**
- Disabled brokers prevent IN/OUT nodes from processing messages
- Visual feedback with status indicators
- Seamless integration with existing Node-RED flows
- No conflicts with core MQTT nodes

## 📦 Installation

### Via Node-RED Palette Manager (Recommended)
1. Open Node-RED editor
2. Go to **Menu → Manage palette**
3. Select **Install** tab
4. Search for `node-red-contrib-mqtt-gem`
5. Click **Install**

### Via npm
```bash
npm install node-red-contrib-mqtt-gem
```

### Manual Installation
```bash
cd ~/.node-red
npm install node-red-contrib-mqtt-gem
```

## 🔧 Configuration

### Environment Variables Setup

![launch.json](./docs/node-red-contrib-mqtt-gem%20launch.png)

**You can use ANY variable names you prefer.** The examples below use common naming conventions:

```bash
# Example with standard names
export MQTT_HOST="broker.example.com"
export MQTT_PORT="1883"
export MQTT_AUTOCONNECT="true"
export MQTT_USETLS="false"
export MQTT_PROTOCOL="5"

# Example with custom names
export MY_BROKER_ADDRESS="broker.example.com"
export MY_BROKER_PORT="1883"
export ENABLE_MQTT="true"
export USE_SSL="false"
export MQTT_VERSION="5"

# Example with company-specific names
export COMPANY_MQTT_SERVER="internal.company.com"
export PRODUCTION_MQTT_PORT="8883"
export MQTT_CONNECTION_ENABLED="true"

# Start Node-RED
node-red
```

### Docker Configuration

```dockerfile
# Dockerfile
FROM nodered/node-red:latest

# Install the plugin
RUN npm install node-red-contrib-mqtt-gem

# Set environment variables (use any names you prefer)
ENV MY_MQTT_HOST=broker.example.com
ENV MY_MQTT_PORT=1883
ENV MQTT_ENABLED=true
ENV USE_TLS=false
ENV PROTOCOL_VERSION=5
```

### Docker Compose

```yaml
version: '3.8'
services:
  node-red:
    image: nodered/node-red:latest
    ports:
      - "1880:1880"
    environment:
      - MY_MQTT_HOST=broker.example.com
      - MY_MQTT_PORT=1883
      - MQTT_ENABLED=true
      - USE_TLS=false
      - PROTOCOL_VERSION=5
    volumes:
      - node-red-data:/data
    command: >
      bash -c "npm install node-red-contrib-mqtt-gem && 
               npm start -- --userDir /data"

volumes:
  node-red-data:
```

## 🎮 Usage Examples

### Basic Broker Configuration

**Static Configuration:**
```
Server: broker.example.com
Port: 1883
Auto Connect: true
Use TLS: false
Protocol: MQTT V3.1.1
```

**Dynamic Configuration with Environment Variables (use any variable names):**
```
Server: ${MY_BROKER_HOST}
Port: ${MY_BROKER_PORT}
Auto Connect: ${MQTT_ENABLED}
Use TLS: ${USE_SSL_CONNECTION}
Protocol: Custom → ${MQTT_VERSION}
```

### Conditional MQTT Publishing

```javascript
// In a Function node before mqtt-gem out
if (env.get("MY_MQTT_ENABLED") === "true") {
    return msg; // Send message
} else {
    return null; // Block message
}
```

### Multi-Environment Setup

```bash
# Development Environment
export DEV_MQTT_HOST="dev-broker.internal"
export DEV_MQTT_PORT="1883"
export DEV_MQTT_ENABLED="true"

# Production Environment
export PROD_MQTT_HOST="prod-broker.company.com"
export PROD_MQTT_PORT="8883"
export PROD_MQTT_ENABLED="true"
export PROD_USE_TLS="true"

# Staging Environment
export STAGING_BROKER="staging.company.com"
export STAGING_PORT="1883"
export STAGING_CONNECTION="false"  # Disabled in staging
```

### Protocol Version Examples

```bash
# MQTT v3.1 (legacy)
export MY_PROTOCOL="3"

# MQTT v3.1.1 (standard)  
export BROKER_PROTOCOL="4"

# MQTT v5.0 (latest)
export MQTT_VERSION="5"
```

## 📋 Node Types

### `mqtt-gem-broker` (Configuration Node)
Enhanced broker configuration with environment variable support for all parameters.

### `mqtt-gem in` (Input Node)
MQTT subscriber with dynamic broker configuration. Shows "disabled" status when broker is disabled.

### `mqtt-gem out` (Output Node)  
MQTT publisher with dynamic broker configuration. Blocks messages when broker is disabled.

## 🔍 Environment Variables Reference

**Important**: You can use **any variable names** you prefer. The table below shows common examples, but you have complete freedom in naming:

| Example Variable | Description | Default | Example Values |
|------------------|-------------|---------|----------------|
| `MY_MQTT_HOST` | Broker hostname/IP | localhost | `broker.example.com` |
| `BROKER_PORT` | Broker port | 1883 | `1883`, `8883` |
| `MQTT_ENABLED` | Auto-connect on startup (enable/disable connection and nodes)| true | `true`, `false` |
| `USE_SSL` | Enable TLS/SSL | false | `true`, `false` |
| `PROTOCOL_VERSION` | MQTT protocol version | 4 | `3`, `4`, `5` |

**Configuration Examples:**
```bash
# Company-specific naming
export COMPANY_MQTT_BROKER="internal.company.com"
export COMPANY_MQTT_PORT="1883"

# Project-specific naming  
export PROJECT_A_BROKER="project-a.broker.com"
export PROJECT_A_ENABLED="true"

# Environment-specific naming
export PROD_MQTT_HOST="prod-broker.com"
export DEV_MQTT_HOST="dev-broker.com"
```

## 🧪 Testing

### Test Flow Example

1. **Create test brokers:**
   - Active broker with `MY_MQTT_ENABLED=true`
   - Disabled broker with `MQTT_CONNECTION=false`

2. **Add MQTT nodes:**
   - Input nodes for both brokers
   - Output nodes for both brokers

3. **Verify behavior:**
   - Active broker: nodes work normally
   - Disabled broker: nodes show "disabled" status and don't process messages

### Environment Variables Test

```bash
# Set test variables (use any names you prefer)
export TEST_MQTT_HOST="test.mosquitto.org"
export TEST_MQTT_PORT="1883" 
export TEST_CONNECTION_ENABLED="true"
export TEST_PROTOCOL_VERSION="5"

# Start Node-RED and verify configuration
node-red
```

## 🔧 Development

### Local Development Setup

```bash
# Clone repository
git clone https://github.com/lucagem/node-red-contrib-mqtt-gem.git
cd node-red-contrib-mqtt-gem

# Install dependencies
npm install

# Setup development environment
npm run dev-setup

# Start development Node-RED instance
npm run dev
```

### Development Commands

```bash
# Start development server
npm run dev

# Debug mode
npm run dev-debug

# Run tests (when available)
npm test
```

## 📝 Migration from Standard MQTT Nodes

1. **Replace node types** in your flows:
   - `mqtt in` → `mqtt-gem in`
   - `mqtt out` → `mqtt-gem out`  
   - `mqtt-broker` → `mqtt-gem-broker`

2. **Update broker configurations** to use environment variables:
   - Replace static values with `${VARIABLE_NAME}`
   - Set corresponding environment variables

3. **Deploy and test** the updated flow

## ❓ Troubleshooting

### Common Issues

**Q: Nodes show "disabled" status**  
A: Check that your auto-connect variable (e.g., `MY_MQTT_ENABLED`) is set to `"true"` (as string)

**Q: Environment variables not resolving**  
A: Ensure variables are set before starting Node-RED and use correct syntax: `${YOUR_VARIABLE_NAME}`

**Q: Protocol version not working**  
A: For custom protocols, select "Custom..." in dropdown and enter `${YOUR_PROTOCOL_VAR}` in text field

**Q: TLS connection failing**  
A: Verify your TLS variable (e.g., `USE_TLS="true"`) and correct port (usually 8883 for TLS)

### Debug Mode

Enable Node-RED debug logging:
```bash
DEBUG=mqtt-gem* node-red
```

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

## 🔗 Links

- **Repository**: https://github.com/lucagem/node-red-contrib-mqtt-gem
- **Issues**: https://github.com/lucagem/node-red-contrib-mqtt-gem/issues
- **Node-RED**: https://nodered.org
- **MQTT.org**: https://mqtt.org

## 📊 Compatibility

- **Node-RED**: >= 2.0.0
- **Node.js**: >= 14.0.0
- **MQTT**: Versions 3.1, 3.1.1, 5.0

---

**Developed by [GEM srl](https://www.gemsrl.it) - Sant'Agata sul Santerno (RA), Italy**  
**Author**: [Luca Tralli](https://github.com/lucagem)