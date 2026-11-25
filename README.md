# INBXX Smart Add-on – ESPHome firmware

ESPHome firmware for the **INBXX Heated Semi-smart add-on** (Arduino Nano ESP32).

## Features

- **Heater control** – PID on chamber temperature (SHT4x) with a predictive power
  limiter on the heater NTC (protects the KSD9700 bimetal switch)
- **Modes** – `Off`, `Auto` (printer coupling / humidity hold), `Dry` (with timer, 1–12 h)
- **3 profiles** – temperature + humidity, names editable in Home Assistant
- **Fan control** – follows the heater, NTC ramp, after-run, circulation
- **Door detection** – heating pauses while the door is open
- **Safety monitoring** – sensor timeouts/plausibility, over-temperature,
  heater max. time, heater without effect, heater stuck on (latched, must be acknowledged)
- **Display** (SH1107 128×128, LVGL) – main, setpoints, status and profile pages
- **Status LED** (WS2811) – standby / printing / finished / door / error
- **Managed updates** – new releases appear as an update in Home Assistant

## Installation

Open the install page and flash via USB from the browser:
**https://marvhar.github.io/inbxx-smart-addon-esphome/**

WiFi is set up in the installer or via the device hotspot (captive portal).
Home Assistant discovers the device automatically.

## Updates

The device checks for new releases every 6 hours. Home Assistant then shows a
firmware update for the device – press **Install**. Settings stored on the
device (profiles, setpoints, dry time, LED timeout) are kept.

## Customizing

Adopt the device in the ESPHome dashboard to build your own firmware based on
[`inbxx-smart-addon.yaml`](inbxx-smart-addon.yaml). Limits and tuning values are
in the `substitutions` block. Note: once you build your own firmware, do not use
the Home Assistant update entity – it would replace your build with the release.

## Hardware

| Function            | Pin (Nano ESP32) | GPIO   |
|---------------------|------------------|--------|
| Fan (PWM, MOSFET)   | D3               | GPIO6  |
| Button ACTION       | D6               | GPIO9  |
| Button PLUS         | D7               | GPIO10 |
| Button MINUS        | D8               | GPIO17 |
| Printer status      | D9               | GPIO18 |
| Heater (PWM, MOSFET)| D10              | GPIO21 |
| NTC 100k (10k up)   | A7               | GPIO14 |
| I²C SDA / SCL       | A4 / A5          | GPIO11 / GPIO12 |
| WS2811 LED strip    | –                | GPIO47 |

Printer status: `M262 P0 B0` (set as output), `M264 P0 B1` / `B0` (start / stop print).

> **Safety:** the software monitoring does not replace a thermal cut-off in the
> heater supply (e.g. KSD9700 70 °C).
