# 🔄 Update Notifications (Telegram)

[![version](https://img.shields.io/badge/version-1.4.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)
[![Platform](https://img.shields.io/badge/Platform-Telegram-blue.svg)](https://telegram.org/)

Get notified about Home Assistant updates via Telegram! Receive notifications when updates are available for core, addons, or integrations with inline keyboard buttons to install or skip updates directly from the message. 🚀

## ✨ Features

- 💬 **Telegram Notifications** - Get notified via Telegram Bot
- 🔔 **Update Alerts** - Get notified when new updates are available
- 🎛️ **Inline Keyboard Buttons** - Install or skip directly from messages
- 📋 **Changelog Link** - Quick access to release notes in the message (when available)
- ✅ **Completion Notifications** - Know when updates finish installing (skipping an update does not send one)
- ⏳ **Progress Updates** - See when updates start
- 🔁 **Periodic Reminders** - Configurable reminders for the pending updates you monitor (5min - 24h intervals)
- 🌙 **Quiet Hours** - Updates that appear outside the notification window are announced when the window opens
- 🏠 **HA Notifications** - Optional persistent notifications in Home Assistant
- ⚙️ **Config Check** - Automatically run config check before core updates
- 💾 **Backup Support** - Option to create backup before updating
- 💬 **Instant Feedback** - Immediate responses when buttons are pressed

## 📋 Requirements

Before using this blueprint, you need:

1. **Telegram Bot** - Create a bot via [@BotFather](https://t.me/botfather)
2. **Telegram bot integration** - Set up in Home Assistant (with your chat as an allowed chat)
3. **Update Entities** - The update entities you want to monitor

### Setting Up Telegram Bot

1. Open Telegram and search for [@BotFather](https://t.me/botfather)
2. Send `/newbot` and follow the instructions
3. Save the **Bot Token** you receive
4. Get your **Chat ID**:
   - Send a message to your bot
   - Visit: `https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates`
   - Find your chat_id in the response

### Configure Telegram in Home Assistant

1. Go to **Settings** → **Devices & Services** → **Add Integration** → **Telegram bot**
2. Enter your bot token and choose polling or webhooks
3. Add your chat ID as an allowed chat
4. Select this Telegram bot in the blueprint (*Telegram Bot* input)

See the [Telegram bot integration](https://www.home-assistant.io/integrations/telegram_bot/) for details.

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
| 📱 Telegram Bot | The Telegram bot integration used for all messages | - | *(pick from dropdown)* |
| 🏠 Send to HA | Also send persistent notifications in HA | false | - |

### ⏰ Reminder Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| ⏰ Reminder Interval | Time between reminders (5min to 24h or disabled) | 3 hours |
| 🌅 Only After | Only send notifications after this time (a new update outside the window is announced when it opens) | 07:00 |
| 🌙 Only Before | Only send notifications before this time | 22:00 |

**Available reminder intervals:**
- Every 5 minutes (testing)
- Every 15 minutes (testing)
- Every 30 minutes (testing)
- Every 1, 2, 3, 6, 12, or 24 hours

### 🔧 Advanced Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 💾 Take Backup | Create backup before updating (only for update entities that support backups) | true |
| ✅ Run Config Check | Run config check for core updates | false |
| 📋 Custom Changelog URLs | Custom URLs for entities without changelogs | {} |

## 🎛️ Inline Keyboard Buttons

The blueprint includes built-in callback handling for inline keyboard buttons. When you press a button in Telegram:

- ✅ **Install** - Starts the update with optional backup (configured in Advanced Settings)
- ⏭️ **Skip** - Skips the current version of the update

**Features:**
- Instant feedback when buttons are pressed
- Buttons only work for the update entities you monitor
- The changelog link is part of the message text (Telegram limits button data to 64 bytes, too short for most release URLs)
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
        telegram_bot_config: <your_telegram_bot_config_entry_id>
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
        telegram_bot_config: <your_telegram_bot_config_entry_id>
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
        telegram_bot_config: <your_telegram_bot_config_entry_id>
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
        telegram_bot_config: <your_telegram_bot_config_entry_id>
        changelog_urls:
          update.my_custom_addon: "https://github.com/user/addon/releases"
```

## 🔧 Troubleshooting

### Notifications Not Sending

1. Verify the Telegram bot integration is set up and the right bot is selected in the blueprint
2. Check that your chat is an allowed chat of the bot
3. Check your notification window (a new update outside the window is announced when the window opens)
4. Test the bot: Developer Tools → Actions → `telegram_bot.send_message`
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

### Changelog Link Not Appearing

1. The changelog link only appears when a `release_url` is available on the update entity
2. You can provide custom URLs via the "Custom Changelog URLs" setting in Advanced Settings
3. Some addons don't have changelog URLs available

## 📝 Version History

### Version 1.4.0
- 🐛 Fixed: the selected Telegram bot was never passed to the Telegram actions (`config_entry_id` was missing)
- 🐛 Fixed: pressing **Skip** triggered a "✅ Update Complete" message — the state also goes `on` → `off` for a skipped update
- 🐛 Fixed: names or release notes containing `_`, `*`, `` ` `` or `[` broke the Markdown message, so the notification was not delivered — they are now escaped
- 🐛 Fixed: the Changelog button put the release URL in Telegram's 64-byte `callback_data`; long URLs made the whole message fail. The changelog is now a link in the message text
- 🐛 Fixed: reminders listed *all* update entities instead of only the ones you selected
- 🐛 Fixed: an update that appeared outside the notification window was silently dropped (no persistent notification, no config check, no later notice when reminders are disabled). It is now announced when the window opens
- 🐛 Fixed: update entities without a device broke the "new update" notification
- 🐛 Fixed: install failed for update entities that do not support backups while "Take Backup" was on
- 🔒 Install/Skip buttons are only handled for monitored update entities
- 🧹 HA startup now dismisses the persistent notifications of *all* monitored updates that are no longer pending
- 🔧 A failing Telegram message no longer stops the persistent notification and config check
- 🔧 The "5 minutes (testing)" reminder rounds correctly; the reminder trigger is not registered when reminders are disabled
- 🔧 Modernized syntax (`triggers`, `trigger:`, `filter` selectors); README brought in line with the blueprint (it still described the old notify-service inputs)

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
A: Messages go to the default chat of the selected bot. Use a separate bot (integration entry) per chat, each with its own automation.

**Q: Why don't I see the changelog link?**
A: The changelog link only appears when the update entity has a `release_url` attribute or you've configured a custom URL.

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
