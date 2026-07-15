![STM32F405](https://img.shields.io/badge/FC%20MCU-STM32F405-red?style=flat-square)
![AT32F421](https://img.shields.io/badge/ESC%20MCU-AT32F421%20x4-orange?style=flat-square)
![Betaflight](https://img.shields.io/badge/Firmware-Betaflight-blue?style=flat-square)
![AM32](https://img.shields.io/badge/ESC%20Firmware-AM32-brightgreen?style=flat-square)
![KiCad](https://img.shields.io/badge/PCB-KiCad%2010-blue?style=flat-square)
![4-Layer](https://img.shields.io/badge/Layers-4--Layer-yellow?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-lightgrey?style=flat-square)
 
---
 
# Dragonfly
 
A custom all-in-one flight controller + ESC, built entirely from discrete ICs rather than premade modules, designed for me by me. Flight control and all 4 motor drivers live on a single 4-layer PCB, designed from scratch in KiCad.
 
# Why I Built This
 
I wanted to go past just building a flight controller most DIY FC projects stop at a board that reads a gyro and outputs signals. I wanted the whole thing: FC and ESC combined on one board, IC-level design instead of stacking pre-built modules, a custom 3D-printed frame, and firmware configured to actually fly and hold up to real maneuvers, not just hover.
 
This became a fromscratch systems project schematic, PCB layout, mechanical frame design, and firmware, all built and understood end-to-end rather than assembled from a kit.
 
---
 
## Features
 
- 4-layer PCB designed from scratch in KiCad, all-in-one FC + ESC on a single board
- STM32F405RGTx flight controller MCU running Betaflight, custom unified target
- 4x independent ESC channels, each with its own AT32F421G8U7 MCU running AM32 firmware real per-motor commutation, not a single shared driver
- FD6288Q 3-phase gate drivers + discrete MOSFETs per channel, sized for freestyle current draw, not just hover
- ICM-20602 IMU (SPI), isolated placement and routing to minimize motor-noise coupling into gyro data
- AT7456E OSD for FPV video overlay (battery voltage, timer)
- BMP280 barometer for altitude hold
- TPS5430 buck (5V) + AMS1117-3.3 LDO + dedicated L78L08 8V rail for gate drivers — separate, correctly isolated power domains
- Individual SWD test points per ESC channel for one-time AM32 flashing
- ELRS receiver support (Happymodel Nano RX) over UART
- Custom 3" toothpick-class frame, designed in Fusion 360, 3D printed
- **Estimated build cost:** ~$250–300 (board, motors, frame, battery, receiver, transmitter)
---
 
## What's Inside
 
| Component | Part | Specification |
|---|---|---|
| Flight Controller MCU | STM32F405RGTx | ARM Cortex-M4, 168 MHz |
| IMU | ICM-20602 | 6-axis, SPI |
| ESC MCU (x4) | AT32F421G8U7 | One per motor, runs AM32 |
| Gate Driver (x4) | FD6288Q | 3-phase, one per motor |
| Motor Drive | 6x MOSFET per channel | 24 total, sized for real current draw |
| Buck Regulator | TPS5430 | Battery → 5V |
| LDO | AMS1117-3.3 | 5V → 3.3V |
| Gate Driver Supply | L78L08 | Battery → 8V, dedicated rail |
| OSD | AT7456E | Analog FPV video overlay |
| Barometer | BMP280 | Altitude hold |
| Receiver | Happymodel ELRS Nano RX | UART |
| Transmitter | RadioMaster Zorro (ELRS) | Full-size hall gimbals |
| Motors | 3" class, 1404, ~3800–4500KV | 4S |
| Frame | Custom 3" toothpick | 3D printed, Fusion 360 |
| PCB | 4-layer | KiCad |
 
---
 
## Firmware
 
**Status:** in progress configuration and pin-mapping stage, not reqady to flash
 
Two separate firmware bases run on this board:
 
- **Betaflight** (main STM32F405) custom unified target describing this board's exact pin map (motors, IMU SPI, receiver UART)
- **AM32** (each of the 4 AT32F421 ESC MCUs) open-source ESC firmware, flashed individually per channel via dedicated SWD test points
```bash
firmware/
├── betaflight-unified-target/   # Unified target config for the main FC
├── am32/                        # AM32 firmware source, per-channel builds
└── notes.md                     # Pin mapping reference
```
 
---
 
## How to Use
 
### Hardware
 
1. PCB files are located in `PCB/`
2. Open the `.kicad_pro` file in KiCad 8+
3. Upload Gerbers from `PCB/gerbers/` to JLCPCB (4-layer)
4. Order components using `BOM/BOM.csv`
5. Frame STEP file is available in `CAD/`
### Firmware
 
1. Flash AM32 onto each of the 4 ESC MCUs individually, using the SWD test points per channel
2. Flash Betaflight onto the main STM32 via USB-C, using the custom unified target in `firmware/betaflight-unified-target/`
3. Configure IMU calibration, receiver binding, and OSD via Betaflight Configurator
---
 
## Repository Structure
 
```text
Dragonfly/
├── PCB/                         # KiCad project + Gerbers
├── CAD/                         # Fusion 360 frame design (.step)
├── firmware/                    # Betaflight unified target + AM32
├── BOM/                         # Bill of Materials
├── imgs/                        # Photos and renders
└── README.md
```
 
---
 
## Built By
 
**broccoli 🥦** — Solo hardware builder from Pakistan.
 
*Chasing what I love. GEO*
