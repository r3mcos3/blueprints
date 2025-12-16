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
| 🚗 **[AI Parking Counter](ai_parking_counter/)** | Use AI to analyze camera feed and count free/occupied parking spaces | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fai_parking_counter%2Fai_parking_counter.yaml) |
| 🌤️ **[AI Weather Report](ai_weather_report/)** | Generate AI-powered weather reports with natural language | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fai_weather_report%2Fai_weather_report.yaml) |
| 🔔 **[Doorbell Chime](doorbell_chime/)** | Play a chime sound on media players when the doorbell rings | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fdoorbell_chime%2Fdoorbell_chime.yaml) |
| 💡 **[Presence Lights](presence_lights/)** | Automate lighting based on presence detection | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fpresence_lights%2Fpresence_lights.yaml) |
| 🔈 **[Volume Control](volumecontrol/)** | Schedule-based volume control for media players | [![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fvolumecontrol%2Fvolumecontrol.yaml) |

## 🤝 Contributing

We welcome contributions! If you have a useful Home Assistant blueprint that you'd like to share, please consider submitting a Pull Request. Before contributing, please ensure your blueprint adheres to Home Assistant's best practices and includes clear documentation.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
