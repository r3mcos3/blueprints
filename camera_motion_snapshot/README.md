# 📸 Camera Snapshot on Motion to Telegram 🤖

This blueprint 🏗️ automatically takes a snapshot 🖼️ from a specified camera 📷 when a motion sensor 🏃‍♂️ is triggered and sends it to a specific Telegram chat 📨.

## ✨ Features
- **⚡ Instant Snapshot:** Captures an image the moment motion is detected.
- **🤖 Multiple Bot Support:** Select a specific Telegram Bot integration instance.
- **🆔 Targeted Messaging:** Send to a specific Chat ID.
- **✍️ Fully Customizable Caption:** You decide exactly what the message says.
- **💾 Customizable Path:** Define where the temporary snapshot is stored.
- **⏱️ Adjustable Timeout:** Prevent spam by setting a cooldown period between snapshots.

## 🛠️ Requirements
- **🤖 Telegram Bot Integration:** Ensure the [Telegram Bot](https://www.home-assistant.io/integrations/telegram_bot/) integration is configured.
- **📂 Writable Directory:** The path must be writable by Home Assistant (e.g., `/config/www/`).

## 📥 Inputs

| Input | Description | Required |
|---|---|---|
| 🏃‍♂️ Motion Sensor | The sensor that detects motion. | ✅ Yes |
| 📷 Camera | The camera entity for the snapshot. | ✅ Yes |
| 🤖 Telegram Bot Instance | Choose which bot integration to use. | ✅ Yes |
| 🆔 Target Chat ID | The ID of the chat/user to send the photo to. | ✅ Yes |
| ✍️ Message Caption | The exact text to send with the photo. | ✅ Yes |
| 📂 Snapshot Path | Local storage path for the image. | ✅ Yes |
| ⏱️ Timeout (Cooldown) | The time to wait after a snapshot before allowing another one. | ❌ No (Default: 60s) |

## 🚀 Installation
1. 📥 Import this blueprint into Home Assistant.
2. ⚙️ Configure your sensors, camera, bot, chat ID, and message.
3. ✅ Save and stay informed!

## 🏷️ Version History
- **1.7.0**: ⏱️ Added a customizable timeout (cooldown) to prevent multiple snapshots in a short period.
- **1.6.0**: 🛠️ Added `author` and `source_url` for better integration with Home Assistant.
- **1.5.0**: ✍️ Made the message caption fully customizable.
- **1.4.0**: 🏷️ Added custom notification name and 🤖 Config Entry picker.
- **1.3.0**: 🐛 Fixed "UndefinedError" for manual testing.
- **1.2.0**: ✨ Added more emojis and polished descriptions.
- **1.1.0**: 🗑️ Removed `target_chat_id`.
- **1.0.0**: 🎉 Initial release.
