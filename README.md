# Relay Driver Circuit — LTspice Simulation
 
## Overview
LTspice simulation of a relay driver circuit that uses a 3.3V microcontroller signal to switch a 12V relay coil. Designed as part of a battery discharge test system for DC-DC solar-to-EV power conversion research.
 
## Schematic
![Schematic](https://github.com/SUSH1237/Relay-Driver/blob/a4ee95b3e3a0fec9a7f3e2e174f8b01526c365e9/RelayDriverSchem.png)
 
## Simulation Results
![Simulation Graph](https://github.com/SUSH1237/Relay-Driver/blob/a4ee95b3e3a0fec9a7f3e2e174f8b01526c365e9/RelayDriverGraph.png)
 
## Circuit Description
A 2N2222 NPN transistor acts as a low-side switch, allowing a 3.3V GPIO signal to control a 12V relay coil without exposing the microcontroller to high voltage. A 1N4007 flyback diode protects the transistor from inductive voltage spikes when the relay deactivates.
 
## Components
| Reference | Value | Description |
|-----------|-------|-------------|
| V1 | 3.3V | Microcontroller signal source |
| V2 | 12V | Relay coil power supply |
| Q1 | 2N2222 | NPN transistor (low-side switch) |
| R1 | 1kΩ | Base current limiting resistor |
| L1 | 100mH | Relay coil model (360Ω series resistance) |
| D1 | 1N4007 | Flyback diode |
 
## How It Works
The 3.3V microcontroller GPIO pin cannot directly drive a 12V relay coil. Instead:
1. The Arduino sends a 3.3V signal through a 1kΩ resistor to the base of Q1
2. Q1 switches on, pulling the collector to near 0V
3. This completes the 12V coil circuit, energizing the relay
4. When the signal goes low, Q1 turns off and D1 clamps the inductive spike
## Simulation Results
| Measurement | Value | Status |
|------------|-------|--------|
| Collector voltage V(n005) | ~67mV | ✅ Transistor fully on |
| Coil current I(L1) | ~33mA | ✅ Expected (12V ÷ 360Ω) |
| MCU pin current I(R1) | ~2.3mA | ✅ Safe (well under 40mA limit) |
 
## Files
```
├── README.md
├── relay_driver.asc       # LTspice schematic file
├── schematic.png          # Schematic screenshot
└── graph.png              # Simulation results screenshot
```
 
## Part of Larger Project
This relay driver is one component of a multi-battery sequential discharge test system used to validate a round-robin switching algorithm for DC-DC solar-to-EV charging research.
 
## Tools
- LTspice XVII
