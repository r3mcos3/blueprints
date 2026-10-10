# 🚪 Door Open Alert

[![version](https://img.shields.io/badge/version-1.1.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

Get notified when a door (e.g. the back door) has been open for too long, and optionally have it announced at full volume on your speakers when the weather is bad. 🚪

## ✨ Features

- 📱 **Mobile Notification** - Sent to one or more mobile devices after a configurable time (default 10 minutes)
- 🏷️ **Custom Door Name** - Use a friendly name like "the back door" in the notification and announcement
- 🌧️ **Bad Weather Announcement** - Optional text-to-speech announcement on selected speakers, only when the weather entity reports a bad condition
- 🔊 **Full Volume** - Announcement volume is adjustable (default 100%)
- 🌍 **Fully Translatable** - Notification title, messages and the spoken announcement are text inputs, so you can write them in your own language
- 🔄 **Volume Restore** - Restores the original speaker volume afterwards

## 📋 Requirements

1. **Door Sensor** - A binary sensor (contact sensor) for the door
2. **Mobile App** - The Home Assistant companion app on at least one device
3. For the optional announcement: a **weather** entity, a **TTS** entity and one or more **media players**

## 🚀 Installation

[![Open your Home Assistant instance and show the blueprint import dialog.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fdoor_open_alert%2Fdoor_open_alert.yaml)

## ⚙️ Configuration

| Input | Description |
|-------|-------------|
| Door Sensor | The contact sensor to monitor |
| Door Name | Name used in messages (empty = sensor name) |
| Open Duration | How long the door must be open before alerting |
| Mobile Devices | Devices that receive the notification |
| Enable Speaker Announcement | Announce on speakers when the weather is bad |
| Weather Entity / Bad Weather Conditions | Which conditions count as bad weather |
| Speakers / TTS Entity | Where and how the announcement is played |
| Notification Title / Messages | Your own text, with placeholders `{door}` and `{weather}` |
| Announcement Message | Spoken text (match your TTS voice language), same placeholders |
| Announcement Volume / Restore Volume | Volume handling for the announcement |

## 📝 Changelog

- **1.1.0** - Messages and announcement are now configurable (multi-language support)
- **1.0.0** - Initial release
