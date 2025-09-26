# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0-beta.4] - 2025-09-26

### Added
- Initial beta release
- MQTT broker configuration with environment variables support
- Dynamic enable/disable for MQTT connections via `Auto Connect` field
- Environment variable support for:
  - Port configuration (accepts any variable name)
  - Auto-connect control (checkbox replaced with text input)
  - TLS configuration (checkbox replaced with text input) 
  - Protocol version selection (combo with custom text input)
- Visual status indicators for disabled nodes
- Disabled nodes show "disabled" in gray and block message processing
- Support for MQTT v3.1, v3.1.1, and v5.0 protocols
- Complete compatibility with Node-RED's environment variable resolution (`${variable_name}`)
- No conflicts with core MQTT nodes

### Enhanced
- Extended core Node-RED MQTT nodes with advanced dynamic configuration
- Improved broker management for multi-environment deployments
- Better visual feedback for node status

### Technical
- Based on Node-RED core MQTT implementation
- Full backward compatibility with standard MQTT node configurations
- Optimized for development, staging, and production environments
- Docker and Docker Compose ready

## [Unreleased]

### Planned
- Additional configuration options
- Enhanced error handling
- Performance optimizations