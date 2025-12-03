# Self-Watering Plant 🌿💧

A simple self-watering plant project that automates watering based on soil moisture. This repository contains the hardware wiring, firmware code and basic setup notes to get a plant watering system running using a microcontroller, a moisture sensor and a water pump (or solenoid valve).

This README gives an overview, parts list, wiring guidance, software setup and troubleshooting tips so you can get the system working quickly. 🚀

---

## Table of contents 📚

- [Overview](#overview)
- [Features](#features)
- [Parts & tools](#parts--tools)
- [Hardware wiring](#hardware-wiring)
- [Firmware / Software setup](#firmware--software-setup)
- [Configuration](#configuration)
- [Operation](#operation)
- [Troubleshooting](#troubleshooting)
- [Project structure](#project-structure)
- [License & contact](#license--contact)

---

## Overview 📝

This project monitors soil moisture and waters the plant automatically when moisture drops below a configurable threshold. It is intended as a small DIY project for hobbyists and can be adapted for different microcontrollers (Arduino, ESP8266, ESP32, Raspberry Pi Pico, etc.) and pumps/valves.

---

## Features ✨

- Periodic soil moisture readings 🛰️
- Automatic watering when dryness threshold is reached 💧
- Configurable watering duration and sampling interval ⏲️
- Manual testing mode for safety and calibration 🧪

---

## Parts & tools 🧰

Typical components (adjust to your build):

- Microcontroller (e.g., Arduino Uno / Nano, ESP8266, ESP32) ⚙️  
- Soil moisture sensor (capacitive recommended) 🌱  
- Water pump (submersible) or solenoid valve and power driver (e.g., MOSFET/relay) 🛠️  
- Relay module or MOSFET and diode (for pump control) 🔌  
- Power supply (suitable for pump and microcontroller) 🔋  
- Tubing and water reservoir 💧  
- Breadboard / wires / connectors 🧩  
- Enclosure for electronics (optional) 🧰

Recommended: use a capacitive moisture sensor to avoid corrosion; if using resistive sensors, expect shorter lifespan.

---

## Hardware wiring 🔧

A generic wiring example:

- Moisture sensor:
  - VCC -> 3.3V or 5V (match your sensor & MCU)  
  - GND -> GND  
  - SIG (analog) -> Analog input (e.g., A0)

- Pump / valve:
  - Pump positive -> External power supply positive  
  - Pump negative -> Relay / MOSFET drain / transistor collector  
  - Relay / MOSFET gate -> Microcontroller digital pin (with appropriate resistor)  
  - Use diode/flyback protection where needed and common ground between MCU and pump power supply.

Notes:
- Do NOT drive pumps directly from MCU pins. Use a relay or MOSFET and an appropriate separate power supply.
- Add a flyback diode and base/gate resistor as appropriate to protect electronics.
- Secure tubing and check for leaks before leaving the system unattended.

---

## Firmware / Software setup 🖥️

1. Clone the repository:
   ```
   git clone https://github.com/CereteuPaul/Self-WateringPlant.git
   cd Self-WateringPlant
   ```

2. Open the firmware sketch / source in your preferred IDE:
   - Arduino IDE: open `.ino` file
   - PlatformIO: open the project in VS Code
   - ESP boards: use the board manager and select the correct board

3. Edit configuration parameters (see [Configuration](#configuration)).

4. Compile and upload code to your microcontroller.

5. Test in manual mode first (short watering pulses) to confirm relay/pump control and sensor readings.

---

## Configuration ⚙️

Common configuration options inside the firmware (variable names will vary by implementation):

- MOISTURE_PIN — analog input for the sensor (e.g., A0)  
- PUMP_PIN — digital output for relay or MOSFET control  
- MOISTURE_THRESHOLD — analog value below which watering triggers (calibrate for your soil)  
- WATER_DURATION_MS — how long to run the pump per cycle (in milliseconds)  
- SAMPLE_INTERVAL_MS — how often to check the moisture (in milliseconds)  
- MANUAL_TEST_PIN or serial command for manual trigger

Calibration tip: read raw sensor values for wet and dry soil and set the threshold between them.

---

## Operation ▶️

- Start with short watering durations (e.g., 500–1500 ms) and observe moisture response.
- Ensure the reservoir has enough water and tubing is connected correctly.
- Consider adding safety features in code:
  - Maximum daily watering limit
  - Minimum interval between watering cycles
  - Low-reservoir detection (optional float sensor)

If using a Wi-Fi board, you can optionally add telemetry (e.g., send moisture readings to a dashboard or log to serial).

---

## Troubleshooting 🐛

- Pump does not activate:
  - Check pump power supply and that relay/MOSFET wiring is correct.
  - Verify control pin toggles (use a multimeter or LED temporarily).
  - Ensure grounds are common between MCU and pump power.

- Sensor readings unstable or noisy:
  - Use a capacitive sensor or add filtering (take multiple samples and average).
  - Ensure sensor probe is clean and not corroded.
  - Add a small delay between readings.

- False triggers / overwatering:
  - Increase the moisture threshold or sample interval.
  - Implement hysteresis in firmware (require several consecutive low readings before watering).

- Board won't program:
  - Check board selection, port, and drivers in your IDE.
  - If using 5V vs 3.3V logic, ensure compatibility.

---

## Project structure 📁

Adjust based on the actual repository content, a typical layout:

- firmware/ — microcontroller code (Arduino sketches, PlatformIO project)
- docs/ — wiring diagrams, photos, notes
- hardware/ — schematics, PCB files (if any)
- README.md — this file

---
