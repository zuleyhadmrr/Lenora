# Lenora

A standalone, headless desktop music player built on a Raspberry Pi Zero 2 W. Designed as a first-principles hardware and embedded Linux learning project, documented end-to-end as an open engineering log.

![Status](https://img.shields.io/badge/status-in%20progress-111111?style=flat-square)
![Platform](https://img.shields.io/badge/platform-Raspberry%20Pi%20Zero%202%20W-111111?style=flat-square)
![Language](https://img.shields.io/badge/language-Python%203-111111?style=flat-square)
![Audio](https://img.shields.io/badge/audio-Spotify%20Connect-111111?style=flat-square)

---

## Overview

The goal is to build a compact, tactile desktop audio unit that streams directly over Wi-Fi without relying on Bluetooth tethering or local MP3 storage. Every hardware decision, wiring mistake, and software trade-off is recorded chronologically in the engineering log.

### System Architecture

```mermaid
flowchart LR
    Phone[Spotify App] -->|Spotify Connect / Wi-Fi| Pi[Raspberry Pi Zero 2 W]
    Pi -->|USB OTG| DAC[USB Audio Adapter]
    DAC -->|3.5mm Analog| Speaker[Desktop Speaker]
    Pi -->|I2C| OLED[0.96 in OLED Display]
    Encoder[KY-040 Rotary Encoder] -->|GPIO Interrupts| Pi
```
