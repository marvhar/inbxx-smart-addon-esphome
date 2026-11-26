# ⚠️ BETA – first untested version – for selected beta testers only

> [!CAUTION]
> This is an early, **untested** release of the firmware. It controls a **heater** –
> faults in the software or configuration can cause overheating or damage.
> Use it **only if you were invited as a beta tester**, never leave the device
> unattended during the beta phase, and make sure a **hardware thermal cut-off**
> (e.g. KSD9700 70 °C) is installed in the heater supply.
> Please report any problems via [GitHub Issues](https://github.com/marvhar/inbxx-smart-addon-esphome/issues).

# INBXX Smart Add-on – ESPHome firmware

ESPHome firmware for the **INBXX Heated Semi-smart Advanced add-on** (Arduino Nano ESP32).

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
- **WS2811 LED strip** – status light (standby / printing / finished / door / error)
  plus a freely usable extended light; LED count per segment adjustable at runtime
- **Managed updates** – new releases appear as an update in Home Assistant

## Installation

Open the install page and flash via USB from the browser:
**https://marvhar.github.io/inbxx-smart-addon-esphome/**

### WiFi setup

A freshly flashed device has no WiFi credentials. Choose one of these ways:

- **USB (Improv Serial)** – enter your WiFi directly in the install page right after flashing.
- **Bluetooth (Improv BLE)** – Home Assistant shows the device under
  *Settings → Devices & services → Discovered* (requires a Bluetooth adapter or
  Bluetooth proxy in range). The Home Assistant companion app or
  [improv-wifi.com](https://www.improv-wifi.com) work as well.
- **Hotspot (captive portal)** – connect to the WiFi network
  `inbxx-smart-addon-xxxxxx` and enter your credentials in the page that opens.

Once connected, Home Assistant discovers the device automatically.

## Home Assistant entities

All entities the device provides in Home Assistant (control, sensors, settings,
lighting, diagnostics) are explained in the
[Wiki](https://github.com/marvhar/inbxx-smart-addon-esphome/wiki).

## LED strip

One WS2811 strip on GPIO47 is split into two optional segments, wired in series:

| Segment | Entity in Home Assistant | Purpose                                   | LEDs set by           |
|---------|--------------------------|-------------------------------------------|-----------------------|
| 1       | `Light`                  | Status (standby, printing, finished, door, error) | `Status LED Count`    |
| 2       | `Extended Light`         | Free to use (e.g. chamber lighting)       | `Extended LED Count`  |

Segment 1 starts at the first LED of the strip, segment 2 follows directly after it.
Set the counts to match your setup under *Settings → Devices & services → ESPHome →
INBXX Smart Add-on → Configuration* (or in the device's web UI). Changes apply
immediately, no reboot or new firmware needed. Use `0` for a segment that is not
installed. Together both segments can drive up to **60 LEDs** (defaults: 4 + 8).

> **Note:** size the power supply for your strip – a WS2811 LED draws up to ~60 mA
> at full white.

## Updates

The device checks for new releases every 6 hours. Home Assistant then shows a
firmware update for the device – press **Install**. Settings stored on the
device (profiles, setpoints, dry time, LED timeout, LED counts) are kept.

## Customizing

Adopt the device in the ESPHome dashboard to build your own firmware based on
[`inbxx-smart-addon.yaml`](inbxx-smart-addon.yaml). Limits and tuning values are
in the `substitutions` block (e.g. `NUM_LEDS_MAX` for strips with more than 60 LEDs). Note: once you build your own firmware, do not use
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
