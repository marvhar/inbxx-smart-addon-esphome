# ⚠️ BETA – first untested version – for selected beta testers only

> **Caution:** This is an early, **untested** release of the firmware. It controls a
> **heater** – faults in the software or configuration can cause overheating or damage.
> Install it **only if you were invited as a beta tester**, never leave the device
> unattended during the beta phase, and make sure a **hardware thermal cut-off**
> (e.g. KSD9700 70 °C) is installed in the heater supply.
> **Use of this firmware is entirely at your own risk**
> Please report any problems via
> [GitHub Issues](https://github.com/marvhar/inbxx-smart-addon-esphome/issues).

# INBXX Smart Add-on

ESPHome firmware for the **INBXX Heated Semi-smart add-on**: heater and fan control,
humidity hold, filament drying with timer, door detection, safety monitoring and
status display – fully integrated into Home Assistant.

# Installation

1. Connect the Arduino Nano ESP32 via USB.
2. Click the button below (Chrome or Edge on a desktop computer) and follow the steps.
3. Set up WiFi – choose one of these ways:
   - **USB:** enter your WiFi credentials directly in the installer right after flashing.
   - **Bluetooth (Improv BLE):** Home Assistant shows the device under
     *Settings → Devices & services → Discovered* (requires a Bluetooth adapter or
     Bluetooth proxy in range). The companion app or
     [improv-wifi.com](https://www.improv-wifi.com) work as well.
   - **Hotspot:** connect to the WiFi network `inbxx-smart-addon-xxxxxx` and enter
     your credentials in the page that opens.
4. Home Assistant discovers the device automatically.

<esp-web-install-button manifest="firmware/inbxx-smart-addon.manifest.json"></esp-web-install-button>

<script type="module" src="https://unpkg.com/esp-web-tools@10/dist/web/install-button.js?module"></script>

# Updates

New releases appear in Home Assistant as a firmware update of the device –
just press **Install**. Your settings (profiles, setpoints, dry time, …) are kept.
