# Blinker One

🚧 **Work in progress** — waiting for some components before the next hardware tests.

## What is it?

Blinker One is an open source handheld device based on the **ESP32-S3**.

The idea is to build a small portable platform that can be used for:
- simple retro / homebrew games
- small virtual companion experiments
- home automation control over Wi‑Fi / BLE
- embedded UI, audio and haptics experiments

It’s not meant to be a polished product.  
The goal is mostly to have a flexible device to test ideas, build small applications, and share both hardware and firmware.

---

## Repository structure

```
BlinkerOne
.
├── Documents
│   ├── Critical_Item_Development_Specification(CIDS).pdf
│   ├── Hardware_Description_Document(HDD).pdf
│   ├── Software_Description_Document(SDD).pdf
│   └── Components_Derating.pdf
├── Hardware
│   ├── Gerber/
│   ├── Schematic/
│   └── Bill_Of_Materials(BOM).xlsx
└── Software
    ├── Sources/
    └── BlinkerOne_MAIN_FlowDiagram.pdf
```

---

## Main hardware

| Category | Reference | Notes |
|---|---|---|
| MCU | ESP32-S3-WROOM-1-N16R8 | Main controller, Wi‑Fi, Bluetooth, PSRAM |
| Power | XC6220B331MR | 3.3V regulator |
| Haptics | DRV2605LDGSR | LRA haptic driver over I²C |
| Audio | MAX98357AETE+T | I²S audio amp |
| Display | HS20BS097RX | SPI display |
| Joystick | TS-1095PS-A1B2-C3D2 | 5-way switch |
| Storage | microSD | Assets, configs, ROMs, saves |
| Battery | LiPo + external charger | Portable power |

---

## Current hardware notes

### Power
The board uses an **XC6220B331MR** 3.3V regulator.  
The idea is to keep the system stable even when battery voltage drops or current peaks appear during Wi‑Fi or audio activity.

### Joystick
The 5-way joystick is wired in **active-low**:

- **UP**: GPIO 21
- **DOWN**: GPIO 2
- **LEFT**: GPIO 48
- **RIGHT**: GPIO 47
- **CENTER**: GPIO 1

### Haptics
The **DRV2605L** is connected over I²C:
- **SDA**: GPIO 4
- **SCL**: GPIO 5

### Audio
Audio output is handled by the **MAX98357A** over I²S for a small onboard speaker.

### Storage
A **microSD** card is used for assets, save files, configs, and any larger resources.

---

## What I want to do with it

Planned use cases include:

- a small emulation / homebrew console
- a virtual pet or simple companion system
- a portable smart home remote
- a small status/dashboard device

I’m keeping the platform fairly open on purpose, so it can be reused for different projects instead of a single fixed application.

---

## Software direction

The firmware will probably target one or more of these environments depending on the use case:

- **ESP-IDF**
- **Arduino / PlatformIO**
- possibly **MicroPython** for quick experiments

The basic software blocks are expected to include:
- display driver
- joystick input
- I²S audio
- DRV2605L haptics
- microSD support
- a few example applications

---

## Project status

Current status:
- [ ] hardware revision fully validated
- [ ] display / audio / haptics / input drivers
- [ ] example firmware
- [ ] setup / usage documentation

So for now this repository is mainly a place to store the hardware files, documentation, and upcoming firmware work.

Some parts may change during testing.

---

## Contributing

If you want to contribute, feel free to open an issue or a pull request.

Possible contributions:
- hardware improvements
- firmware / drivers
- demo applications
- documentation fixes

---

## License

Open source project by **DEON electronics**.

Exact licenses for hardware and firmware are still to be defined.

---
