# 🔄 Update Notifications

[![version](https://img.shields.io/badge/version-2.0.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

Get notified about Home Assistant updates via Mobile App! Receive notifications when updates are available for core, addons, or integrations with actionable buttons to install or skip updates directly from the notification. 🚀

## ✨ Features

- 📱 **Mobile Notifications** - Get notified on your iOS or Android device
- 🔔 **Update Alerts** - Get notified when new updates are available
- ✅ **Completion Notifications** - Know when updates finish installing
- ⏳ **Progress Updates** - See when updates start
- 🔁 **Periodic Reminders** - Configurable reminders for pending updates
- 🏠 **HA Notifications** - Optional persistent notifications in Home Assistant
- ⚙️ **Config Check** - Automatically run config check before core updates
- 💾 **Backup Support** - Option to create backup before updating
- 📋 **Changelog Links** - Quick access to release notes
- 🎛️ **Actionable Buttons** - Install or skip updates directly from notifications

## 📋 Requirements

Before using this blueprint, you need:

1. **Mobile App** - Home Assistant Companion App on iOS or Android
2. **Update Entities** - The update entities you want to monitor (core, addons, integrations)

### Setting Up Mobile App

1. Install the [Home Assistant Companion App](https://companion.home-assistant.io/) on your device
2. Sign in and connect to your Home Assistant instance
3. The mobile device will automatically appear in the blueprint selector

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
| 📱 Mobile Device | Mobile device(s) for notifications | - |
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

## 🎛️ Actionable Notifications

The blueprint includes built-in callback handling for actionable buttons. When you press a button:

- ✅ **Install** - Starts the update with optional backup (configured in Advanced Settings)
- ⏭️ **Skip** - Skips the current version of the update

Features:
- Notifications include actionable buttons for Install/Skip
- Tapping the notification opens the changelog or updates page
- Each update gets a unique notification tag for proper handling

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
        mobile_app_device:
          - <your_mobile_device_id>
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
        mobile_app_device:
          - <your_mobile_device_id>
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
        mobile_app_device:
          - <your_mobile_device_id>
        changelog_urls:
          update.my_custom_addon: "https://github.com/user/addon/releases"
```

## 🔧 Troubleshooting

### Notifications Not Sending

1. Verify the Companion App is connected and working
2. Check that you've selected the correct device in the blueprint
3. Ensure the time is within your configured notification window
4. Check Home Assistant logs for errors

### Buttons Not Working

1. Verify the Companion App is connected and working
2. Check that `mobile_app_notification_action` events are being received in Developer Tools → Events
3. Ensure the correct device is selected in the blueprint
4. Ensure the automation is enabled and not paused

### Reminders Not Triggering

1. Verify reminder interval is not set to "Disabled"
2. Check that the current time is within your notification window
3. Ensure there are actually pending updates (state = "on")

### Config Check Not Running

1. Ensure you've enabled "Run Config Check" in advanced settings
2. Verify the core update entity is included in your monitored entities
3. Make sure the Check Configuration addon is installed

## 📝 Version History

### Version 2.0.0 (2025-12-18)
- 📱 Simplified to Mobile App notifications only
- 🎛️ Actionable notifications with Install/Skip buttons
- 📱 Multiple mobile device support
- 🔄 Removed Telegram support for simplicity

### Version 1.2.0 (2025-12-18)
- 🎛️ Added inline keyboard buttons to reminder notifications
- 📋 Each pending update now has its own Install/Skip buttons

### Version 1.1.0 (2025-12-18)
- 🔄 Merged callback handler into main blueprint (single blueprint)
- 🎛️ Built-in handling for Install/Skip buttons

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
