# ☀️ Sun Notifications

[![version](https://img.shields.io/badge/version-1.1.2-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

Get notified at sunrise and sunset via Telegram! Stay informed about the day-night cycle with customizable notifications and time offsets. Perfect for planning outdoor activities or automating home routines! 🌅

## ✨ Features

- 🌅 **Sunrise Notifications** - Get notified when the sun rises
- 🌇 **Sunset Notifications** - Get notified when the sun sets
- ⏰ **Time Offsets** - Set notifications before or after sunrise/sunset
- 💬 **Custom Messages** - Personalize your notification messages with templates
- 🔔 **Telegram Integration** - Receive notifications via Telegram Bot
- ⚙️ **Independent Control** - Enable/disable sunrise and sunset notifications separately
- 🌍 **Automatic Calculation** - Uses your Home Assistant location for accurate times

## 📋 Requirements

Before using this blueprint, you need:

1. **Telegram Bot** - Create a bot via [@BotFather](https://t.me/botfather)
2. **Telegram Integration** - Set up in Home Assistant
3. **Sun Integration** - Built-in Home Assistant sun integration (automatically available)

### Setting Up Telegram Bot

1. Open Telegram and search for [@BotFather](https://t.me/botfather)
2. Send `/newbot` and follow the instructions
3. Save the **Bot Token** you receive
4. Get your **Chat ID**:
   - Send a message to your bot
   - Visit: `https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates`
   - Find your chat_id in the response

### Configure Telegram in Home Assistant

Add to your `configuration.yaml`:

```yaml
telegram_bot:
  - platform: polling
    api_key: YOUR_BOT_TOKEN
    allowed_chat_ids:
      - YOUR_CHAT_ID

notify:
  - platform: telegram
    name: telegram
    chat_id: YOUR_CHAT_ID
```

## 🚀 Installation

### Automatic Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fsun_notifications%2Fsun_notifications.yaml)

### Manual Installation

1. In Home Assistant, navigate to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click the **Import Blueprint** button
3. Enter the blueprint URL:
   ```
   https://github.com/r3mcos3/blueprints/blob/main/sun_notifications/sun_notifications.yaml
   ```
4. Click **Preview** and then **Import**

## ⚙️ Configuration

When creating an automation from this blueprint, you'll configure:

| Parameter | Description | Default |
|-----------|-------------|---------|
| 📱 Telegram Bot | Telegram Bot integration for notifications | Required |
| 🌅 Enable Sunrise Notification | Toggle sunrise notifications on/off | Enabled |
| ⏰ Sunrise Offset | Time before (-) or after (+) sunrise | 00:00:00 |
| 💬 Sunrise Message | Custom message for sunrise (supports templates) | "De zon komt op ☀️" |
| 🌇 Enable Sunset Notification | Toggle sunset notifications on/off | Enabled |
| ⏰ Sunset Offset | Time before (-) or after (+) sunset | 00:00:00 |
| 💬 Sunset Message | Custom message for sunset (supports templates) | "De zon gaat onder 🌃" |

### Offset Examples

- `-00:30:00` = 30 minutes before
- `00:00:00` = Exactly at sunrise/sunset
- `00:15:00` = 15 minutes after

## 💡 Usage Examples

### Example 1: Basic Sunrise/Sunset Notifications

Simple setup with default messages:

```yaml
automation:
  - alias: "Sun Notifications"
    use_blueprint:
      path: r3mcos3/sun_notifications
      input:
        notification_target: <your_telegram_bot_config_entry>
        sunrise_enabled: true
        sunset_enabled: true
```

**Expected Behavior:**
- Notification at exact sunrise: "De zon komt op ☀️"
- Notification at exact sunset: "De zon gaat onder 🌃"

### Example 2: Morning Reminder Before Sunrise

Get notified before sunrise to prepare:

```yaml
automation:
  - alias: "Morning Sunrise Reminder"
    use_blueprint:
      path: r3mcos3/sun_notifications
      input:
        notification_target: <your_telegram_bot_config_entry>
        sunrise_enabled: true
        sunrise_offset: "-00:30:00"
        sunrise_message: "🌅 The sun rises in 30 minutes! Time to wake up!"
        sunset_enabled: false
```

**Expected Behavior:**
- Notification 30 minutes before sunrise
- No sunset notifications

### Example 3: Evening Automation Trigger

Get notified after sunset for evening routines:

```yaml
automation:
  - alias: "Evening Sunset Alert"
    use_blueprint:
      path: r3mcos3/sun_notifications
      input:
        notification_target: <your_telegram_bot_config_entry>
        sunrise_enabled: false
        sunset_enabled: true
        sunset_offset: "00:15:00"
        sunset_message: "🌃 It's getting dark outside. Time to close the curtains!"
```

**Expected Behavior:**
- No sunrise notifications
- Notification 15 minutes after sunset

### Example 4: Custom Messages with Templates

Dynamic messages with time information:

```yaml
automation:
  - alias: "Smart Sun Notifications"
    use_blueprint:
      path: r3mcos3/sun_notifications
      input:
        notification_target: <your_telegram_bot_config_entry>
        sunrise_enabled: true
        sunrise_message: "🌅 Good morning! Sunrise at {{ state_attr('sun.sun', 'next_rising') | as_timestamp | timestamp_custom('%H:%M') }}"
        sunset_enabled: true
        sunset_message: "🌇 Sunset at {{ state_attr('sun.sun', 'next_setting') | as_timestamp | timestamp_custom('%H:%M') }}. Enjoy your evening!"
```

**Expected Behavior:**
- Sunrise notification with actual sunrise time
- Sunset notification with actual sunset time

### Example 5: Photography Golden Hour Alerts

Get notified for perfect photography lighting:

```yaml
automation:
  - alias: "Golden Hour Alerts"
    use_blueprint:
      path: r3mcos3/sun_notifications
      input:
        notification_target: <your_telegram_bot_config_entry>
        sunrise_enabled: true
        sunrise_offset: "-00:45:00"
        sunrise_message: "📷 Golden hour starting soon! Perfect time for morning photography!"
        sunset_enabled: true
        sunset_offset: "-01:00:00"
        sunset_message: "📸 Golden hour alert! Best light for sunset photography in 1 hour!"
```

**Expected Behavior:**
- Morning alert 45 minutes before sunrise
- Evening alert 1 hour before sunset

## 🔧 Troubleshooting

### Notifications Not Sending

1. Verify Telegram bot is configured correctly in `configuration.yaml`
2. Check that the Telegram Bot config entry is selected in blueprint
3. Test the Telegram notification: Developer Tools → Services → `telegram_bot.send_message`
4. Ensure your bot has been started (send `/start` to your bot)
5. Check Home Assistant logs for Telegram errors

### Wrong Notification Time

1. Verify Home Assistant location is set correctly: Settings → System → General
2. Check timezone configuration in Settings → System → General
3. Test sun times in Developer Tools → States → `sun.sun`
4. Verify offset format is correct (HH:MM:SS)
5. Remember: negative offset = before, positive = after

### Sun Integration Not Working

1. Ensure `sun.sun` entity exists in Developer Tools → States
2. Verify Home Assistant has correct latitude and longitude configured
3. Check that timezone is set properly
4. Restart Home Assistant if sun integration was just configured

### Messages Not Customizing

1. Check that message text is entered correctly in blueprint configuration
2. Verify template syntax if using Jinja2 templates
3. Test templates in Developer Tools → Template
4. Ensure quotes are properly escaped in messages

### Only One Notification Working

1. Check both "Enable Sunrise" and "Enable Sunset" toggles
2. Verify that disabled notification is intentional
3. Check automation traces to see which triggers are firing
4. Ensure both messages are configured

## 📝 Version History

### Version 1.1.2 (2025-12-18)
- 📱 Updated to use Telegram Bot config_entry selector
- 🔧 Improved Telegram integration compatibility

### Version 1.1.1
- 🐛 Bug fixes and improvements

### Version 1.1.0
- ✨ Added independent enable/disable toggles for sunrise and sunset
- 💬 Enhanced message customization

### Version 1.0.0
- 🎉 Initial release
- 🌅 Sunrise notifications
- 🌇 Sunset notifications
- ⏰ Time offset support
- 💬 Custom messages with template support

## 🤝 Contributing

Found a bug or have a suggestion? Please [open an issue](https://github.com/r3mcos3/blueprints/issues) on GitHub!

## 📄 License

This blueprint is provided as-is under the MIT License.

## 🙏 Credits

Created by [r3mcos3](https://github.com/r3mcos3)
