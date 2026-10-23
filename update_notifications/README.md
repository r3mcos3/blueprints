# 🔄 Update Notifications (Android)

[![version](https://img.shields.io/badge/version-2.7.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)
[![Platform](https://img.shields.io/badge/Platform-Android-green.svg)](https://www.android.com/)

Get notified about Home Assistant updates via Mobile App! Receive notifications when updates are available for core, addons, or integrations with actionable buttons to install, skip, or view changelogs directly from the notification. 🚀

> **⚠️ Platform Support:** This blueprint is specifically designed and tested for **Android devices only**. iOS support has not been tested and may not work as expected.

## ✨ Features

- 📱 **Android Notifications** - Get notified on your Android device via the Companion App
- 🔔 **Update Alerts** - Get notified when new updates are available
- 🎛️ **Actionable Buttons** - Install, skip, or view changelog directly from notifications
- 📋 **Changelog Button** - Quick access to release notes (when available)
- ✅ **Completion Notifications** - Know when updates finish installing (skipping an update just clears its notification)
- ⏳ **Progress Updates** - See when updates start
- 🔁 **Periodic Reminders** - Configurable reminders for the pending updates you monitor (5min - 24h intervals)
- 🌙 **Quiet Hours** - Updates that appear outside the notification window are announced as soon as the window opens (even with reminders disabled)
- 🏠 **HA Notifications** - Optional persistent notifications in Home Assistant
- ⚙️ **Config Check** - Automatically run config check before core updates
- 💾 **Backup Support** - Option to create backup before updating
- 🐛 **Debug Logging** - Built-in logging for troubleshooting callback issues

## 📋 Requirements

Before using this blueprint, you need:

1. **Android Device** - This blueprint is designed for Android only
2. **Mobile App** - Home Assistant Companion App for Android
3. **Update Entities** - The update entities you want to monitor (core, addons, integrations)

### Setting Up Mobile App

1. Install the [Home Assistant Companion App](https://companion.home-assistant.io/) on your Android device
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
| 📱 Mobile Device | Android device(s) for notifications | - |
| 🏠 Send to HA | Also send persistent notifications in HA | false |

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

## 🎛️ Actionable Notifications

The blueprint includes built-in callback handling for actionable buttons. When you press a button:

- ✅ **Install** - Starts the update with optional backup (configured in Advanced Settings)
- ⏭️ **Skip** - Skips the current version of the update
- 📋 **Changelog** - Opens the release notes URL (only shown when available)

**Features:**
- Android supports maximum 3 notification actions
- Each update gets a unique notification tag for proper handling
- Tapping the notification body opens the changelog or updates page
- Debug logging helps troubleshoot button callback issues

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
          - <your_android_device_id>
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
          - <your_android_device_id>
        run_config_check: true
        take_backup: true
```

### Example 3: Quick Testing with 5-Minute Reminders

```yaml
automation:
  - alias: "Test Update Notifications"
    use_blueprint:
      path: r3mcos3/update_notifications
      input:
        update_entities:
          - update.home_assistant_core_update
        mobile_app_device:
          - <your_android_device_id>
        reminder_hours: "0.083"  # 5 minutes
```

### Example 4: Custom Changelog URLs

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
          - <your_android_device_id>
        changelog_urls:
          update.my_custom_addon: "https://github.com/user/addon/releases"
```

## 🔧 Troubleshooting

### Notifications Not Sending

1. Verify the Companion App is connected and working on your Android device
2. Check that you've selected the correct device in the blueprint
3. Check your notification window (a new update outside the window is announced when the window opens, so you may simply have to wait)
4. Check Home Assistant logs for errors

### Buttons Not Working

1. Check the debug logs at `blueprints.update_notifications` for callback data
2. Verify that `mobile_app_notification_action` events are being received in Developer Tools → Events
3. Ensure the correct Android device is selected in the blueprint
4. Ensure the automation is enabled and not paused
5. Look for "Install callback received" or "Skip callback received" messages in logs

**Debug log example:**
```
Install callback received - Action: install_update, Raw tag: reminder_home_assistant_operating_system_update, Clean Entity: update.home_assistant_operating_system_update
```

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

## Screenshot

<img width="1035" height="689" alt="Screenshot 2025-12-25 121709" src="https://github.com/user-attachments/assets/40e5af1c-3759-4923-9e35-71403c214645" />


## 📝 Version History

### Version 2.7.0
- 🐛 Fixed: pressing **Skip** triggered a "✅ Update Complete" notification — the state also goes `on` → `off` for a skipped update. Now the notification (and its reminder) is simply cleared
- 🐛 Fixed: reminders listed *all* update entities instead of only the ones you selected
- 🐛 Fixed: an update that appeared outside the notification window was silently dropped (no persistent notification, no config check, no later notice when reminders are disabled). It is now announced when the window opens
- 🐛 Fixed: update entities without a device (some integrations) broke the "new update" notification
- 🐛 Fixed: install failed for update entities that do not support backups while "Take Backup" was on
- 🔒 Install/Skip buttons are only handled for monitored update entities, so multiple automations/apps no longer react to each other's buttons; unrelated notification actions no longer produce warnings in the log
- 🧹 HA startup now dismisses the persistent notifications of *all* monitored updates that are no longer pending (not only core/OS)
- 🔧 A failing notify service for one device no longer stops the notifications for the other devices
- 🔧 The "5 minutes (testing)" reminder rounds correctly; the reminder trigger is not registered when reminders are disabled
- 🔧 Modernized syntax (`triggers`, `trigger:`, `filter` selectors)

### Version 2.6.0 (2025-12-19)
- ✨ Added Changelog button to notifications (3rd action button)
- 📋 Opens release notes URL when available
- 🔧 Falls back to custom changelog URLs from config

### Version 2.5.0 (2025-12-19)
- ⏱️ Added short reminder intervals for testing (5, 15, 30 minutes)
- 🔧 Changed reminder logic to minute-based calculation
- 🧪 Easier to test notification functionality

### Version 2.4.0 (2025-12-19)
- 🐛 Fixed entity_id extraction from notification tags
- 🧹 Strips `reminder_` and `config_check_` prefixes correctly
- 📊 Enhanced debug logging to show tag transformation

### Version 2.3.0 (2025-12-19)
- ♻️ Removed iOS-specific code for simplicity
- 🤖 Blueprint now explicitly Android-only
- 🧹 Cleaner codebase without iOS compatibility layer

### Version 2.2.0 (2025-12-19)
- 🐛 Fixed callback handling to use notification tag instead of action_data
- 🔧 Tag-based entity identification for proper callback routing

### Version 2.1.0 (2025-12-19)
- 🐛 Fixed install button callback handling
- 🔧 Combined duplicate event triggers
- 🐛 Added debug logging for callbacks

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

## ❓ FAQ

**Q: Does this work on iOS?**
A: This blueprint is designed and tested for Android only. iOS support has not been tested and may not work correctly.

**Q: Why Android only?**
A: The blueprint uses Android-specific notification action handling. iOS uses different event formats that haven't been implemented or tested.

**Q: Can I test the notifications quickly?**
A: Yes! Use the "Every 5 minutes (testing)" reminder interval to get quick test notifications. Don't forget to change it back to a longer interval after testing.

**Q: The changelog button doesn't appear, why?**
A: The changelog button only appears when the update entity has a `release_url` attribute or you've configured a custom URL in the Advanced Settings.

## 🤝 Contributing

Found a bug or have a suggestion? Please [open an issue](https://github.com/r3mcos3/blueprints/issues) on GitHub!

## 📄 License

This blueprint is provided as-is under the MIT License.

## 🙏 Credits

Created by [r3mcos3](https://github.com/r3mcos3)
