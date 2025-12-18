# 🔄 Update Notifications

[![version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

Get notified about Home Assistant updates via Telegram! Receive notifications when updates are available for core, addons, or integrations with actionable buttons to install or skip updates directly from the notification. 🚀

## ✨ Features

- 🔔 **Update Alerts** - Get notified when new updates are available
- ✅ **Completion Notifications** - Know when updates finish installing
- ⏳ **Progress Updates** - See when updates start
- 🔁 **Periodic Reminders** - Configurable reminders for pending updates
- 🏠 **HA Notifications** - Optional persistent notifications in Home Assistant
- ⚙️ **Config Check** - Automatically run config check before core updates
- 💾 **Backup Support** - Option to create backup before updating
- 📋 **Changelog Links** - Quick access to release notes
- 🎛️ **Inline Actions** - Install or skip updates directly from Telegram

## 📋 Requirements

Before using this blueprint, you need:

1. **Telegram Bot Integration** - A configured Telegram bot in Home Assistant
2. **Update Entities** - The update entities you want to monitor (core, addons, integrations)

### Setting Up Telegram Bot

1. Create a bot via [@BotFather](https://t.me/botfather) on Telegram
2. Add the [Telegram Bot integration](https://www.home-assistant.io/integrations/telegram_bot/) to Home Assistant
3. Configure your chat ID and bot token

## 🚀 Installation

### Automatic Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fupdate_notifications%2Fupdate_notifications.yaml)

### Manual Installation

1. In Home Assistant, navigate to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click the **Import Blueprint** button
3. Enter the blueprint URL:
   ```
   https://github.com/r3mcos3/blueprints/blob/main/update_notifications/update_notifications.yaml
   ```
4. Click **Preview** and then **Import**

## ⚙️ Configuration

### Main Settings

| Parameter | Description | Required |
|-----------|-------------|----------|
| 🔄 Update Entities | Update entities to monitor | Yes |

### 📱 Notification Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 📱 Telegram Bot | Telegram bot for notifications | - |
| 🏠 Send to HA | Also send persistent notifications in HA | false |

### ⏰ Reminder Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| ⏰ Reminder Interval | Hours between reminders (or disabled) | 3 hours |
| 🌅 Only After | Only send notifications after this time | 07:00 |
| 🌙 Only Before | Only send notifications before this time | 22:00 |

### 🔧 Advanced Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 💾 Take Backup | Create backup before updating | true |
| ✅ Run Config Check | Run config check for core updates | false |
| 📋 Custom Changelog URLs | Custom URLs for entities without changelogs | {} |

## 🎛️ Telegram Callback Actions

The blueprint sends notifications with inline keyboard buttons. To make these buttons work, you need to create a separate automation to handle the callbacks:

### Install Update Handler

```yaml
automation:
  - alias: "Handle Telegram Install Update"
    trigger:
      - platform: event
        event_type: telegram_callback
        event_data:
          command: "/install_update"
    action:
      - action: telegram_bot.answer_callback_query
        data:
          callback_query_id: "{{ trigger.event.data.id }}"
          message: "Starting update..."
      - action: update.install
        target:
          entity_id: "{{ trigger.event.data.args[0] }}"
        data:
          backup: true
```

### Skip Update Handler

```yaml
automation:
  - alias: "Handle Telegram Skip Update"
    trigger:
      - platform: event
        event_type: telegram_callback
        event_data:
          command: "/skip_update"
    action:
      - action: telegram_bot.answer_callback_query
        data:
          callback_query_id: "{{ trigger.event.data.id }}"
          message: "Update skipped"
      - action: update.skip
        target:
          entity_id: "{{ trigger.event.data.args[0] }}"
```

## 💡 Usage Examples

### Example 1: Monitor All Updates

```yaml
automation:
  - alias: "All Update Notifications"
    use_blueprint:
      path: r3mcos3/update_notifications
      input:
        update_entities:
          - update.home_assistant_core_update
          - update.home_assistant_operating_system_update
          - update.home_assistant_supervisor_update
        telegram_bot: <your_telegram_bot_config_entry>
        reminder_hours: "6"
```

### Example 2: Core Updates Only with Config Check

```yaml
automation:
  - alias: "Core Update Notifications"
    use_blueprint:
      path: r3mcos3/update_notifications
      input:
        update_entities:
          - update.home_assistant_core_update
        telegram_bot: <your_telegram_bot_config_entry>
        run_config_check: true
        take_backup: true
```

### Example 3: Custom Changelog URLs

For addons or integrations without built-in changelog URLs:

```yaml
automation:
  - alias: "Addon Updates with Custom Changelogs"
    use_blueprint:
      path: r3mcos3/update_notifications
      input:
        update_entities:
          - update.my_custom_addon
        telegram_bot: <your_telegram_bot_config_entry>
        changelog_urls:
          update.my_custom_addon: "https://github.com/user/addon/releases"
```

## 🔧 Troubleshooting

### Notifications Not Sending

1. Verify your Telegram bot is configured correctly
2. Check that you've selected the correct bot in the blueprint
3. Ensure the time is within your configured notification window
4. Check Home Assistant logs for errors

### Buttons Not Working

1. Make sure you've created the callback handler automations (see above)
2. Verify the `telegram_callback` event is being received
3. Check that the entity_id in the callback is correct

### Reminders Not Triggering

1. Verify reminder interval is not set to "Disabled"
2. Check that the current time is within your notification window
3. Ensure there are actually pending updates (state = "on")

### Config Check Not Running

1. Ensure you've enabled "Run Config Check" in advanced settings
2. Verify the core update entity is included in your monitored entities
3. Make sure the Check Configuration addon is installed

## 📝 Version History

### Version 1.0.0 (2025-12-18)
- 🎉 Initial release
- 📱 Telegram notifications for updates
- 🎛️ Inline keyboard for install/skip actions
- ⏰ Configurable reminder intervals
- 🏠 Optional HA persistent notifications
- ⚙️ Core config check support
- 💾 Pre-update backup option
- 📋 Custom changelog URL support

## 🤝 Contributing

Found a bug or have a suggestion? Please [open an issue](https://github.com/r3mcos3/blueprints/issues) on GitHub!

## 📄 License

This blueprint is provided as-is under the MIT License.

## 🙏 Credits

Created by [r3mcos3](https://github.com/r3mcos3)
