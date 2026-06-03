# Home Assistant Community Forum Posts

Templates voor het plaatsen van blueprints op https://community.home-assistant.io/c/blueprints-exchange/53

---

## 1. 🚗 AI Parking Spot Counter

**Title:** `🚗 AI Parking Spot Counter - Count free parking spaces with AI vision`

**Tags:** `automation`, `ai`, `camera`, `notification`, `telegram`

**Post:**

```markdown
# AI Parking Spot Counter 🚗

**Version 2.0.0** | Automatically count free and occupied parking spaces using AI vision when you arrive home!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fai_parking_counter%2Fai_parking_counter.yaml)

## Features

- 🤖 **AI-Powered Analysis** - Uses AI Task integration to analyze camera images
- 📷 **Camera Integration** - Works with any Home Assistant camera
- 🏘️ **Multiple Zones** - 1 required + 4 optional zone detection points
- 🧭 **Optional Proximity Check** - Only trigger when approaching home
- 📱 **Telegram Notifications** - Get notified with free spots count
- 📸 **Snapshot Storage** - Save camera snapshots for review
- 📦 **Organized UI** - Clean collapsed input sections

## Requirements

- Home Assistant 2025.12.0+
- AI Task integration (Google AI recommended, OpenAI may have issues with camera attachments)
- Camera entity with snapshot support
- Person entity for tracking
- Zone entities
- Input Number helpers for storing counts

## Configuration

| Input | Description |
|-------|-------------|
| Person | Person to track for arrivals |
| Zone 1 | Primary zone (required) |
| Zones 2-5 | Optional additional zones |
| Proximity Sensor | Optional direction check |
| Camera | Camera to analyze |
| AI Task | AI entity for vision analysis |
| Parking Spaces | Total spaces to count (1-20) |
| Telegram | Optional notification settings |

## GitHub

Full documentation and source code: [GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/ai_parking_counter)

## Changelog

- **2.0.0** - Multiple zones, optional proximity, collapsed sections
- **1.0.5** - English translations
- **1.0.0** - Initial release
```

---

## 2. ⏰ Alarm Light

**Title:** `⏰ Alarm Light - Wake up gently with lights before your phone alarm`

**Tags:** `automation`, `light`, `alarm`, `presence`

**Post:**

```markdown
# Alarm Light ⏰

**Version 1.0.0** | Wake up gently with lights that turn on before your phone alarm!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Falarm_light%2Falarm_light.yaml)

## Features

- ⏰ **Alarm Integration** - Syncs with your phone's next alarm sensor
- 💡 **Gradual Wake-up** - Lights turn on 5-60 minutes before alarm
- 🏠 **Presence Aware** - Only triggers when you're home
- 🌙 **Darkness Check** - Only activates when it's dark outside
- 📅 **Day Selection** - All days, weekdays only, or weekends only
- ✨ **Adjustable Brightness** - Configure the perfect wake-up brightness

## Requirements

- Home Assistant 2025.12.0+
- Next Alarm sensor (Android: built-in, iOS: requires Shortcuts workaround)
- Person entity
- Light entity

## Android Setup

1. Install Home Assistant Companion App
2. Enable "Next Alarm" sensor in Companion App settings
3. Sensor appears as `sensor.phone_name_next_alarm`

## iOS Setup

iOS doesn't natively expose alarm data. Use iOS Shortcuts to sync your alarm to an Input Datetime helper. See [iOS guides in the README](https://github.com/r3mcos3/blueprints/tree/main/alarm_light#setting-up-next-alarm-sensor-ios--iphone).

## Configuration

| Input | Description | Default |
|-------|-------------|---------|
| Alarm Sensor | Next alarm timestamp sensor | - |
| Person | Person to check if home | - |
| Lights | Lights to turn on | - |
| Offset | Minutes before alarm | 10 min |
| Brightness | Light brightness | 33% |
| Days | All/Weekdays/Weekends | All |

## GitHub

[GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/alarm_light)
```

---

## 3. 🤖 AI Weather Report Generator

**Title:** `🤖 AI Weather Report Generator - Daily weather summaries with AI`

**Tags:** `automation`, `ai`, `weather`, `notification`

**Post:**

```markdown
# AI Weather Report Generator 🤖

**Version 1.0.2** | Generate beautiful emoji-rich weather summaries using AI!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fai_weather_report%2Fai_weather_report.yaml)

## Features

- 🤖 **AI-Powered** - Uses AI to create natural language weather summaries
- ☀️ **Emoji Rich** - Beautiful weather descriptions with relevant emojis
- 📊 **Forecast Data** - Processes hourly/daily weather forecasts
- 💾 **Text Helper** - Stores report in an input_text for dashboard use
- ⏰ **Scheduled Updates** - Runs at configurable intervals

## Requirements

- Home Assistant 2025.12.0+
- AI Task integration (Google AI, OpenAI, etc.)
- Weather integration
- Input Text helper

## GitHub

[GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/ai_weather_report)
```

---

## 4. 🔔 Doorbell Chime

**Title:** `🔔 Doorbell Chime - Play sounds on media players when doorbell rings`

**Tags:** `automation`, `doorbell`, `media-player`, `notification`

**Post:**

```markdown
# Doorbell Chime 🔔

**Version 1.0.4** | Play a chime sound on your media players when the doorbell rings!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fdoorbell_chime%2Fdoorbell_chime.yaml)

## Features

- 🔊 **Adjustable Volume** - Set chime volume with optional restore
- 🔇 **Quiet Hours** - Respect do-not-disturb times
- 🎵 **Custom Sounds** - Use any audio file as your chime
- 📱 **Multiple Speakers** - Play on one or many media players
- 🚪 **Any Trigger** - Works with any doorbell sensor or button
- ⏱️ **Built-in Cooldown** - Prevent chime spam

## Requirements

- Home Assistant 2025.12.0+
- Media player entity (Sonos, Google Home, etc.)
- Doorbell sensor/button entity
- Audio file accessible to HA

## GitHub

[GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/doorbell_chime)
```

---

## 5. 💡 Presence Home/Away Lights

**Title:** `💡 Presence Lights - Turn lights on/off based on who's home`

**Tags:** `automation`, `light`, `presence`, `person`

**Post:**

```markdown
# Presence Home/Away Lights 💡

**Version 1.0.13** | Automatically control lights based on presence - lights on when someone arrives, off when everyone leaves!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fpresence_lights%2Fpresence_lights.yaml)

## Features

- 🏠 **Arrival Detection** - Lights on when someone comes home
- 👋 **Departure Detection** - Lights off when last person leaves
- 🌅 **Sun Awareness** - Only activates after sunset
- 👥 **Multi-Person** - Tracks multiple people
- 💡 **Flexible Control** - Control any light, switch, or group

## Requirements

- Home Assistant 2025.12.0+
- Person entities with device trackers
- Light/switch entities
- Zone entity

## GitHub

[GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/presence_lights)
```

---

## 6. 🛡️ Persistent Motion Light

**Title:** `🛡️ Persistent Motion Light - Keep lights ON with motion protection`

**Tags:** `automation`, `light`, `motion`, `safety`

**Post:**

```markdown
# Persistent Motion Light 🛡️

**Version 1.1** | Keep your lights ON as long as there's motion - with protection against manual turn-off!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fpersistent_motion_light%2Fpersistent_motion_light.yaml)

## Features

- 🛡️ **Safety Feature** - Immediately re-activates if manually turned off during motion
- 🏃‍♂️ **Motion Detection** - Keeps lights on while motion is detected
- ⏳ **Configurable Wait Time** - Adjustable delay after motion stops
- 💡 **Flexible Control** - Works with lights and switches
- 🔄 **Restart Mode** - Seamlessly handles continuous motion detection

## Requirements

- Home Assistant 2025.12.0+
- Motion sensor (binary sensor with motion device class)
- Light or switch entity

## Perfect For

- Stairways and hallways where safety is important
- Bathrooms where lights should stay on
- Garages with multiple motion zones
- Any area where accidental turn-off could be dangerous

## Configuration

| Input | Description | Default |
|-------|-------------|---------|
| Motion Sensor | Binary sensor detecting motion | - |
| Target Light | Light(s) or switch(es) to control | - |
| Wait Time | Minutes to wait after motion stops | 5 min |

## GitHub

[GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/persistent_motion_light)
```

---

## 7. 🔥 Smart Heating Controller

**Title:** `🔥 Smart Heating Controller - Intelligent climate control with presence & door protection`

**Tags:** `automation`, `climate`, `heating`, `presence`, `energy`

**Post:**

```markdown
# Smart Heating Controller 🔥

**Version 1.8.0** | Intelligent climate control with presence detection, door/window protection, manual override, and energy-saving features!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fsmart_heating%2Fsmart_heating.yaml)

## Features

- 🏠 **Presence-based control** - Automatically adjusts temperature when you arrive or leave
- 🌡️ **Outdoor temperature factor** - Disables heating when it's warm outside (eco mode)
- 🚪 **Door/window protection** - Pauses heating when doors or windows are open too long
- 🌙 **Night mode** - Reduces temperature during sleeping hours
- ⏰ **Smart pre-heating** - Starts heating before you wake up, scaled to outdoor coldness
- ❄️ **Frost protection** - Maintains minimum temperature to prevent pipe freezing
- 💧 **Humidity compensation** - Adjusts target temperature based on indoor humidity (optional)
- 🛠️ **Manual override** - Temporarily hold any temperature for a configurable duration
- 🪟 **Virtual window detection** - Detects open windows via rapid indoor temperature drops (no sensor needed)
- 🔄 **Gradual transitions** - Stepwise temperature changes instead of immediate jumps (optional)
- 🎛️ **Dynamic comfort temperature** - Optional `input_number` helper to adjust comfort temp from the UI
- 🔍 **Debug mode** - Persistent notification showing active mode and all state values after every run

## How the priority system works

The blueprint decides the target temperature based on a strict priority hierarchy:

| Priority | Mode | Condition |
|----------|------|-----------|
| 1 | ❄️ Frost protection | Indoor temp below frost threshold |
| 2 | 🛠️ Manual override | Override helper is active & not expired |
| 3 | ☀️ Eco | Outdoor temp above threshold |
| 4 | 🏃 Away | Nobody home |
| 5 | ⏰ Pre-heat | Within pre-heat window before wake-up |
| 6 | 🌙 Night | Between configured night start/end times |
| 7 | 🏠 Comfort | Default — home, daytime, cold outside |

## Requirements

- Home Assistant 2025.12.0+
- Climate entity (thermostat, e.g. `climate.tado`)
- Indoor + outdoor temperature sensors
- Presence zone (typically `zone.home`)
- Door/window binary sensors

### Optional

- **Input Boolean helper** — for manual override activation
- **Input Number helper** — for dynamic comfort temperature via UI slider
- **Humidity sensor** — for humidity-based temperature adjustments

## Configuration

| Input | Description | Default |
|-------|-------------|---------|
| 🌡️ Comfort temperature | Target when people are home | 21°C |
| 🏃 Away temperature | Target when nobody is home | 17°C |
| ❄️ Frost protection temp | Absolute minimum temperature | 7°C |
| 🌙 Night temperature | Target during sleeping hours | 18°C |
| 🌡️ Outdoor threshold | Disable heating above this outdoor temp | 18°C |
| 🚪 Door open delay | Seconds before pausing heating | 300 s |
| 🌙 Night start/end | Scheduled night mode times | 23:00 / 07:00 |
| ⏰ Pre-heat duration | Minutes before wake-up to start heating | 30 min |
| 🛠️ Override duration | How long manual override lasts | 2 hours |
| 🔍 Debug mode | Enable persistent state notification | Off |

## Debug mode

Enable **Debug Mode** in the Debug Settings section to get a persistent notification after every run showing:

```
Mode: comfort
Target temp: 21.0°C
Indoor: 19.5°C | Outdoor: 8.2°C
People home: 2
Night: false | Pre-heat: false
Override active: false
Any door/window open: false
Last run: 2026-05-31 14:23:05
```

The notification updates in place — no spam.

## GitHub

Full documentation, examples, and troubleshooting: [GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/smart_heating)

## Changelog

- **1.8.0** - Fixed: manual override mode now correctly holds temperature (variable order bug); night start skips when override is active; added optional debug mode
- **1.7.0** - Adaptive pre-heating scaled to outdoor coldness; virtual window detection; gradual transitions
- **1.6.0** - Dynamic comfort temperature via input_number helper
- **1.3.1** - Improved override handling; automatic restoration when override expires
- **1.3.0** - Manual override feature with configurable timeout
- **1.2.3** - Initial full-featured release
```

---

## 8. 🔈 Volume Control

**Title:** `🔈 Volume Control - Automated speaker volume management`

**Tags:** `automation`, `media-player`, `volume`

**Post:**

```markdown
# Volume Control 🔈

**Version 1.0** | Automate volume control for all your speakers!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fvolumecontrol%2Fvolumecontrol.yaml)

## Features

- 🔊 **Volume Automation** - Set volumes automatically
- 🕐 **Time-Based** - Different volumes at different times
- 📱 **Multiple Speakers** - Control multiple media players
- 🔇 **Quiet Hours** - Lower volume at night
- ⚙️ **Custom Actions** - Additional automation support

## Requirements

- Home Assistant 2025.12.0+
- Media player entities
- Schedule helper

## GitHub

[GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/volumecontrol)
```

---

## 9. 🔄 Update Notifications (Android)

**Title:** `🔄 Update Notifications (Android) - Get notified about HA updates via Mobile App`

**Tags:** `automation`, `mobile-app`, `android`, `notification`, `update`

**Post:**

```markdown
# Update Notifications 🔄 (Android)

**Version 2.6.0** | Get notified about Home Assistant updates via Mobile App with actionable buttons!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fupdate_notifications%2Fupdate_notifications.yaml)

> **⚠️ Platform Support:** This blueprint is specifically designed and tested for **Android devices only**. iOS support has not been tested and may not work as expected.

## Features

- 📱 **Android Notifications** - Get notified on your Android device
- 🔔 **Update Alerts** - Notifications when updates are available
- 🎛️ **3 Actionable Buttons** - Install, skip, or view changelog directly from notification
- 📋 **Changelog Button** - Quick access to release notes (when available)
- ✅ **Completion Notifications** - Know when updates finish
- ⏳ **Progress Updates** - See when updates start
- 🔁 **Periodic Reminders** - Configurable reminders (5min - 24h intervals)
- ⚙️ **Config Check** - Run config check before core updates
- 💾 **Backup Support** - Create backup before updating
- 🐛 **Debug Logging** - Built-in logging for troubleshooting

## Requirements

- Home Assistant 2025.12.0+
- **Android Device** with Home Assistant Companion App
- Update entities to monitor

## How It Works

When an update is available, you'll receive a notification with:
- Update name and version info
- ✅ **Install** button to start the update
- ⏭️ **Skip** button to skip this version
- 📋 **Changelog** button to view release notes (when available)
- Tap notification body to view changelog or updates page

Android supports maximum 3 notification actions, and this blueprint uses all three!

## Quick Testing

Want to test it out quickly? Use the "Every 5 minutes (testing)" reminder interval to get test notifications without waiting hours. Don't forget to change it back to a longer interval after testing!

## GitHub

Full documentation, version history, and troubleshooting: [GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/update_notifications)
```

---

## 10. 🔄 Update Notifications (Telegram)

**Title:** `🔄 Update Notifications (Telegram) - Get notified about HA updates via Telegram`

**Tags:** `automation`, `telegram`, `notification`, `update`

**Post:**

```markdown
# Update Notifications 🔄 (Telegram)

**Version 1.3.0** | Get notified about Home Assistant updates via Telegram with inline keyboard buttons!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Ftelegram_update_notifications%2Ftelegram_update_notifications.yaml)

## Features

- 💬 **Telegram Bot Integration** - Get notified via your Telegram bot
- 🔔 **Update Alerts** - Notifications when updates are available
- 🎛️ **Inline Keyboard Buttons** - Install, skip, or view changelog directly from messages
- 📋 **Changelog Button** - Quick access to release notes (when available)
- ✅ **Completion Notifications** - Know when updates finish
- ⏳ **Progress Updates** - See when updates start
- 🔁 **Periodic Reminders** - Configurable reminders (5min - 24h intervals)
- ⚙️ **Config Check** - Run config check before core updates
- 💾 **Backup Support** - Create backup before updating
- 💬 **Instant Feedback** - Immediate responses when buttons are pressed

## Requirements

- Home Assistant 2025.12.0+
- **Telegram Bot** (create via @BotFather)
- **Telegram Integration** configured in Home Assistant
- Your **Chat ID**
- Update entities to monitor

## Quick Setup

1. **Create a Bot:**
   - Open Telegram, search for @BotFather
   - Send `/newbot` and follow instructions
   - Save your bot token

2. **Get Your Chat ID:**
   - Send a message to your bot
   - Visit: `https://api.telegram.org/bot<TOKEN>/getUpdates`
   - Find your chat_id in the response

3. **Configure Home Assistant:**
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

## How It Works

When an update is available, you'll receive a Telegram message with:
- Update name and version info
- ✅ **Install** button to start the update
- ⏭️ **Skip** button to skip this version
- 📋 **Changelog** button to view release notes (when available)

Click any button and get instant feedback!

## Quick Testing

Want to test it out quickly? Use the "Every 5 minutes (testing)" reminder interval to get test notifications without waiting hours. Don't forget to change it back to a longer interval after testing!

## Comparison

**Telegram vs Mobile App version:**
- ✅ Telegram: Works on any device with Telegram app
- ✅ Telegram: Inline keyboard buttons directly in chat
- ✅ Telegram: Instant feedback messages
- ✅ Mobile App (Android): Native Android notifications
- ✅ Mobile App (Android): Integrates with notification system

Choose the version that fits your preferred notification platform!

## GitHub

Full documentation, setup guide, and troubleshooting: [GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/telegram_update_notifications)
```

---

## 11. ☀️ Sun-aware Motion Light

**Title:** `☀️ Sun-aware Motion Light - Motion-activated lights with day/night brightness`

**Tags:** `automation`, `light`, `motion`, `sun`

**Post:**

```markdown
# Sun-aware Motion Light ☀️

**Version 1.0** | Smart motion-activated lighting that adapts to the sun's position!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fsun_aware_motion_light%2Fsun_aware_motion_light.yaml)

## Features

- 🏃‍♂️ **Motion Detection** - Automatically turns lights on when motion is detected
- ☀️ **Sun-Aware Mode** - Different brightness levels for day and night
- 🌓 **Flexible Brightness** - Customizable brightness for both day and night
- ⏱️ **Auto Turn-Off** - Configurable delay before lights turn off
- 🔆 **Default Brightness** - Option to use single brightness level instead of sun-aware mode
- 🔄 **Restart Mode** - Seamlessly handles continuous motion detection

## Requirements

- Home Assistant 2025.12.0+
- Motion sensor (binary sensor with motion device class)
- Light entity
- Sun integration (built-in)

## Perfect For

- Hallways with bright daytime, dim nighttime lighting
- Bathrooms with consistent brightness
- Outdoor paths with adaptive safety lighting
- Any motion-activated scenario where brightness should vary by time of day

## Configuration

| Input | Description | Default |
|-------|-------------|---------|
| Motion Sensor | Binary sensor detecting motion | - |
| Target Light | Light(s) to control | - |
| Sun-aware Mode | Enable day/night brightness | Enabled |
| Brightness (Day) | Brightness when sun is up | 100% |
| Brightness (Night) | Brightness when sun is down | 10% |
| Turn-off Delay | Minutes before turning off | 5 min |

## GitHub

Full documentation with examples: [GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/sun_aware_motion_light)
```

---

## 12. ☀️ Sun Notifications

**Title:** `☀️ Sun Notifications - Get notified at sunrise and sunset via Telegram`

**Tags:** `automation`, `telegram`, `notification`, `sun`

**Post:**

```markdown
# Sun Notifications ☀️

**Version 1.1.2** | Get notified at sunrise and sunset via Telegram with customizable messages and time offsets!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fsun_notifications%2Fsun_notifications.yaml)

## Features

- 🌅 **Sunrise Notifications** - Get notified when the sun rises
- 🌇 **Sunset Notifications** - Get notified when the sun sets
- ⏰ **Time Offsets** - Set notifications before or after sunrise/sunset
- 💬 **Custom Messages** - Personalize your notification messages with templates
- 🔔 **Telegram Integration** - Receive notifications via Telegram Bot
- ⚙️ **Independent Control** - Enable/disable sunrise and sunset notifications separately
- 🌍 **Automatic Calculation** - Uses your Home Assistant location for accurate times

## Requirements

- Home Assistant 2025.12.0+
- Telegram Bot (create via @BotFather)
- Telegram Integration configured in Home Assistant
- Sun integration (built-in)

## Perfect For

- Morning wake-up reminders
- Evening routine triggers
- Photography golden hour alerts
- Planning outdoor activities
- Automating home routines based on daylight

## Configuration

| Input | Description | Default |
|-------|-------------|---------|
| Telegram Bot | Your Telegram bot integration | - |
| Enable Sunrise | Toggle sunrise notifications | Enabled |
| Sunrise Offset | Time before/after sunrise | 00:00:00 |
| Sunrise Message | Custom sunrise message | "De zon komt op ☀️" |
| Enable Sunset | Toggle sunset notifications | Enabled |
| Sunset Offset | Time before/after sunset | 00:00:00 |
| Sunset Message | Custom sunset message | "De zon gaat onder 🌃" |

### Offset Examples
- `-00:30:00` = 30 minutes before
- `00:00:00` = Exactly at sunrise/sunset
- `00:15:00` = 15 minutes after

## GitHub

Full documentation with template examples: [GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/sun_notifications)
```

---

## 13. 📸 Camera Motion Snapshot

**Title:** `📸 Camera Motion Snapshot - Captures and sends a camera snapshot via Telegram`

**Tags:** `automation`, `camera`, `motion`, `telegram`, `notification`

**Post:**

```markdown
# Camera Motion Snapshot 📸

**Version 1.7.0** | Automatically capture a snapshot from your camera when motion is detected and send it instantly via your Telegram bot!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fcamera_motion_snapshot%2Fcamera_motion_snapshot.yaml)

## Features

- 📸 **Instant Snapshot** - Captures an image the moment motion is detected
- 🏃‍♂️ **Motion Triggered** - Works with any motion sensor
- 🤖 **Telegram Support** - Send images to specific Telegram Chat IDs
- ✍️ **Custom Caption** - You decide the message text
- ⏱️ **Cooldown Timer** - Built-in timeout to prevent notification spam
- 💾 **Local Path** - Fully customizable storage location

## Requirements

- Home Assistant 2025.12.0+
- Camera entity
- Motion sensor (binary sensor)
- Telegram Bot integration
- Writable local directory

## Configuration

| Input | Description |
|-------|-------------|
| Motion Sensor | Sensor that triggers the snapshot |
| Camera | Camera to take the snapshot from |
| Telegram Bot | Telegram Bot instance to use |
| Target Chat ID | ID of the chat to receive the photo |
| Message Caption | Text sent with the photo |
| Timeout | Cooldown period between snapshots |

## GitHub

[GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/camera_motion_snapshot)
```

---

## 14. 🔋 Accu Saver

**Title:** `🔋 Accu Saver - Smart battery health management for laptop servers`

**Tags:** `automation`, `battery`, `power`, `energy`

**Post:**

```markdown
# Accu Saver 🔋

**Version 1.2.0** | Smart battery health management for laptop servers!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Faccu_saver%2Faccu_saver.yaml)

## Features

- 🔋 **Battery Level Monitoring** - Dual threshold monitoring for optimal battery health
- ⚡ **Automatic Charge Control** - Smart plug integration for charging control
- 🎯 **Configurable Limits** - Set your own upper/lower battery thresholds
- 🔄 **Immediate Response** - No delays in charge control
- ⏰ **Periodic Status Checks** - Regular monitoring every 5 minutes
- 🛡️ **Protection** - Prevents overcharging and deep discharge
- 🚀 **Startup Sync** - Correct initial state on startup

## Requirements

- Home Assistant 2025.12.0+
- Battery percentage sensor (from laptop or other device)
- Smart plug or switch to control charging

## How It Works

The blueprint monitors your battery level and controls a smart plug:
- When battery drops **below lower limit** → Turn ON charging
- When battery reaches **upper limit** → Turn OFF charging
- Regular checks ensure the battery stays within healthy limits

## Perfect For

- Laptop servers running Home Assistant
- Always-plugged devices that need battery protection
- Any device where maintaining battery health is important
- Extending the lifespan of Li-ion batteries

## Configuration

| Input | Description | Default |
|-------|-------------|---------|
| Battery Sensor | Sensor reporting battery percentage | - |
| Charger Switch | Smart plug controlling the charger | - |
| Upper Limit | Battery % to stop charging | 80% |
| Lower Limit | Battery % to start charging | 20% |

## GitHub

Full documentation and examples: [GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/accu_saver)
```

---

## 15. ☀️ Sun-Aware Shutter Control

**Title:** `☀️ Sun-Aware Shutter Control - Automatically close shutters based on sun position`

**Tags:** `automation`, `cover`, `sun`, `shutter`, `blinds`

**Live URL:** https://community.home-assistant.io/t/sun-aware-shutter-control-automatically-close-shutters-based-on-sun-position/1012173

**Post:**

```markdown
# Sun-Aware Shutter Control ☀️

**Version 1.14.0** | Automatically close your shutters when the sun shines on your house — and open them again when it moves away!

> ⚠️ **This blueprint is currently in a testing phase.** It has been tested in a single environment. Feedback and bug reports are very welcome!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fsun_shutter_control%2Fsun_shutter_control.yaml)

## ## The problem this solves

Every day the sun moves from one side of your house to the other. In the morning it shines on the front, in the afternoon on the back. Without automation you have to remember to close and open your shutters multiple times a day — this blueprint handles that for you automatically.

## Features

- ☀️ **Sun position tracking** - Closes shutters when the sun shines on the front or back facade
- 🔄 **Automatic opening** - Opens shutters once the sun moves away (optional)
- 🖐️ **Smart manual override** - Only triggers when a shutter is manually **closed**; a manual open never blocks the sun-close logic so the automation stays in control
- 👥 **Presence-aware override** - Configure up to 2 person entities: when someone is home, manual operations are respected; when nobody is home, the automation takes full control regardless
- 🌇 **Sunset reset** - All overrides are automatically cleared at sunset so the next day starts fresh
- 🌤️ **Cloud detection** - Optional weather integration (supports two entities as cross-check): shutters stay open when overcast, close again when it clears up. When two weather entities are configured, both must agree before shutters close — prevents false closes caused by a single unreliable source
- ⏱️ **Anti-oscillation cooldown** - Minimum wait between moves, prevents rapid up/down on partly cloudy days
- 📍 **Position awareness** - Skips the command if shutters are already at the target position
- 📐 **Configurable sun window** - Control how many degrees of margin counts as "sun on facade"
- 🌅 **Minimum elevation** - Ignores low morning/evening sun below your threshold
- 🔽 **Flexible positions** - Set custom close position (e.g. 50% for partial shade)
- 🏠 **Front and back separately** - Independent shutter groups per facade side

## How it works

The blueprint uses the `sun.sun` azimuth (compass direction 0–360°) and compares it to your house orientation. It fires automatically whenever Home Assistant updates the sun's azimuth — event-driven, no polling needed. Each time it calculates whether the sun is within the configured angle window of each facade:

```
Angle difference = ((sun azimuth − facade direction + 180) % 360) − 180
Sun on facade    = angle difference < sun window AND elevation > minimum
```

This formula handles all compass directions correctly, including the North wrap-around (359° → 1°).

### Decision logic per facade side

| Sun on facade | Weather allows | Override active | Someone home | Action |
|---|---|---|---|---|
| ✅ Yes | ✅ Yes | ❌ No | — | Close shutters |
| ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes | Do nothing (respect manual override) |
| ✅ Yes | ✅ Yes | ✅ Yes | ❌ No | Close shutters (nobody home overrules) |
| ✅ Yes | ❌ No (cloudy) | — | — | Open shutters (treat as no sun) |
| ❌ No | — | ❌ No | — | Open shutters |
| ❌ No | — | ✅ Yes | ✅ Yes | Do NOT open (respect manual close) |
| ❌ No | — | ✅ Yes | ❌ No | Open shutters (nobody home overrules) |
| 🌇 Sunset | — | any | — | Reset all overrides (daily reset) |

## Finding your house azimuth

Go to **[suncalc.org](https://www.suncalc.org/)**, find your house and determine which direction your front door faces. North = 0°, East = 90°, South = 180°, West = 270°. The back facade is calculated automatically (front + 180°).

## Requirements

- Home Assistant 2025.12.0+
- Cover entities (shutters/blinds as `cover` domain)
- Sun integration (built-in, no setup needed)

### Optional

- **Input Boolean helpers** — for manual override detection (one per facade side). Create via Settings → Helpers → Create Helper → Toggle.
- **Person entities** — for presence-aware override behavior.

## Configuration

| Input | Description | Default |
|-------|-------------|---------|
| 🏠 Front facade direction | Compass direction your front facade faces (0–359°) | 180° |
| 🏠 Front shutters | Cover entities on the front | — |
| 🏡 Back shutters | Cover entities on the back | — |
| 📐 Sun window angle | Degrees left/right of facade that count | 90° |
| 🌅 Minimum sun elevation | Minimum sun height above horizon | 10° |
| 🔽 Close position | Shutter position when sun shines (0% = fully closed) | 0% |
| 🔼 Automatically open | Open when sun moves away | On |
| 🔼 Open position | Position when automatically opening | 100% |
| 🖐️ Override helper front | Input Boolean for front manual override | Optional |
| 🖐️ Override helper back | Input Boolean for back manual override | Optional |
| 👤 Person 1 | First household member for presence detection | Optional |
| 👤 Person 2 | Second household member for presence detection | Optional |
| 🌤️ Weather entity | Weather integration for cloud detection | Optional |
| 🌥️ Second weather entity | Second weather source as cross-check; both must agree before closing | Optional |
| ☁️ When to close | Always / Sunny+partly cloudy / Sunny only | Sunny or partly cloudy |
| ⏱️ Cooldown between moves | Minimum minutes between two movements (0 = disabled) | 20 min |

## Manual override explained

Home Assistant records **who** initiated every state change. When a user manually **closes** a shutter (via app, dashboard or physical switch), the context contains a `user_id` — the blueprint detects this and activates the override, preventing the automation from re-opening it.

A manual **open** does **not** set the override by default. This means: if someone opens a shutter in the morning when it's cloudy and later the sun comes out, the blueprint will still close the shutter automatically. Exception: if a presence entity is configured and someone is home, a manual open also sets the override (the automation won't fight the user).

### Override lifecycle

| Event | Override |
|-------|----------|
| User manually **closes** shutter | → ON (always) |
| User manually **opens** shutter while someone is home | → ON |
| Shutter returns to the open position | → OFF |
| **Sun sets** (`sun.sun` → `below_horizon`) | → OFF (daily reset) |

### Presence-aware behavior

Configure **Person 1** and/or **Person 2** (optional) to make the override presence-aware:

| Situation | Close? | Open? |
|-----------|--------|-------|
| Override OFF | ✓ | ✓ |
| Override ON + someone home | ✗ | ✗ (manual operation respected) |
| Override ON + nobody home | ✓ | ✓ (automation takes full control) |

> **Note:** Voice assistant commands (Alexa/Google) don't carry a `user_id` and won't trigger the override.

## GitHub

Full documentation, examples, and troubleshooting: [GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/sun_shutter_control)

## Changelog

- **1.14.0** - Added optional second weather entity as cross-check: when both are configured, shutters only close when BOTH agree (AND-logic) — prevents false closes from a single unreliable weather source
- **1.13.0** - Override is now also bypassed on auto-open when nobody is home (mirrors close behaviour)
- **1.12.0** - Added sunset trigger: all overrides reset at the end of each day so the next morning starts fresh
- **1.11.0** - Fixed: override was reset too early when shutter was still closed, causing the automation to reopen a manually closed shutter
- **1.10.0** - Two separate person inputs (Person 1 + Person 2) replace the single presence entity
- **1.9.0** - Presence-aware override: when nobody is home the automation ignores the override and closes on sun
- **1.8.0** - Manual override only triggers on manual close (not open), so automation can still close after a manual open
- **1.7.0** - Added anti-oscillation cooldown and position check to prevent unnecessary motor activations
- **1.6.0** - Auto-open no longer fires at night — shutters closed in the evening stay closed
- **1.5.0** - Added optional weather/cloud detection: shutters stay open when overcast
- **1.4.0** - Replaced 5-minute polling with event-driven sun azimuth trigger
- **1.3.0** - Fixed: manually closing shutters at bedtime no longer causes them to be re-opened
- **1.2.0** - Translated all labels and descriptions to English
- **1.1.0** - Manual override detection with input_boolean helpers, auto-reset when sun moves away
- **1.0.1** - Added suncalc.org tip to description
- **1.0.0** - Initial release
```

---

# Tips voor het posten

1. **Eén post per blueprint** - Maak een aparte post voor elke blueprint
2. **Gebruik de import button** - De `my.home-assistant.io` badge maakt importeren makkelijk
3. **Screenshots** - Voeg screenshots toe van de blueprint config UI
4. **Reageer op vragen** - Check regelmatig voor vragen van gebruikers
5. **Update posts** - Werk de post bij als je nieuwe versies uitbrengt
