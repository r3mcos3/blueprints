# Home Assistant Community Forum Posts

Templates voor het plaatsen van blueprints op https://community.home-assistant.io/c/blueprints-exchange/53

---

## 1. 🚗 AI Parking Spot Counter

**Title:** `🚗 AI Parking Spot Counter - Count free parking spaces with AI vision`

**Tags:** `automation`, `ai`, `camera`, `notification`, `telegram`

**Post:**

```markdown
# AI Parking Spot Counter 🚗

Automatically count free and occupied parking spaces using AI vision when you arrive home!

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

Wake up gently with lights that turn on before your phone alarm!

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

Generate beautiful emoji-rich weather summaries using AI!

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

Play a chime sound on your media players when the doorbell rings!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fdoorbell_chime%2Fdoorbell_chime.yaml)

## Features

- 🔊 **Adjustable Volume** - Set chime volume with optional restore
- 🔇 **Quiet Hours** - Respect do-not-disturb times
- 🎵 **Custom Sounds** - Use any audio file as your chime
- 📱 **Multiple Speakers** - Play on one or many media players
- 🚪 **Any Trigger** - Works with any doorbell sensor or button

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

Automatically control lights based on presence - lights on when someone arrives, off when everyone leaves!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fpresence_lights%2Fpresence_lights.yaml)

## Features

- 🏠 **Arrival Detection** - Lights on when someone comes home
- 👋 **Departure Detection** - Lights off when last person leaves
- 🌅 **Sun Awareness** - Only activates after sunset
- 👥 **Multi-Person** - Tracks multiple people
- 💡 **Any Lights** - Control any light, switch, or group

## Requirements

- Home Assistant 2025.12.0+
- Person entities with device trackers
- Light/switch entities

## GitHub

[GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/presence_lights)
```

---

## 6. 🔥 Smart Heating Controller

**Title:** `🔥 Smart Heating Controller - Intelligent climate control with presence & door protection`

**Tags:** `automation`, `climate`, `heating`, `presence`, `energy`

**Post:**

```markdown
# Smart Heating Controller 🔥

Intelligent climate control with presence detection, door/window protection, and energy-saving features!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fsmart_heating%2Fsmart_heating.yaml)

## Features

- 🌡️ **Smart Temperature Control** - Automatic heating management
- 🏠 **Presence Detection** - Lower temp when away
- 🚪 **Door/Window Protection** - Pause heating when open
- ⏰ **Scheduling** - Different temps for different times
- 💰 **Energy Saving** - Reduce heating costs automatically
- 🔄 **HA Start & Reload Triggers** - Applies settings on restart

## Requirements

- Home Assistant 2025.12.0+
- Climate entity (thermostat)
- Optional: Door/window sensors, presence sensors

## GitHub

[GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/smart_heating)
```

---

## 7. 🔈 Volume Control

**Title:** `🔈 Volume Control - Automated speaker volume management`

**Tags:** `automation`, `media-player`, `volume`

**Post:**

```markdown
# Volume Control 🔈

Automate volume control for all your speakers!

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fvolumecontrol%2Fvolumecontrol.yaml)

## Features

- 🔊 **Volume Automation** - Set volumes automatically
- 🕐 **Time-Based** - Different volumes at different times
- 📱 **Multiple Speakers** - Control multiple media players
- 🔇 **Quiet Hours** - Lower volume at night

## Requirements

- Home Assistant 2025.12.0+
- Media player entities

## GitHub

[GitHub Repository](https://github.com/r3mcos3/blueprints/tree/main/volumecontrol)
```

---

# Tips voor het posten

1. **Eén post per blueprint** - Maak een aparte post voor elke blueprint
2. **Gebruik de import button** - De `my.home-assistant.io` badge maakt importeren makkelijk
3. **Screenshots** - Voeg screenshots toe van de blueprint config UI
4. **Reageer op vragen** - Check regelmatig voor vragen van gebruikers
5. **Update posts** - Werk de post bij als je nieuwe versies uitbrengt
