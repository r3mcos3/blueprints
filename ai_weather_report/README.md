# 🤖 AI Weather Report Generator

[![version](https://img.shields.io/badge/version-1.1.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

This blueprint automatically fetches weather forecasts at regular intervals, uses AI to create an emoji-rich summary, and stores it in a text helper. Perfect for displaying on dashboards, sending in notifications, or using in other automations! ☀️🌧️⛈️

## ✨ Features

- 🌤️ **Flexible Weather Source** - Works with any Home Assistant weather integration
- ⏰ **Customizable Update Frequency** - Set updates from every hour to once per day
- 📊 **Hourly or Daily Forecasts** - Choose the forecast type that suits your needs
- 🌍 **Multi-Language Support** - Available in Dutch, English, German, French, and Spanish
- 📝 **Configurable Report Length** - Control the summary length from 50 to 255 characters
- 🛡️ **Safe Updates** - Keeps the previous report when there is no forecast or the AI returns nothing, and never exceeds the helper's maximum length
- 🧠 **AI-Powered Summaries** - Uses your AI integration to create natural, emoji-rich reports
- 💾 **Automatic Storage** - Saves the report to an input_text helper for easy access

## 📋 Requirements

Before using this blueprint, you need:

1. **Weather Integration** - Any Home Assistant weather integration (e.g., Met.no, OpenWeatherMap, AccuWeather)
2. **AI Task Integration** - The AI Task integration configured with a provider (e.g., OpenAI, Google Generative AI, Anthropic)
3. **Input Text Helper** - Create an input_text helper to store the generated weather report

### Setting Up the Input Text Helper

1. Go to **Settings** → **Devices & Services** → **Helpers**
2. Click **+ CREATE HELPER** → **Text**
3. Configure:
   - **Name**: AI Weather Report (or any name you prefer)
   - **Maximum length**: 255 (the maximum allowed by Home Assistant)
4. Click **Create**

## 🚀 Installation

### Automatic Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fai_weather_report%2Fai_weather_report.yaml)

### Manual Installation

1. In Home Assistant, navigate to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click the **Import Blueprint** button
3. Enter the blueprint URL:
   ```
   https://github.com/r3mcos3/blueprints/blob/main/ai_weather_report/ai_weather_report.yaml
   ```
4. Click **Preview** and then **Import**

## ⚙️ Configuration

When creating an automation from this blueprint, you'll configure:

| Parameter | Description | Default |
|-----------|-------------|---------|
| 🌤️ Weather Entity | Your weather integration entity | - |
| 📊 Forecast Type | Hourly or daily forecasts | Hourly |
| ⏰ Update Frequency | Every 1, 2, 3, 6 or 12 hours, or once per day at 06:00 | 6 hours |
| 🧠 AI Task Entity | Your AI Task integration entity | - |
| 📝 Report Length | Maximum characters (50-255, limited by input_text) | 150 |
| 🌍 Report Language | Language for the report | Dutch |
| 📄 Target Input Text Helper | Where to store the report | - |

## 💡 Usage Examples

### Example 1: Dashboard Card

Display the weather report on your dashboard using a Markdown card:

```yaml
type: markdown
content: >
  ## 🌤️ Weather Report

  {{ states('input_text.ai_weather_report') }}
```

### Example 2: Morning Notification

Combine with another automation to send the report as a notification:

```yaml
- action: notify.mobile_app
  data:
    title: "Today's Weather"
    message: "{{ states('input_text.ai_weather_report') }}"
```

### Example 3: Voice Assistant

Use the report with your voice assistant:

```yaml
- action: tts.speak
  data:
    entity_id: tts.google_translate
    message: "{{ states('input_text.ai_weather_report') }}"
```

## 🔧 Troubleshooting

### No Report Generated

1. Check that your AI Task integration is properly configured
2. Verify the weather entity is providing forecast data
3. Check Home Assistant logs for any errors

### Report Not Updating

1. Verify the update frequency is set correctly
2. Check that the automation is enabled
3. Look for any automation errors in the logs

### Report Too Long/Short

Adjust the **Report Length** parameter to your desired character count. Note that the AI may not always respect the exact length, but will try to stay close to it.

## Screenshot

<img width="778" height="805" alt="Screenshot 2025-12-23 194254" src="https://github.com/user-attachments/assets/68c3b054-228f-4209-ac9a-a5af826217f4" />


## 📝 Version History

### Version 1.1.0
- 🐛 Fixed: an AI answer longer than the helper's maximum length made `input_text.set_value` fail — the report is now cut to the helper's `max`
- 🐛 Fixed: without forecast data the AI invented a report; now the previous report is kept (also when the AI returns nothing)
- 🐛 Fixed: "Once per day" used `/24`, which is not a valid hour pattern — it now runs at 06:00
- 🔧 Only the next 24 hours (hourly) or 7 days (daily) are sent to the AI: smaller prompt, better summary
- 🔧 Prompts now ask for "at most N characters" and for the report text only
- 🔧 Fixed the import badge URL (wrong GitHub user) and the documented length range (50-255)
- 🔧 Modernized `filter` selectors

### Version 1.0.2 (2025-12-16)
- 🔧 Fix GitHub username in credits section

### Version 1.0.1 (2025-12-16)
- ⬆️ Update minimum Home Assistant version to 2025.12.0

### Version 1.0.0 (2025-12-16)
- 🎉 Initial release
- ✨ Support for hourly and daily forecasts
- 🌍 Multi-language support (Dutch, English, German, French, Spanish)
- ⚙️ Fully configurable parameters
- 📊 Emoji-rich AI-generated summaries

## 🤝 Contributing

Found a bug or have a suggestion? Please [open an issue](https://github.com/r3mcos3/blueprints/issues) on GitHub!

## 📄 License

This blueprint is provided as-is under the MIT License.

## 🙏 Credits

Created by [r3mcos3](https://github.com/r3mcos3)
