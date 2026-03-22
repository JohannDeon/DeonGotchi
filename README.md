---
# Project Status

🚧 In progress waiting for components

---
## Repository Structure
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

---
# Blinker One - Open Source Console & Versatile Companion

![Brand](https://img.shields.io/badge/Brand-DEON%20electronics-blue)
![Hardware](https://img.shields.io/badge/Hardware-ESP32--S3--N16R8-orange)
![License](https://img.shields.io/badge/License-Open%20Source-green)

**Blinker One** is an **open source** handheld console based on the **ESP32‑S3**, designed as a **versatile tool**:

- 🎮 **Retro game emulation** (old consoles, simple homebrew games)  
- 🧬 **Custom virtual environments** or small DIY “OS‑like” systems  
- 🏠 **Home automation / IoT control** via **Wi‑Fi** and **Bluetooth**  
- 🎨 Experiments in UI/UX, haptics, and embedded audio

The goal is not just to build a “modern Tamagotchi”, but a **modular platform** to hack, learn, and prototype interactive physical interfaces.

---

## Project Goals

- **Open hardware & open firmware**: public schematics, PCB, code, and examples  
- **Versatility**: allow Blinker One to become:
  - A mini emulation console (NES‑like, GB‑like, simple retro games)
  - A virtual assistant, interactive companion, or custom “micro OS”
  - A smart home remote (MQTT, HTTP, BLE, etc.)
  - A portable dashboard (sensors, logs, notifications, etc.)
- **Developer‑friendly**: firmware in C/C++ (ESP‑IDF / Arduino / PlatformIO) or MicroPython if preferred, with example projects
- **Community‑driven**: hardware and software contributions are encouraged

---

## Hardware (Main BOM)

| Category        | Reference               | Function                                        |
|----------------|-------------------------|-------------------------------------------------|
| **MCU**        | ESP32-S3-WROOM-1-N16R8  | Dual‑core, Wi‑Fi, BT, 16MB Flash, 8MB PSRAM    |
| **Power**      | XC6220B331MR            | 3.3V 900mA ultra low‑dropout LDO               |
| **Haptics**    | DRV2605LDGSR            | LRA haptic driver via I²C                      |
| **Audio**      | MAX98357AETE+T          | Digital I²S Class‑D audio amplifier            |
| **Display**    | HS20BS097RX             | High‑clarity LCD / TFT (SPI)                   |
| **Joystick**   | TS-1095PS-A1B2-C3D2     | 5‑way multidirectional switch                  |
| **Storage**    | microSD (SDMMC)         | Resources, ROMs, assets, configs               |
| **Battery**    | LiPo + external charger | Portable power supply                          |

---

## Power Management

The **XC6220B331MR** regulator provides a stable 3.3V rail even when the LiPo battery drops below ~3.4V, helping to avoid random resets during current peaks from Wi‑Fi or audio output.

This makes Blinker One suitable for **long‑running use cases** such as dashboards, home automation control, or always‑on companions.

---

## Input — 5‑Way Joystick

The 5‑way joystick is wired in **active‑low logic** with a common GND:

- **UP**: GPIO 21  
- **DOWN**: GPIO 2  
- **LEFT**: GPIO 48  
- **RIGHT**: GPIO 47  
- **CENTER (confirm / click)**: GPIO 1  

Each direction is normally pulled high and goes low (connected to GND) when pressed.

---

## Audio & Haptics

### Audio

- **Amplifier**: MAX98357A (I²S Class‑D)  
- **Input**: Digital I²S audio stream from the ESP32‑S3  
- **Output**: Small speaker on the device  

Use cases include:

- Game audio and sound effects  
- UI sounds and feedback  
- Alerts/notifications for home automation or monitoring

### Haptics

- **Driver**: DRV2605L  
- **Bus**: I²C  
  - SDA: GPIO 4  
  - SCL: GPIO 5  

The DRV2605L can play complex vibration patterns independent of audio, making it useful for:

- UI feedback (clicks, confirmations, errors)  
- Game haptics  
- Silent alerts for notifications or events

---

## Memory & Performance

With **8MB of PSRAM**, Blinker One can:

- Store multiple **framebuffers** for smooth graphics (games, animations, dashboards)  
- Use larger **audio buffers**  
- Load **assets** (sprites, tilesets, fonts, etc.) into memory  

This gives enough headroom for:

- Lightweight emulators  
- Custom “micro‑OS” UI  
- Complex animations or interactive dashboards

---

## Buses & Peripherals

### I²C

Used for:

- **DRV2605L** haptic driver  
- Optional external sensors (IMU, temperature, light sensors, etc.)

Typical firmware will include an **I²C scanner** on boot to detect connected devices.

### SPI

Used for:

- **LCD/TFT display** (HS20BS097RX) with high‑speed SPI  
- Optional extra SPI devices if needed (external flash, sensors, etc.)

### SDMMC (microSD)

- Stores:
  - ROMs and games  
  - Graphics and sound assets  
  - Configuration files (Wi‑Fi credentials, domotics profiles, etc.)  
- Can act as the main resource storage for custom environments or small OS‑like systems.

### Wi‑Fi & Bluetooth (ESP32‑S3)

- **Wi‑Fi**:
  - HTTP / REST APIs  
  - MQTT for home automation (e.g. Home Assistant)  
  - WebSockets, simple web UI, etc.
- **Bluetooth**:
  - BLE communication with smartphones  
  - Custom BLE services for control or data display  
  - Remote control peripherals

---

## Example Use Cases

### 1. Mini Emulation Console

- Run simple emulators (8‑bit / lightweight 16‑bit)  
- Load ROMs from microSD  
- Control via 5‑way joystick  
- Audio + haptic feedback for a complete “pocket console” experience

### 2. Custom Virtual Environment / Companion

- Create your own **virtual pet**, assistant, or simulation  
- Display character states, stats, or environments on screen  
- Store save files and states on microSD  
- Use haptics/audio to give personality to your companion

### 3. Home Automation Controller

- UI with menus to control lights, shutters, scenes, etc.  
- Communicate via Wi‑Fi (MQTT/HTTP) or BLE with your smart home system  
- Use vibrations and sounds as confirmation or error feedback  

Blinker One can act as a **dedicated, physical remote** for your smart home.

### 4. Portable Dashboard / Monitor

- Display sensor data (local or via network)  
- Show logs, alerts, or system status  
- Integrate with servers, clusters, or IoT devices  
- Useful as a small **status monitor** you can carry around

---

## Software Stack & Development

The project aims to stay **flexible** so you can choose your preferred development environment:

- **ESP‑IDF** (official Espressif framework) for low‑level control and advanced projects  
- **Arduino / PlatformIO** for easier onboarding and faster prototyping  
- **MicroPython** / **CircuitPython** (where supported on ESP32‑S3 + PSRAM) for scripting‑style development

The repository will provide:

- A **base firmware** with:
  - Display driver  
  - Joystick input handling  
  - Audio (I²S)  
  - Haptics (DRV2605L via I²C)  
  - microSD (SDMMC) and basic filesystem handling
- **Example projects**, such as:
  - Simple game / emulator demo  
  - Home automation client (e.g. MQTT controller)  
  - Companion / UI demo

---

## Project Status

- [ ] Hardware revision validated / under iteration  
- [ ] Core drivers (display, audio, haptics, joystick)  
- [ ] SDK / example firmwares for developers  
- [ ] API documentation and tutorials  

Some parts are still experimental and may change. Feedback and suggestions are very welcome via issues or pull requests.

---

## Contributing

Contributions of all kinds are welcome:

- **Hardware**: alternative components, board revisions, shields, or docks  
- **Software**: drivers, libraries, examples, games, domotics integrations, PC tools  
- **Documentation**: tutorials, “getting started” guides, translations

Typical workflow:

1. Fork the repository  
2. Create a feature branch (`feature/my-awesome-idea`)  
3. Open a Pull Request with a clear description and rationale

---

## License & Credits

- Project initiated by **DEON electronics**  
- Hardware and firmware are released under open source licenses  
  - (To be defined precisely: e.g. MIT / GPL for firmware, CERN OHL for hardware, etc.)

---
