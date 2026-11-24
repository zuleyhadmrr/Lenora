# Log 001 — Architecture Trade-offs and Initial BOM

**Date:** 2026-11-24  
**Phase:** Phase 0 — Planning

## Problem Statement

Build a standalone desktop music player with physical controls and a small display, starting from zero electronics experience and minimal soldering overhead.

## Key Architectural Decisions

### 1. Streaming Protocol: Spotify Connect over YouTube Music / Bluetooth
- **YouTube Music** lacks an official developer API for embedded playback, forcing reliance on fragile unofficial scrapers.
- **Bluetooth** ties audio playback to the host device's proximity and battery.
- **Decision:** Use Spotify Connect (`librespot` / `raspotify`) over 2.4 GHz Wi-Fi so the device streams directly from the network once triggered.

### 2. Compute Platform: Raspberry Pi Zero 2 W over ESP32
- An **ESP32** offers lower cost and deeper bare-metal learning, but running unofficial Spotify Connect clients requires PSRAM-equipped variants, complex ESP-IDF builds, and external I2S DAC/amplifier circuitry.
- **Decision:** Start with a **Raspberry Pi Zero 2 W** running headless Raspberry Pi OS Lite. Audio output is handled via a plug-and-play USB audio adapter over OTG to isolate early hardware risk.

### 3. Solderless Prototyping Strategy
- Pre-soldered Zero 2 WH boards were out of stock locally; opted for a standard Zero 2 W paired with a standard 2x20 (2.54 mm) male header to be soldered once, keeping all subsequent peripheral wiring strictly jumper-based.

## Initial Bill of Materials (v1.0)

| Component | Specification | Purpose |
| :--- | :--- | :--- |
| Raspberry Pi Zero 2 W | Quad-core ARM, 2.4 GHz Wi-Fi | Main compute unit |
| GPIO Header | 2x20 Pin, 2.54 mm Male | Solderless jumper interface |
| MicroSD Card | 16 GB, Class 10 | OS and application storage |
| USB Audio Adapter | USB-A, UAC compliant | Analog 3.5 mm audio output |
| Micro-USB OTG Cable | Micro-USB Male to USB-A Female | Audio adapter bridge |
| OLED Display | 0.96 in, 128x64, I2C (SSD1306) | Track metadata and volume UI |
| Rotary Encoder | KY-040 Module (with push switch) | Tactile volume and playback control |
| Jumper Wires | Female-to-Female, 200 mm | Prototyping connections |

## Next Steps
- Provision MicroSD card using Raspberry Pi Imager with pre-configured 2.4 GHz hotspot credentials and SSH access.
- Verify headless SSH connection via VS Code Remote - SSH once hardware arrives.
