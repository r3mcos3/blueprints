# 🔄 Update Notifications (Telegram)

[![version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)
[![Platform](https://img.shields.io/badge/Platform-Telegram-blue.svg)](https://telegram.org/)

Get notified about Home Assistant updates via Telegram! Receive notifications when updates are available for core, addons, or integrations with inline keyboard buttons to install, skip, or view changelogs directly from the message. 🚀

## ✨ Features

- 💬 **Telegram Notifications** - Get notified via Telegram Bot
- 🔔 **Update Alerts** - Get notified when new updates are available
- 🎛️ **Inline Keyboard Buttons** - Install, skip, or view changelog directly from messages
- 📋 **Changelog Button** - Quick access to release notes (when available)
- ✅ **Completion Notifications** - Know when updates finish installing
- ⏳ **Progress Updates** - See when updates start
- 🔁 **Periodic Reminders** - Configurable reminders for pending updates (5min - 24h intervals)
- 🏠 **HA Notifications** - Optional persistent notifications in Home Assistant
- ⚙️ **Config Check** - Automatically run config check before core updates
- 💾 **Backup Support** - Option to create backup before updating
- 💬 **Instant Feedback** - Immediate responses when buttons are pressed

## 📋 Requirements

Before using this blueprint, you need:

1. **Telegram Bot** - Create a bot via [@BotFather](https://t.me/botfather)
2. **Telegram Integration** - Set up in Home Assistant
3. **Chat ID** - Your Telegram user or group chat ID
4. **Update Entities** - The update entities you want to monitor

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

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Ftelegram_update_notifications%2Ftelegram_update_notifications.yaml)

### Manual Installation

1. In Home Assistant, navigate to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click the **Import Blueprint** button
3. Enter the blueprint URL:
   ```
   https://github.com/r3mcos3/blueprints/blob/main/telegram_update_notifications/telegram_update_notifications.yaml
   ```
4. Click **Preview** and then **Import**

## ⚙️ Configuration

### Main Settings

| Parameter | Description | Required |
|-----------|-------------|----------|
| 🔄 Update Entities | Update entities to monitor | Yes |

### 💬 Notification Settings (Collapsed)

| Parameter | Description | Default | Example |
|-----------|-------------|---------|---------|
| 💬 Telegram Notify Service | Name of your Telegram notify service | - | `telegram` |
| 💬 Telegram Chat ID | Your Telegram chat ID | - | `123456789` |
| 🏠 Send to HA | Also send persistent notifications in HA | false | - |

### ⏰ Reminder Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| ⏰ Reminder Interval | Time between reminders (5min to 24h or disabled) | 3 hours |
| 🌅 Only After | Only send notifications after this time | 07:00 |
| 🌙 Only Before | Only send notifications before this time | 22:00 |

**Available reminder intervals:**
- Every 5 minutes (testing)
- Every 15 minutes (testing)
- Every 30 minutes (testing)
- Every 1, 2, 3, 6, 12, or 24 hours

### 🔧 Advanced Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 💾 Take Backup | Create backup before updating | true |
| ✅ Run Config Check | Run config check for core updates | false |
| 📋 Custom Changelog URLs | Custom URLs for entities without changelogs | {} |

## 🎛️ Inline Keyboard Buttons

The blueprint includes built-in callback handling for inline keyboard buttons. When you press a button in Telegram:

- ✅ **Install** - Starts the update with optional backup (configured in Advanced Settings)
- ⏭️ **Skip** - Skips the current version of the update
- 📋 **Changelog** - Opens the release notes URL (only shown when available)

**Features:**
- Instant feedback when buttons are pressed
- Error messages if update is no longer available
- Buttons work for all notification types (new, reminder, config check)

## 💡 Usage Examples

### Example 1: Monitor All Updates

```yaml
automation:
  - alias: "All Update Notifications"
    use_blueprint:
      path: r3mcos3/telegram_update_notifications
      input:
        update_entities:
          - update.home_assistant_core_update
          - update.home_assistant_operating_system_update
          - update.home_assistant_supervisor_update
        telegram_notify_service: "telegram"
        telegram_chat_id: "123456789"
        reminder_hours: "6"
```

### Example 2: Core Updates Only with Config Check

```yaml
automation:
  - alias: "Core Update Notifications"
    use_blueprint:
      path: r3mcos3/telegram_update_notifications
      input:
        update_entities:
          - update.home_assistant_core_update
        telegram_notify_service: "telegram"
        telegram_chat_id: "123456789"
        run_config_check: true
        take_backup: true
```

### Example 3: Quick Testing with 5-Minute Reminders

```yaml
automation:
  - alias: "Test Update Notifications"
    use_blueprint:
      path: r3mcos3/telegram_update_notifications
      input:
        update_entities:
          - update.home_assistant_core_update
        telegram_notify_service: "telegram"
        telegram_chat_id: "123456789"
        reminder_hours: "0.083"  # 5 minutes
```

### Example 4: Custom Changelog URLs

For addons or integrations without built-in changelog URLs:

```yaml
automation:
  - alias: "Addon Updates with Custom Changelogs"
    use_blueprint:
      path: r3mcos3/telegram_update_notifications
      input:
        update_entities:
          - update.my_custom_addon
        telegram_notify_service: "telegram"
        telegram_chat_id: "123456789"
        changelog_urls:
          update.my_custom_addon: "https://github.com/user/addon/releases"
```

## 🔧 Troubleshooting

### Notifications Not Sending

1. Verify the Telegram bot token is correct in configuration.yaml
2. Check that your chat_id is correct
3. Ensure the time is within your configured notification window
4. Test the notify service: Developer Tools → Services → `notify.telegram`
5. Check Home Assistant logs for Telegram errors

### Buttons Not Working

1. Verify the `telegram_callback` event is being received in Developer Tools → Events
2. Ensure your bot has been started (send `/start` to your bot)
3. Check that the automation is enabled and not paused
4. Test with a simple update to verify button callbacks work

### Getting Your Chat ID

If you're not sure about your chat_id:

1. Send a message to your bot
2. Visit: `https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates`
3. Look for `"chat":{"id":123456789}` in the JSON response
4. Use that number as your chat_id

### Reminders Not Triggering

1. Verify reminder interval is not set to "Disabled"
2. Check that the current time is within your notification window
3. Ensure there are actually pending updates (state = "on")
4. For short intervals (5min), wait for the next matching minute

### Config Check Not Running

1. Ensure you've enabled "Run Config Check" in advanced settings
2. Verify the core update entity is included in your monitored entities
3. Make sure the Check Configuration addon is installed

### Changelog Button Not Appearing

1. The changelog button only appears when a `release_url` is available on the update entity
2. You can provide custom URLs via the "Custom Changelog URLs" setting in Advanced Settings
3. Some addons don't have changelog URLs available

## 📝 Version History

### Version 1.0.0 (2025-12-19)
- 🎉 Initial release
- 💬 Telegram notifications with inline keyboard
- 🎛️ Install, Skip, and Changelog buttons
- 🔁 Configurable reminders (5min-24h)
- ⚙️ Config check support
- 💾 Backup support before updates
- 📋 Custom changelog URL support
- 💬 Instant feedback on button presses

## ❓ FAQ

**Q: Can I use this with multiple Telegram chats?**
A: Currently, the blueprint supports one chat_id at a time. You can create multiple automations with the same blueprint for different chats.

**Q: Why don't I see the changelog button?**
A: The changelog button only appears when the update entity has a `release_url` attribute or you've configured a custom URL.

**Q: Can I test the notifications quickly?**
A: Yes! Use the "Every 5 minutes (testing)" reminder interval to get quick test notifications. Don't forget to change it back to a longer interval after testing.

**Q: What's the difference between this and the Mobile App version?**
A: This version uses Telegram Bot API with inline keyboard buttons, while the Mobile App version uses Android notification actions. Choose based on your preferred notification platform.

## 🤝 Contributing

Found a bug or have a suggestion? Please [open an issue](https://github.com/r3mcos3/blueprints/issues) on GitHub!

## 📄 License

This blueprint is provided as-is under the MIT License.

## 🙏 Credits

Created by [r3mcos3](https://github.com/r3mcos3)
