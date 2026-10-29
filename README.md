# Havells 9W TW+RGB Wi-Fi Bulb - ESPHome Configuration

This repository contains the ESPHome configuration for the **Havells 9W TW+RGB Wi-Fi Smart Bulb** (sold primarily in India), based on the Beken CB2L chipset.

This configuration provides a complete foundation for integrating the bulb locally into Home Assistant or any other smart home platform using ESPHome, completely bypassing the proprietary cloud apps. 

## Features

* **Beken CB2L Support:** Fully configured for the internal CB2L Wi-Fi module.
* **BP5758D LED Driver Calibration:** Pre-configured with specific channel mapping (RGB + Warm/Cold White).
* **Thermal Safety Capping:** The LED driver currents have been intentionally limited (12mA for RGB, 30mA for Whites) to match factory safety limits and prevent the bulb from overheating or melting over time.
* **Color Interlock:** Prevents the white and RGB LEDs from firing at maximum brightness simultaneously, reducing heat and power draw.
* **Custom Effects:** Includes built-in custom lambda effects like a smooth "Relaxing Rainbow".
* **Bluetooth Proxy (Optional):** Pre-written, commented-out blocks to easily enable ESPHome Bluetooth Proxy forwarding for extending your smart home's BLE reach.

## Hardware Reference

| Component / Pin | Value / Note | 
| ----- | ----- |
| **Board** | `cb2l` |
| **LED Driver** | `bp5758d` |
| **Clock Pin (CLK)** | `P6` |
| **Data Pin (DAT)** | `P7` |

**Channel Mapping (BP5758D):**
* Channel 1: Blue
* Channel 2: Green
* Channel 3: Red
* Channel 4: Warm White
* Channel 5: Cold White

## Prerequisites

1. An installed instance of [ESPHome](https://esphome.io/) (Dashboard or CLI).
2. A method to initially flash the Beken chip. Because this is a Tuya-based Beken device, you may be able to use cloud-cutting exploits (like [tuya-cloudcutter](https://github.com/tuya-cloudcutter/tuya-cloudcutter)), or you will need to open the bulb and flash it via serial using [ltchiptool](https://github.com/libretiny-eu/ltchiptool). 

## Installation

1. Clone or download this repository.
2. Copy the `havells_tw_rgb_9w_bulb.yaml` file into your ESPHome configuration directory.
3. Ensure you have a `secrets.yaml` file in the same directory. You will need to define the following secrets:

```yaml
# Example secrets.yaml
wifi_ssid: "Your_WiFi_SSID"
wifi_password: "Your_WiFi_Password"
ap_password: "Fallback_AP_Password"
api_key: "Your_Generated_API_Key"
ota_password: "Your_OTA_Password"
```

4. Compile and install the firmware. Future updates can be done easily via OTA.

## A Note on Brightness and Heat

Smart bulbs cram a power supply, a Wi-Fi chip, and bright LEDs into a very small, enclosed space. The current limits in this YAML (`current: 12` for RGB and `current: 30` for White) are specifically chosen to match the thermal limits of the physical hardware. **Do not arbitrarily increase these values** in an attempt to make the bulb brighter, as this can cause the LED driver to overheat, potentially melting the plastic casing or causing premature failure of the bulb.
