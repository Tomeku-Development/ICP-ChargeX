# ESP32 Battery Monitor - Schematic Diagram

## 📋 Overview

Complete schematic diagram and connection details for the ESP32-based battery monitoring node in the ChargeX system.

---

## 🔌 **ESP32 Pinout & Connections**

### ESP32-WROOM-32 Pin Configuration

```
                    ESP32-WROOM-32 Development Board
                    ┌─────────────────────────────────┐
                    │  3V3  ■ ■ GND                  │
                    │  EN   ■ ■ GPIO23               │
                    │  VP   ■ ■ GPIO22  ──── SCL (I2C)
                    │  VN   ■ ■ GPIO1   ──── TX      │
                    │  GPIO34 ■ ■ GPIO3 ──── RX      │
                    │  GPIO35 ■ ■ GPIO21 ──── SDA (I2C)
                    │  GPIO32 ■ ■ GND                │
                    │  GPIO33 ■ ■ GPIO19 ──── MISO   │
                    │  GPIO25 ■ ■ GPIO18 ──── SCK    │
                    │  GPIO26 ■ ■ GPIO5  ──── CS (SD)│
                    │  GPIO27 ■ ■ GPIO17 ──── GPS TX │
                    │  GPIO14 ■ ■ GPIO16 ──── GPS RX │
                    │  GPIO12 ■ ■ GPIO4  ──── 1-Wire │
                    │  GPIO13 ■ ■ GPIO0              │
                    │  GND  ■ ■ GPIO2               │
                    │  VIN  ■ ■ GPIO15              │
                    │         USB                     │
                    └─────────────────────────────────┘
```

---

## 🔧 **Complete System Schematic**

```
Power Management Section:
┌─────────────────────────────────────────────────────────────────────────────┐
│                                POWER SYSTEM                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐             │
│  │18650 #1  │    │18650 #2  │    │ TP4056   │    │AMS1117   │             │
│  │  3.7V    │────│  3.7V    │────│USB-C     │────│3.3V REG  │──── 3.3V    │
│  │ 3000mAh  │    │ 3000mAh  │    │CHARGER   │    │          │             │
│  └──────────┘    └──────────┘    └──────────┘    └──────────┘             │
│       │               │               │               │                    │
│       └───────────────┼───────────────┼───────────────┘                    │
│                       │               │                                    │
│  ┌─────────────────────┘               │                                    │
│  │ ┌───────────────────────────────────┘                                    │
│  │ │  ┌──────────┐                                                          │
│  │ │  │  POWER   │                                                          │
│  │ │  │ SWITCH   │                                                          │
│  │ │  │  SPDT    │                                                          │
│  │ │  └──────────┘                                                          │
│  │ │       │                                                                │
│  │ └───────┼─── BATTERY+ (7.4V)                                             │
│  └─────────┼─── BATTERY- (GND)                                              │
│            │                                                                │
└────────────┼────────────────────────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                              SENSOR SECTION                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌──────────────────────────────────────────────────────────────────────┐   │
│  │                        ESP32-WROOM-32                                │   │
│  │                                                                      │   │
│  │  GPIO21 (SDA) ────┐                          GPIO22 (SCL) ────┐     │   │
│  │  GPIO4  (1-Wire)──┼──┐                       GPIO17 (TX) ─────┼──┐  │   │
│  │  GPIO16 (RX) ─────┼──┼──┐                    GPIO5  (CS) ─────┼──┼──┼─┐│   │
│  │  GPIO18 (SCK) ────┼──┼──┼──┐                 GPIO19 (MISO)────┼──┼──┼─┼┤   │
│  │  3.3V ────────────┼──┼──┼──┼──┐              GND ────────────┼──┼──┼─┼┤   │
│  │  GND ─────────────┼──┼──┼──┼──┼──┐                           │  │  │ ││   │
│  └───────────────────┼──┼──┼──┼──┼──┼───────────────────────────┼──┼──┼─┼┼───┘
│                      │  │  │  │  │  │                           │  │  │ ││
│  I2C Bus:            │  │  │  │  │  │                           │  │  │ ││
│  ┌───────────────────┘  │  │  │  │  │                           │  │  │ ││
│  │  ┌────────────────────┘  │  │  │  │                           │  │  │ ││
│  │  │                       │  │  │  │                           │  │  │ ││
│  │  │  ┌──────────┐         │  │  │  │         ┌──────────┐      │  │  │ ││
│  │  │  │  INA219  │         │  │  │  │         │  DS3231  │      │  │  │ ││
│  │  └──│SDA   VCC │─────────┼──┼──┼──┼─────────│VCC   SDA │──────┘  │  │ ││
│  └─────│SCL   GND │─────────┼──┼──┼──┼─────────│GND   SCL │─────────┘  │ ││
│        │VIN-  VIN+│         │  │  │  │         │          │            │ ││
│        └──────────┘         │  │  │  │         └──────────┘            │ ││
│             │  │            │  │  │  │                                 │ ││
│             │  │            │  │  │  │         ┌──────────┐            │ ││
│             │  │            │  │  │  │         │ SSD1306  │            │ ││
│             │  │            │  │  │  └─────────│VCC   SDA │────────────┘ ││
│             │  │            │  │  └────────────│GND   SCL │──────────────┘│
│             │  │            │  │               │          │               │
│             │  └── To Target │  │               └──────────┘               │
│             │     Battery    │  │                                         │
│             └── Monitoring   │  │                                         │
│                              │  │                                         │
│  1-Wire Bus:                 │  │               SPI Bus:                  │
│  ┌────────────────────────────┘  │               ┌───────────────────────────┘
│  │                              │               │
│  │  ┌──────────┐                │               │  ┌──────────┐
│  │  │ DS18B20  │                │               │  │ MicroSD  │
│  │  │  TEMP    │                │               │  │  Card    │
│  └──│DQ    VCC │────────────────┼───────────────┼──│VCC   CS  │
│     │GND       │────────────────┼───────────────┼──│GND   MOSI│ (GPIO23)
│     └──────────┘                │               │  │SCK   MISO│
│                                 │               │  └──────────┘
│  UART (GPS):                    │               │
│  ┌───────────────────────────────┘               │
│  │                                              │
│  │  ┌──────────┐                                │
│  │  │ NEO-6M   │                                │
│  │  │   GPS    │                                │
│  └──│RX    VCC │────────────────────────────────┘
│     │TX    GND │
│     └──────────┘
│
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 📊 **Detailed Pin Connections Table**

### I2C Devices (3.3V)

| Device | VCC | GND | SDA | SCL | Additional |
|--------|-----|-----|-----|-----|------------|
| **INA219** | 3.3V | GND | GPIO21 | GPIO22 | VIN+/VIN- to target battery |
| **DS3231 RTC** | 3.3V | GND | GPIO21 | GPIO22 | Battery backup (CR2032) |
| **SSD1306 OLED** | 3.3V | GND | GPIO21 | GPIO22 | 128x64 resolution |

**I2C Addresses:**
- INA219: `0x40` (default)
- DS3231: `0x68` (default)  
- SSD1306: `0x3C` (default)

### SPI Device (3.3V)

| Device | VCC | GND | SCK | MISO | MOSI | CS |
|--------|-----|-----|-----|------|------|----|
| **MicroSD** | 3.3V | GND | GPIO18 | GPIO19 | GPIO23 | GPIO5 |

### UART Device (3.3V)

| Device | VCC | GND | TX (ESP RX) | RX (ESP TX) | Additional |
|--------|-----|-----|-------------|-------------|------------|
| **NEO-6M GPS** | 3.3V | GND | GPIO16 | GPIO17 | External antenna |

### 1-Wire Device (3.3V)

| Device | VCC | GND | Data | Pull-up |
|--------|-----|-----|------|---------|
| **DS18B20** | 3.3V | GND | GPIO4 | 4.7kΩ to 3.3V |

---

## ⚡ **Power Distribution Schematic**

```
Battery Management & Power Distribution:

┌─────────────────────────────────────────────────────────────────────────────┐
│                           POWER DISTRIBUTION                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  18650 Cell #1    18650 Cell #2                                             │
│  ┌─────────┐      ┌─────────┐                                               │
│  │   (+)   │──────│   (+)   │────┐                                          │
│  │  3.7V   │      │  3.7V   │    │ 7.4V Series Connection                  │
│  │ 3000mAh │      │ 3000mAh │    │                                          │
│  │   (-)   │──┐   └─────────┘    │                                          │
│  └─────────┘  │                  │                                          │
│               │                  │                                          │
│               │ Battery Common   │ Battery Positive                         │
│               │      (-)         │      (+)                                 │
│               │      │           │       │                                  │
│               │      │       ┌───┴───┐   │  ┌─────────────┐                │
│               │      │       │ SPDT  │   │  │   TP4056    │                │
│               │      │       │ POWER │   │  │   USB-C     │                │
│               │      │       │SWITCH │   │  │  CHARGER    │                │
│               │      │       └───┬───┘   │  │  MODULE     │                │
│               │      │           │       │  └─────────────┘                │
│               │      │           │       │         │                       │
│               │      │           │       │         │ Charge Current        │
│               │      │           │       │         │ (1A max)             │
│               │      │           │       │         │                       │
│               │      └───────────┼───────┼─────────┘                       │
│               │                  │       │                                 │
│               │            ┌─────┴─────┐ │                                 │
│               │            │  AMS1117  │ │                                 │
│               │            │   3.3V    │ │                                 │
│               │            │ REGULATOR │ │                                 │
│               │            └─────┬─────┘ │                                 │
│               │                  │       │                                 │
│               │                  │ 3.3V  │ 7.4V (Raw Battery)             │
│               │                  │       │                                 │
│               └──────────────────┼───────┼─────────────────────────────────│
│                                  │       │                                 │
│  ┌───────────────────────────────┘       │                                 │
│  │ 3.3V Distribution                     │                                 │
│  │ ├── ESP32 VCC                        │                                 │
│  │ ├── INA219 VCC                       │                                 │
│  │ ├── DS18B20 VCC                      │                                 │
│  │ ├── NEO-6M VCC                       │                                 │
│  │ ├── DS3231 VCC                       │                                 │
│  │ ├── SSD1306 VCC                      │                                 │
│  │ └── MicroSD VCC                      │                                 │
│  │                                      │                                 │
│  │ ┌────────────────────────────────────┘                                 │
│  │ │ 7.4V (Battery Voltage Monitoring)                                    │
│  │ │ └── INA219 VIN+ (Through Current Shunt)                             │
│  │ │                                                                      │
│  │ │ Ground Distribution                                                  │
│  │ │ ├── ESP32 GND                                                        │
│  │ │ ├── All Sensor GND                                                   │
│  │ │ ├── Battery Common (-)                                               │
│  │ │ └── INA219 VIN-                                                      │
│  │ │                                                                      │
└──┴─┴──────────────────────────────────────────────────────────────────────┘
```

---

## 🔌 **Current Sensing Circuit Detail**

```
INA219 Current & Voltage Monitoring:

Target Battery Pack (Being Monitored)
┌─────────────────────────────────────┐
│  LiFePO4 4S Battery Pack            │
│  ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐    │
│  │ C1  │─│ C2  │─│ C3  │─│ C4  │    │
│  │3.2V │ │3.2V │ │3.2V │ │3.2V │    │
│  └─────┘ └─────┘ └─────┘ └─────┘    │
│    │                         │      │
│    │                         │      │
└────┼─────────────────────────┼──────┘
     │ Battery Negative        │ Battery Positive
     │ (Common/Ground)         │ (+12.8V Nominal)
     │                         │
     │       ┌─────────────────┘
     │       │ 
     │       │   Current Shunt Resistor (0.1Ω, 1%)
     │       │   ┌─────────────┐
     │       └───│ ≈≈≈≈≈≈≈≈≈≈≈ │───┐
     │           │  0.1 Ohm    │   │
     │           └─────────────┘   │
     │                 │           │
     │                 │           │
     │  ┌──────────────┴───────────┴────────────┐
     │  │            INA219                     │
     │  │         I2C Address: 0x40             │
     │  │                                       │
     └──│VIN-  VCC│───── 3.3V (ESP32)          │
        │VIN+  GND│───── GND                   │
        │SDA   SCL│───── I2C Bus (GPIO21/22)   │
        └─────────────────────────────────────────┘

Voltage Measurement: Across VIN+ and VIN- (Battery Voltage)
Current Measurement: Voltage drop across 0.1Ω shunt resistor
Resolution: 0.1mA current, 4mV voltage
Max Current: ±3.2A continuous
```

---

## 🌡️ **Temperature Sensing Circuit**

```
DS18B20 1-Wire Temperature Sensor:

                     3.3V
                      │
                      │
                   ┌──┴──┐ 4.7kΩ Pull-up Resistor
                   │     │
ESP32 GPIO4 ───────┼─────┴──── DS18B20 Data Pin (DQ)
                   │
                   │      ┌─────────────┐
                   │      │   DS18B20   │
                   │      │ Waterproof  │
                   └──────│DQ       VCC │───── 3.3V
                          │GND          │───── GND
                          └─────────────┘

Features:
- 1-Wire protocol (single data line)
- Waterproof probe for harsh environments
- ±0.5°C accuracy from -10°C to +85°C
- 12-bit resolution (0.0625°C)
- Unique 64-bit address for multiple sensors
```

---

## 📍 **GPS Module Connection**

```
NEO-6M GPS Module UART Interface:

ESP32                        NEO-6M GPS Module
                          ┌─────────────────────┐
GPIO17 (TX) ────────────→ │RX               VCC │ ←─── 3.3V
GPIO16 (RX) ←──────────── │TX               GND │ ←─── GND
                          │PPS          ANTENNA │ ←─── External Antenna
                          └─────────────────────┘

Configuration:
- Baud Rate: 9600 (default)
- Protocol: NMEA 0183
- Update Rate: 1Hz (configurable up to 10Hz)
- Accuracy: 2.5m CEP (50% probability)
- Cold Start: 26s, Hot Start: 1s
```

---

## 💾 **Storage & Display Connections**

```
SPI MicroSD Card Module:

ESP32                        MicroSD Module
                          ┌─────────────────────┐
GPIO18 (SCK) ────────────→│SCK              VCC │ ←─── 3.3V
GPIO19 (MISO) ←───────────│MISO             GND │ ←─── GND
GPIO23 (MOSI) ────────────→│MOSI             N/C │
GPIO5  (CS)  ────────────→│CS               N/C │
                          └─────────────────────┘

I2C OLED Display:

ESP32                        SSD1306 OLED
                          ┌─────────────────────┐
GPIO21 (SDA) ←──────────→ │SDA              VCC │ ←─── 3.3V
GPIO22 (SCL) ────────────→│SCL              GND │ ←─── GND
                          └─────────────────────┘

Features:
- 128x64 pixels monochrome
- I2C Address: 0x3C
- Low power consumption
- Status and data display
```

---

## 🔧 **PCB Layout Considerations**

### Component Placement Guidelines

```
PCB Layout (Top View):

┌─────────────────────────────────────────────────────────────┐
│  [USB-C]     [PWR LED]    [STATUS LED]                     │
│                                                             │
│  ┌─────────────────┐                    ┌──────────┐       │
│  │     TP4056      │                    │ AMS1117  │       │
│  │   USB CHARGER   │                    │3.3V REG  │       │
│  └─────────────────┘                    └──────────┘       │
│                                                             │
│          ┌─────────────────────────────────────┐            │
│          │                                     │            │
│          │         ESP32-WROOM-32              │            │
│          │                                     │            │
│          └─────────────────────────────────────┘            │
│                                                             │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐   │
│  │  INA219  │  │ DS18B20  │  │  NEO-6M  │  │ DS3231   │   │
│  │CURR/VOLT │  │   TEMP   │  │   GPS    │  │   RTC    │   │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘   │
│                                                             │
│  ┌──────────┐                           ┌──────────┐       │
│  │ SSD1306  │     [POWER SWITCH]        │ MicroSD  │       │
│  │   OLED   │                           │   SLOT   │       │
│  └──────────┘                           └──────────┘       │
│                                                            │
│  [BATT CONN]              [EXT SENSOR CONN]                │
└─────────────────────────────────────────────────────────────┘

Trace Width Guidelines:
- Power traces (3.3V, Battery): 0.5mm minimum
- I2C/SPI/UART signals: 0.2mm
- Ground plane: Continuous pour
- Via size: 0.3mm drill, 0.6mm pad
```

### Critical Design Notes

1. **Power Plane Isolation**: Separate analog and digital power planes
2. **Crystal Placement**: Keep ESP32 crystal traces short and shielded
3. **Antenna Clearance**: 15mm keepout around GPS antenna
4. **Current Sensing**: Use 4-layer PCB for clean current measurement
5. **ESD Protection**: TVS diodes on all external connections
6. **Thermal Management**: Thermal vias under voltage regulators

---

## 📐 **Mechanical Specifications**

### Enclosure Requirements

```
IP65 Waterproof Enclosure:
┌─────────────────────────────────────────┐
│  Dimensions: 120mm x 80mm x 40mm        │
│  Material: ABS Plastic + Gasket Seal    │
│  ┌─────────────────────────────────────┐ │
│  │  PCB Mounting Posts (M3 Screws)    │ │
│  │  ┌─────────────────────────────────┐│ │
│  │  │           PCB Area              ││ │
│  │  │  100mm x 60mm                  ││ │
│  │  └─────────────────────────────────┘│ │
│  └─────────────────────────────────────┘ │
│                                         │
│  Cable Glands:                          │
│  - Power Input (PG7)                    │
│  - Target Battery Connection (PG7)      │
│  - Temperature Probe (PG7)              │
│                                         │
│  External Connectors:                   │
│  - GPS Antenna (SMA)                    │
│  - Programming/Debug (USB-C)            │
└─────────────────────────────────────────┘
```

---

## 🔍 **Testing & Validation Points**

### Test Points on PCB

| Test Point | Signal | Purpose |
|------------|--------|---------|
| TP1 | 3.3V | Power rail verification |
| TP2 | Battery+ | Input voltage monitoring |
| TP3 | I2C_SDA | I2C signal integrity |
| TP4 | I2C_SCL | I2C clock verification |
| TP5 | GPS_TX | GPS data output |
| TP6 | Current Shunt+ | Current measurement calibration |
| TP7 | Current Shunt- | Current measurement reference |

### Calibration Procedures

1. **Current Measurement**: Use precision current source (±1mA accuracy)
2. **Voltage Measurement**: Calibrate against precision DMM
3. **Temperature Sensor**: Ice bath (0°C) and boiling water (100°C) calibration
4. **GPS Accuracy**: Known location verification
5. **RTC Accuracy**: Compare against NTP time source

This comprehensive schematic provides all the technical details needed to build the ESP32 battery monitoring hardware for the ChargeX system. The design prioritizes accuracy, reliability, and ease of manufacturing while maintaining compatibility with the ICP blockchain integration requirements.
