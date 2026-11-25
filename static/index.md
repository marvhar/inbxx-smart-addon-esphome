# INBXX Smart Add-on

ESPHome firmware for the **INBXX Heated Semi-smart add-on**: heater and fan control,
humidity hold, filament drying with timer, door detection, safety monitoring and
status display – fully integrated into Home Assistant.

# Installation

1. Connect the Arduino Nano ESP32 via USB.
2. Click the button below (Chrome or Edge on a desktop computer) and follow the steps.
3. After flashing you can enter your WiFi credentials directly in the installer.
   Alternatively the device opens a hotspot named `inbxx-smart-addon-xxxxxx` –
   connect to it and enter your WiFi in the page that opens.
4. Home Assistant discovers the device automatically.

<esp-web-install-button manifest="firmware/inbxx-smart-addon.manifest.json"></esp-web-install-button>

<script type="module" src="https://unpkg.com/esp-web-tools@10/dist/web/install-button.js?module"></script>

# Updates

New releases appear in Home Assistant as a firmware update of the device –
just press **Install**. Your settings (profiles, setpoints, dry time, …) are kept.
