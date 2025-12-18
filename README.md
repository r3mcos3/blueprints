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
| 🚗 **[Ai Parking Counter](ai_parking_counter/)** | 📦 [Version 2.0.0] Analyzes camera feed with AI to count free and occupied par | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fai_parking_counter%2Fai_parking_counter.yaml) |
| 🌤️ **[Ai Weather Report](ai_weather_report/)** | Fetches weather forecasts at regular intervals, uses AI to create an emoji-rich | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fai_weather_report%2Fai_weather_report.yaml) |
| 🏠 **[Alarm Light](alarm_light/)** | 📦 [Version 1.0.0] Turn on lights before your alarm goes off for a gentle | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Falarm_light%2Falarm_light.yaml) |
| 🔔 **[Doorbell Chime](doorbell_chime/)** | Play a chime sound on your media players when the doorbell rings! 🔔 | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fdoorbell_chime%2Fdoorbell_chime.yaml) |
| 💡 **[Presence Lights](presence_lights/)** | "📦 [Version 1.0.13] Turns on specified lights when someone arrives home after | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fpresence_lights%2Fpresence_lights.yaml) |
| 🏠 **[Smart Heating](smart_heating/)** | Intelligent climate control with presence detection, door/window protection, | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fsmart_heating%2Fsmart_heating.yaml) |
| 🏠 **[Update Notifications](update_notifications/)** | 📦 [Version 2.0.0] Get notified about Home Assistant updates via Mobile App! | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fupdate_notifications%2Fupdate_notifications.yaml) |
| 🔈 **[Volumecontrol](volumecontrol/)** | Blueprint to automate all your speakers 🔈 | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fvolumecontrol%2Fvolumecontrol.yaml) |

## 🤝 Contributing

We welcome contributions! If you have a useful Home Assistant blueprint that you'd like to share, please consider submitting a Pull Request. Before contributing, please ensure your blueprint adheres to Home Assistant's best practices and includes clear documentation.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
