# 🏡 Home Assistant Blueprints

Welcome to the Home Assistant Blueprints repository! This repository contains a collection of useful and community-driven blueprints for Home Assistant, designed to simplify the automation of your smart home.

## What are Home Assistant Blueprints?

Blueprints are a way to share and reuse automations, scripts, and other configurations in Home Assistant. They allow you to import pre-configured setups and easily adapt them to your specific needs without writing complex YAML code from scratch.

## 🚀 Usage

To use a blueprint from this repository:

1.  Navigate to **Settings** -> **Automations & Scenes** -> **Blueprints** in your Home Assistant UI.
2.  Click on the **"Import Blueprint"** button.
3.  Enter the URL of the blueprint you wish to import. To get the correct URL, navigate to the blueprint file on GitHub, click the "Raw" button, and copy the URL from your browser's address bar. For example: `https://raw.githubusercontent.com/r3mcos3/blueprints/main/presence_lights/presence_lights.yaml`.
4.  Follow the on-screen prompts to configure the blueprint with your entities and settings.

For more detailed instructions, please refer to the official Home Assistant documentation on [Blueprints](https://www.home-assistant.io/docs/blueprint/).

## ✨ Available Blueprints

Currently, this repository offers the following blueprints:

| Blueprint | Description | Import |
|-----------|-------------|--------|
| 🚗 **[🚗 AI - Parking Spot Counter](ai_parking_counter/ai_parking_counter.yaml)** | v? - 📦 [Version 2.0.0] Analyzes camera feed with AI to count free and occupie... | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint/?blueprint_url=https://github.com/r3mcos3/blueprints/blob/main/ai_parking_counter/ai_parking_counter.yaml) |
| 🌤️ **[🤖 AI Weather Report Generator](ai_weather_report/ai_weather_report.yaml)** | v? - Fetches weather forecasts at regular intervals, uses AI to create an emo... | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint/?blueprint_url=https://github.com/r3mcos3/blueprints/blob/main/ai_weather_report/ai_weather_report.yaml) |
| 🏠 **[☀️ Sun Notifications](sun_notifications/sun_notifications.yaml)** | v? - 🌅 Get notified at sunrise and sunset via Telegram. Version 1.1.2 | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint/?blueprint_url=https://github.com/r3mcos3/blueprints/blob/main/sun_notifications/sun_notifications.yaml) |
| 🏠 **[📸 Camera Snapshot on Motion to Telegram 🤖](camera_motion_snapshot/camera_motion_snapshot.yaml)** | v? - 🚀 Automatically capture a snapshot from your camera 📷 when motion is det... | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint/?blueprint_url=https://github.com/r3mcos3/blueprints/blob/main/camera_motion_snapshot/camera_motion_snapshot.yaml) |
| 🏠 **[✨💡 Sun-aware Motion Light Control 🏃‍♂️☀️](sun_aware_motion_light/sun_aware_motion_light.yaml)** | v? - 💡 Smart Light Control for Motion 🏃‍♂️. Turns on a light with adjustable ... | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint/?blueprint_url=https://github.com/r3mcos3/blueprints/blob/main/sun_aware_motion_light/sun_aware_motion_light.yaml) |
| 💡 **[💡 Presence - Home/Away Lights](presence_lights/presence_lights.yaml)** | v? - 📦 [Version 1.0.13] Turns on specified lights when someone arrives home a... | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint/?blueprint_url=https://github.com/r3mcos3/blueprints/blob/main/presence_lights/presence_lights.yaml) |
| 🏠 **[🔄 Update Notifications](update_notifications/update_notifications.yaml)** | v? - 📦 [Version 2.6.0] Get notified about Home Assistant updates via Mobile A... | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint/?blueprint_url=https://github.com/r3mcos3/blueprints/blob/main/update_notifications/update_notifications.yaml) |
| 🔔 **[🔔 Doorbell Chime](doorbell_chime/doorbell_chime.yaml)** | v? - Play a chime sound on your media players when the doorbell rings! 🔔


🔊 ... | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint/?blueprint_url=https://github.com/r3mcos3/blueprints/blob/main/doorbell_chime/doorbell_chime.yaml) |
| 🏠 **[⏰ Alarm Light](alarm_light/alarm_light.yaml)** | v? - 📦 [Version 1.0.0] Turn on lights before your alarm goes off for a gentle... | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint/?blueprint_url=https://github.com/r3mcos3/blueprints/blob/main/alarm_light/alarm_light.yaml) |
| 🏠 **[🔥 Smart Heating Controller](smart_heating/smart_heating.yaml)** | v? - Intelligent climate control with presence detection, door/window protect... | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint/?blueprint_url=https://github.com/r3mcos3/blueprints/blob/main/smart_heating/smart_heating.yaml) |
| 🔈 **[🔈 Volume Control!](volumecontrol/volumecontrol.yaml)** | v? - Blueprint to automate all your speakers 🔈

📦 Version: 1.0 | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint/?blueprint_url=https://github.com/r3mcos3/blueprints/blob/main/volumecontrol/volumecontrol.yaml) |
| 🏠 **[📱 Telegram Update Notifications](telegram_update_notifications/telegram_update_notifications.yaml)** | v? - 📦 [Version 1.3.0] Get notified about Home Assistant updates via Telegram... | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint/?blueprint_url=https://github.com/r3mcos3/blueprints/blob/main/telegram_update_notifications/telegram_update_notifications.yaml) |

## 🤝 Contributing

We welcome contributions! If you have a useful Home Assistant blueprint that you'd like to share, please consider submitting a Pull Request. Before contributing, please ensure your blueprint adheres to Home Assistant's best practices and includes clear documentation.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
