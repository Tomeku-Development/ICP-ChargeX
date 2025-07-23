# ChargeX Hardware Components

## 🔧 Overview

Physical hardware components for the ChargeX BaaS platform, including IoT devices for battery monitoring, kiosk systems, and sensor integrations.

## 🏗️ Structure

```
hardware/
├── esp32-monitor/       # Battery monitoring node
│   ├── src/            # Arduino/ESP-IDF code
│   ├── libraries/      # Custom libraries
│   ├── schematics/     # Circuit diagrams
│   └── docs/           # Hardware documentation
├── raspberry-pi-kiosk/ # Kiosk & disbursement system
│   ├── src/            # Python/Node.js code
│   ├── config/         # System configurations
│   ├── scripts/        # Setup & maintenance scripts
│   └── ui/             # Kiosk interface
├── bms-integration/    # Battery Management System
│   ├── protocols/      # Communication protocols
│   ├── drivers/        # Hardware drivers
│   └── config/         # BMS configurations
├── sensors/            # Sensor configurations
│   ├── voltage-current/ # INA219/INA226 configs
│   ├── temperature/    # DS18B20/DHT11 configs
│   └── gps/            # NEO-6M/u-blox configs
└── pcb-designs/        # PCB layouts & designs
```

## 🔋 ESP32 Battery Monitor

### Features
- **Real-time Monitoring**: Voltage, current, temperature
- **GPS Tracking**: Location monitoring with NEO-6M
- **Local Alerts**: Over-voltage, temperature warnings
- **ICP Integration**: Direct blockchain communication
- **Low Power**: Optimized for battery operation

### Specifications
- **MCU**: ESP32-WROOM-32
- **Sensors**: INA219 (V/I), DS18B20 (Temp), NEO-6M (GPS)
- **Display**: Optional OLED 128x64
- **Power**: Li-ion battery with BMS
- **Connectivity**: WiFi, Bluetooth

### Code Structure
```cpp
// Main monitoring loop
void setup() {
    initSensors();
    initWiFi();
    initICP();
}

void loop() {
    readSensorData();
    processAlerts();
    sendToICP();
    delay(MONITORING_INTERVAL);
}
```

## 🖥️ Raspberry Pi Kiosk

### Features
- **User Interface**: Touch screen kiosk
- **Battery Disbursement**: Physical battery exchange
- **ICP Integration**: Direct canister communication
- **Local Processing**: Edge computing capabilities
- **Secure Boot**: Hardware security features

### Specifications
- **Model**: Raspberry Pi 4B (4GB RAM)
- **OS**: Raspberry Pi OS Lite
- **Display**: 7" Touch Screen
- **Storage**: 32GB SD Card
- **Connectivity**: Ethernet, WiFi

### Software Stack
- **Runtime**: Node.js/Python
- **UI Framework**: Electron/Kivy
- **ICP SDK**: dfx, agent-js
- **Hardware Control**: GPIO libraries

## ⚡ Battery Management System (BMS)

### Integration Points
- **ESP32 Communication**: I2C/SPI protocols
- **Safety Monitoring**: Over-charge/discharge protection
- **Cell Balancing**: Maintain cell voltage balance
- **State Reporting**: SoC, SoH, temperature

### Supported BMS Types
- **Smart BMS**: With UART/CAN communication
- **Basic BMS**: Analog signal reading
- **Custom BMS**: Tailored for specific batteries

## 📡 Communication Protocols

### ESP32 ↔ ICP
- **Protocol**: HTTPS over WiFi
- **Authentication**: ICP Internet Identity
- **Data Format**: JSON/Candid
- **Frequency**: Configurable (default 30s)

### Raspberry Pi ↔ ICP
- **Protocol**: WebSocket/HTTP
- **Framework**: dfx agent
- **Real-time**: Live canister updates
- **Caching**: Local data storage

## 🔧 Setup & Installation

### ESP32 Setup
```bash
# Install ESP-IDF
git clone --recursive https://github.com/espressif/esp-idf.git
cd esp-idf && ./install.sh

# Configure project
cd hardware/esp32-monitor
idf.py menuconfig

# Build and flash
idf.py build
idf.py flash
```

### Raspberry Pi Setup
```bash
# Update system
sudo apt update && sudo apt upgrade

# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Install DFX
sh -ci "$(curl -fsSL https://sdk.dfinity.org/install.sh)"

# Setup kiosk application
cd hardware/raspberry-pi-kiosk
npm install
npm run setup
```

## 🔒 Security Considerations

- **Secure Boot**: Hardware-level security
- **Encrypted Communication**: TLS/SSL protocols
- **Identity Management**: ICP-based authentication
- **Firmware Updates**: Secure OTA updates
- **Physical Security**: Tamper detection

## 📊 Monitoring & Diagnostics

- **Health Checks**: Automated system monitoring
- **Error Logging**: Comprehensive error tracking
- **Performance Metrics**: Resource usage monitoring
- **Remote Diagnostics**: ICP-based remote access

## 🔄 Maintenance

- **Firmware Updates**: Regular security patches
- **Calibration**: Sensor accuracy maintenance
- **Battery Replacement**: Scheduled maintenance
- **Hardware Inspection**: Physical component checks
