# 🛡️ Add-on Watchdog

[![version](https://img.shields.io/badge/version-1.1.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

Watches an entity and automatically restarts a Home Assistant add-on when it goes offline, and tells you what happened. Works for any add-on: Zigbee2MQTT, Mosquitto, Z-Wave JS, ESPHome, Matter Server, ... 🛡️

## ✨ Features

- 🔁 **Automatic restart** - Restarts the add-on when the monitored entity stays in the problem state
- ⏱️ **No false alarms** - The problem must last a configurable time (default 2 minutes) before the watchdog acts
- ⏳ **Patient** - Waits per attempt (default 3 minutes) and stops waiting as soon as the add-on is back
- 🔢 **Configurable attempts** - Default 2 restarts, adjustable from 1 to 10
- ✅ **Flexible recovery condition** - "State equals X" or "state is anything but X"
- 📱 **Notifications** - Problem started, attempt failed, recovered, or failed with the most likely cause (Telegram and/or Home Assistant)
- 🔍 **Diagnosis** - Optional checks on a related integration and the add-on update entity for a helpful "most likely cause"
- 🌍 **Multi-language** - English and Dutch
- 🧩 **Pick from a list** - Choose the add-on from your installed add-ons, no slug lookup needed
- 🔒 **Nothing hard-coded** - Add-on, entities and Telegram bot are all inputs

## 📋 Requirements

1. **Home Assistant OS or Supervised** - The `hassio.addon_restart` action needs the Supervisor
2. **An installed add-on** - Picked from a list, no need to look up the slug
3. **Monitored entity** - An entity that shows whether the add-on works
4. **Optional:** a Telegram bot integration for Telegram messages

## 🚀 Installation

[![Open your Home Assistant instance and show the blueprint import dialog.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Faddon_watchdog%2Faddon_watchdog.yaml)

## ⚙️ Configuration

| Input | Description |
|-------|-------------|
| Add-on | Pick the installed add-on to restart from a list |
| Monitored Entity | Entity that shows whether the add-on works |
| Service Name | Name in the messages (empty = entity name) |
| Problem State / Duration | State that means "down" and how long it must last |
| Recovery State / Condition | When the add-on counts as recovered (equals / not equals) |
| Maximum Attempts / Wait Time | Number of restarts and wait time after each restart |
| Telegram Bot / Send to HA / Language | Where and in which language to report |
| Related Integration / Add-on Update Entity | Optional diagnosis checks |

## 💡 Examples

| Use case | Add-on | Monitored entity | Problem | Recovery |
|----------|--------|------------------|---------|----------|
| Zigbee2MQTT | `<id>_zigbee2mqtt` | bridge connection state | `off` | equals `on` |
| Mosquitto (MQTT lost) | `core_mosquitto` | bridge connection state | `unavailable` | not equals `unavailable` |

## 📝 Changelog

- **1.1.0** - The add-on is now chosen from a list of installed add-ons (add-on selector) instead of typing the slug. The monitored entity selector is limited to useful domains (binary_sensor, sensor, switch, light, update)
- **1.0.0** - Initial release: generic add-on watchdog replacing separate Zigbee2MQTT and MQTT watchdog automations
