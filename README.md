# 🌾 SmartAgri Node — The All-in-One Environmental Intelligence Board (ESP32-C3)
<img width="774" height="484" alt="image" src="https://github.com/user-attachments/assets/9d4e06cd-fc3c-408a-9c87-1d1ae822dc7e" />

A custom 4-layer PCB designed in KiCad for smart agriculture and ground-to-orbit environmental data logging — built around the **ESP32-C3-WROOM-02-H4**, with onboard sensing, local microSD storage, off-grid solar/LiPo power-path management, and **NASA POWER** satellite data fusion.

### 🔗 NASA Space Apps Challenge — Quick Links
**🌐 Live Ground-to-Orbit Dashboard:** [Open Interactive Dashboard](https://tashfeen-electronics.github.io/NASA-SPACE-APP/)
**📊 7-Slide Pitch Deck:** [View Live Presentation](https://view.officeapps.live.com/op/view.aspx?src=https://raw.githubusercontent.com/tashfeen-electronics/NASA-SPACE-APP/main/SmartAgri%20Node%20%E2%80%94%20NASA%20Space%20Apps%20Challenge.pptx)
* **🛠️ Hardware Design Files:** [`ESP32 Project/`](ESP32%20Project/) (KiCad Schematic, 4-Layer PCB Layout & BOM)

---

## 🚀 Overview

Powered by the **ESP32-C3-WROOM-02-H4**, SmartAgri Node is an edge-computing environmental node engineered to ground-truth macro-scale satellite observations (such as **NASA POWER** agroclimatology and **NASA SMAP** soil moisture) with hyper-local farm telemetry.

### Key Capabilities
* **🌱 Precision Microclimate Sensing:** Real-time temperature, humidity, and barometric pressure (`BME280`) plus ambient light intensity (`TEMT6000X01`) for crop exposure and irrigation modeling.
* **☀️ Off-Grid Solar & LiPo Power Path:** Autonomous charging and dynamic load sharing (`MCP73871`) via USB-C/solar input and 1S Li-ion/LiPo battery.
* **💾 Zero-Loss Edge Logging:** Onboard microSD slot (`GSD090012SEU`) and 32 Mbit SPI flash (`W25Q32JVSSIQ`) ensure continuous logging and OTA updates even in rural connectivity dead zones.
* **🔊 Acoustic Environmental Surveillance:** Integrated electret mic amplifier (`MAX4466EXK`) for pest activity, livestock, and field equipment diagnostics.
* **🔌 Plug-and-Play Soil Expansion:** Dedicated `I2C` (`J4`) and `GPIO` (`J5`) headers for external soil moisture, pH, and EC probes.
* **🛡️ Industrial Front-End Protection:** USB data-line ESD protection (`USBLC6-2SC6`), resettable PTC overcurrent fuse (`0ZCH0110AF2E`), and common-mode power filtering (`CMC-5042PF-AC`).

---

## 🧩 Hardware Architecture

### 🧠 Core Processing & Storage
| Component | Part | Purpose |
| :--- | :--- | :--- |
| `U3` | **ESP32-C3-WROOM-02-H4** | Main RISC-V MCU with integrated Wi-Fi & BLE |
| `U4` | **CP2102N** | USB-to-UART bridge for USB-C flashing and serial debug |
| `U2` | **W25Q32JVSSIQ** | 32 Mbit external SPI flash for OTA updates & log buffering |
| `J3` | **GSD090012SEU** | microSD card slot for offline field telemetry logging |

### 🌡️ Onboard Sensors
| Component | Part | Purpose |
| :--- | :--- | :--- |
| `U6` | **BME280** | Ambient temperature, relative humidity & barometric pressure |
| `Q1` | **TEMT6000X01** | Ambient light intensity sensor for sunlight exposure analysis |
| `U7` | **MAX4466EXK** | Low-noise microphone amplifier for acoustic sensing |

### 🔋 Power Management & Protection
| Component | Part | Purpose |
| :--- | :--- | :--- |
| `J1` | **USB-C (2338792-1)** | Primary power & UART programming port |
| `J2` | **JST (B2B-PH-SM4-TB)** | Single-cell Li-ion/LiPo battery connector |
| `U1` | **MCP73871** | Li-ion charge controller with dynamic power-path management |
| `VR1` | **LM1117MPX-3.3** | 3.3V linear voltage regulator |
| `U5` | **USBLC6-2SC6** | ESD transient voltage suppression on USB D+/D- lines |
| `F1` | **0ZCH0110AF2E** | Resettable PTC overcurrent protection fuse |
| `Q2, Q3` | **BC817** | Transistor power switching / load gating |
| `MK1` | **CMC-5042PF-AC** | Common-mode choke for input power line filtering |

### 🕹️ UI, Debug & Expansion
| Component | Purpose |
| :--- | :--- |
| `S1`, `S2` | Dedicated `BOOT` and `RESET` tactile switches |
| `D1–D6` | Status & fault indicator LEDs (Blue, Green, Red) |
| `TP1–TP5` | Exposed SPI bus test points (`MOSI`, `MISO`, `SCLK`, `CS`, `CS-SD`) |
| `J4` | 4-pin `I2C` expansion header (`GND / SCL / SDA / 3.3V`) |
| `J5` | 5-pin `GPIO` and auxiliary power expansion header |

---

## 🧱 4-Layer PCB Stackup (`Signal / GND / PWR / Signal`)

Designed in **KiCad** using a 4-layer stackup to maintain signal integrity across RF, digital SPI, and sensitive analog sensor domains:
* **Uninterrupted Layer 2 Ground Plane:** Provides a continuous reference plane for the ESP32-C3 RF section and minimizes ground bounce.
* **Controlled SPI Return Paths:** Tightly couples high-speed flash and microSD traces to adjacent reference planes.
* **Dedicated Layer 3 Power Plane:** Low-impedance 3.3V distribution during Wi-Fi transmit current bursts.
* **Mixed-Signal Isolation:** Separates power regulation switching from the `MAX4466` microphone analog front-end.

---

## 📄 License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for details.

**Author:** Tashfeen Electronics — Built with KiCad for the NASA International Space Apps Challenge.
