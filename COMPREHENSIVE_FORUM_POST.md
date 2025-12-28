# 🏠 Home Assistant Blueprint Collection - 14 Blueprints for AI, Lighting, Notifications & More

A comprehensive collection of 14 Home Assistant blueprints designed to simplify and enhance your smart home automations. From AI-powered vision analysis to intelligent climate control, this collection covers lighting, notifications, climate management, media automation, and battery management. All blueprints feature version control, comprehensive documentation, and one-click import buttons for easy setup.

**Quick Stats:**
- 🎯 14 ready-to-use blueprints
- 🤖 2 AI-powered automations
- 💡 4 lighting & motion solutions
- 🔔 4 notification systems
- 🌡️ 1 climate controller
- 🔊 2 media automations
- 🔋 1 battery management
- 📦 Minimum HA Version: 2025.12.0+
- 🔄 Version control on all blueprints
- 📚 Comprehensive documentation

## 📑 Table of Contents

- [🤖 AI-Powered Automations](#-ai-powered-automations)
  - [AI Parking Counter](#-ai-parking-counter)
  - [AI Weather Report Generator](#-ai-weather-report-generator)
- [💡 Lighting & Motion](#-lighting--motion)
  - [Alarm Light](#-alarm-light)
  - [Presence Lights](#-presence-lights)
  - [Persistent Motion Light](#-persistent-motion-light)
  - [Sun-aware Motion Light](#-sun-aware-motion-light)
- [🔔 Notifications & Updates](#-notifications--updates)
  - [Camera Motion Snapshot](#-camera-motion-snapshot)
  - [Update Notifications (Android)](#-update-notifications-android)
  - [Telegram Update Notifications](#-telegram-update-notifications)
  - [Sun Notifications](#-sun-notifications)
- [🌡️ Climate & Energy](#-climate--energy)
  - [Smart Heating Controller](#-smart-heating-controller)
- [🔋 Battery & Power](#-battery--power)
  - [Accu Saver](#-accu-saver)
- [🔊 Media & Sound](#-media--sound)
  - [Doorbell Chime](#-doorbell-chime)
  - [Volume Control](#-volume-control)
- [📦 Repository & Support](#-repository--support)

---

## 🤖 AI-Powered Automations

Leverage AI to enhance your home automation with vision analysis and natural language processing.

### 🚗 AI Parking Counter
**Version 2.0.0** | Automatically count free and occupied parking spaces using AI vision when you arrive home!

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fai_parking_counter%2Fai_parking_counter.yaml)

**Features:**
- 🤖 **AI-Powered Analysis** - Uses AI Task integration to analyze camera images
- 📷 **Camera Integration** - Works with any Home Assistant camera
- 🏘️ **Multiple Zones** - 1 required + 4 optional zone detection points
- 🧭 **Optional Proximity Check** - Only trigger when approaching home
- 📱 **Telegram Notifications** - Get notified with free spots count
- 📸 **Snapshot Storage** - Save camera snapshots for review

**Requirements:** AI Task integration (Google AI recommended), Camera entity, Person entity, Zone entities, Input Number helpers

[📖 Full Documentation](https://github.com/r3mcos3/blueprints/tree/main/ai_parking_counter)

---

### 🤖 AI Weather Report Generator
**Version 1.0.2** | Generate beautiful emoji-rich weather summaries using AI!

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fai_weather_report%2Fai_weather_report.yaml)

**Features:**
- 🤖 **AI-Powered** - Uses AI to create natural language weather summaries
- ☀️ **Emoji Rich** - Beautiful weather descriptions with relevant emojis
- 📊 **Forecast Data** - Processes hourly/daily weather forecasts
- 💾 **Text Helper** - Stores report in an input_text for dashboard use
- ⏰ **Scheduled Updates** - Runs at configurable intervals

**Requirements:** AI Task integration, Weather integration, Input Text helper

[📖 Full Documentation](https://github.com/r3mcos3/blueprints/tree/main/ai_weather_report)

---

## 💡 Lighting & Motion

Smart lighting solutions that adapt to your presence, schedule, and environment.

### ⏰ Alarm Light
**Version 1.0.0** | Wake up gently with lights that turn on before your phone alarm!

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Falarm_light%2Falarm_light.yaml)

**Features:**
- ⏰ **Alarm Integration** - Syncs with your phone's next alarm sensor
- 💡 **Gradual Wake-up** - Lights turn on 5-60 minutes before alarm
- 🏠 **Presence Aware** - Only triggers when you're home
- 🌙 **Darkness Check** - Only activates when it's dark outside
- 📅 **Day Selection** - All days, weekdays only, or weekends only
- ✨ **Adjustable Brightness** - Configure the perfect wake-up brightness

**Requirements:** Next Alarm sensor (Android built-in, iOS requires Shortcuts), Person entity, Light entity

[📖 Full Documentation](https://github.com/r3mcos3/blueprints/tree/main/alarm_light)

---

### 💡 Presence Lights
**Version 1.0.13** | Automatically control lights based on presence - lights on when someone arrives, off when everyone leaves!

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fpresence_lights%2Fpresence_lights.yaml)

**Features:**
- 🏠 **Arrival Detection** - Lights on when someone comes home
- 👋 **Departure Detection** - Lights off when last person leaves
- 🌅 **Sun Awareness** - Only activates after sunset
- 👥 **Multi-Person** - Tracks multiple people
- 💡 **Flexible Control** - Control any light, switch, or group

**Requirements:** Person entities with device trackers, Light/switch entities, Zone entity

[📖 Full Documentation](https://github.com/r3mcos3/blueprints/tree/main/presence_lights)

---

### 🛡️ Persistent Motion Light
**Version 1.1** | Keep your lights ON as long as there's motion - with protection against manual turn-off!

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fpersistent_motion_light%2Fpersistent_motion_light.yaml)

**Features:**
- 🛡️ **Safety Feature** - Immediately re-activates if manually turned off during motion
- 🏃‍♂️ **Motion Detection** - Keeps lights on while motion is detected
- ⏳ **Configurable Wait Time** - Adjustable delay after motion stops
- 💡 **Flexible Control** - Works with lights and switches
- 🔄 **Restart Mode** - Seamlessly handles continuous motion detection

**Requirements:** Motion sensor, Light or switch entity

[📖 Full Documentation](https://github.com/r3mcos3/blueprints/tree/main/persistent_motion_light)

---

### ☀️ Sun-aware Motion Light
**Version 1.0** | Smart motion-activated lighting that adapts to the sun's position!

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fsun_aware_motion_light%2Fsun_aware_motion_light.yaml)

**Features:**
- 🏃‍♂️ **Motion Detection** - Automatically turns lights on when motion is detected
- ☀️ **Sun-Aware Mode** - Different brightness levels for day and night
- 🌓 **Flexible Brightness** - Customizable brightness for both day and night
- ⏱️ **Auto Turn-Off** - Configurable delay before lights turn off
- 🔆 **Default Brightness** - Option to use single brightness level
- 🔄 **Restart Mode** - Seamlessly handles continuous motion detection

**Requirements:** Motion sensor, Light entity, Sun integration (built-in)

[📖 Full Documentation](https://github.com/r3mcos3/blueprints/tree/main/sun_aware_motion_light)

---

## 🔔 Notifications & Updates

Stay informed with intelligent notification systems for updates and events.

### 📸 Camera Motion Snapshot
**Version 1.7.0** | Captures and sends a camera snapshot via Telegram when motion is detected!

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fcamera_motion_snapshot%2Fcamera_motion_snapshot.yaml)

**Features:**
- 📸 **Instant Snapshot** - Captures an image the moment motion is detected
- 🤖 **Telegram Integration** - Sends directly to your specified Telegram chat
- ✍️ **Custom Caption** - Fully customizable message accompanying the photo
- ⏱️ **Adjustable Timeout** - Prevent spam by setting a cooldown period between snapshots
- 💾 **Local Storage** - Saves snapshots to a configurable local path

**Requirements:** Camera entity, Motion sensor, Telegram Bot integration, Writable directory

[📖 Full Documentation](https://github.com/r3mcos3/blueprints/tree/main/camera_motion_snapshot)

---

### 🔄 Update Notifications (Android)
**Version 2.6.0** | Get notified about Home Assistant updates via Mobile App with actionable buttons!

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fupdate_notifications%2Fupdate_notifications.yaml)

> **⚠️ Platform Support:** This blueprint is specifically designed and tested for **Android devices only**.

**Features:**
- 📱 **Android Notifications** - Get notified on your Android device
- 🎛️ **3 Actionable Buttons** - Install, skip, or view changelog directly from notification
- ✅ **Completion Notifications** - Know when updates finish
- ⏳ **Progress Updates** - See when updates start
- 🔁 **Periodic Reminders** - Configurable reminders (5min - 24h intervals)
- ⚙️ **Config Check** - Run config check before core updates
- 💾 **Backup Support** - Create backup before updating

**Requirements:** Android device with Home Assistant Companion App, Update entities

[📖 Full Documentation](https://github.com/r3mcos3/blueprints/tree/main/update_notifications)

---

### 🔄 Telegram Update Notifications
**Version 1.3.0** | Get notified about Home Assistant updates via Telegram with inline keyboard buttons!

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Ftelegram_update_notifications%2Ftelegram_update_notifications.yaml)

**Features:**
- 💬 **Telegram Bot Integration** - Get notified via your Telegram bot
- 🎛️ **Inline Keyboard Buttons** - Install, skip, or view changelog directly from messages
- ✅ **Completion Notifications** - Know when updates finish
- ⏳ **Progress Updates** - See when updates start
- 🔁 **Periodic Reminders** - Configurable reminders (5min - 24h intervals)
- ⚙️ **Config Check** - Run config check before core updates
- 💾 **Backup Support** - Create backup before updating

**Requirements:** Telegram Bot (create via @BotFather), Telegram Integration, Update entities

[📖 Full Documentation](https://github.com/r3mcos3/blueprints/tree/main/telegram_update_notifications)

---

### ☀️ Sun Notifications
**Version 1.1.2** | Get notified at sunrise and sunset via Telegram with customizable messages and time offsets!

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fsun_notifications%2Fsun_notifications.yaml)

**Features:**
- 🌅 **Sunrise Notifications** - Get notified when the sun rises
- 🌇 **Sunset Notifications** - Get notified when the sun sets
- ⏰ **Time Offsets** - Set notifications before or after sunrise/sunset
- 💬 **Custom Messages** - Personalize your notification messages with templates
- ⚙️ **Independent Control** - Enable/disable sunrise and sunset notifications separately
- 🌍 **Automatic Calculation** - Uses your Home Assistant location for accurate times

**Requirements:** Telegram Bot, Telegram Integration, Sun integration (built-in)

[📖 Full Documentation](https://github.com/r3mcos3/blueprints/tree/main/sun_notifications)

---

## 🌡️ Climate & Energy

Intelligent climate control that saves energy while keeping you comfortable.

### 🔥 Smart Heating Controller
**Version 1.3.0** | Intelligent climate control with presence detection, door/window protection, and energy-saving features!

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fsmart_heating%2Fsmart_heating.yaml)

**Features:**
- 🌡️ **Smart Temperature Control** - Automatic heating management
- 🏠 **Presence Detection** - Lower temp when away
- 🚪 **Door/Window Protection** - Pause heating when open
- ⏰ **Scheduling** - Different temps for different times
- 🌙 **Night Mode** - Comfortable sleeping temperature
- 🔄 **HA Start & Reload Triggers** - Applies settings on restart
- 💰 **Energy Saving** - Reduce heating costs automatically

**Requirements:** Climate entity (thermostat), Optional: Door/window sensors, Presence sensors

[📖 Full Documentation](https://github.com/r3mcos3/blueprints/tree/main/smart_heating)

---

## 🔋 Battery & Power

Smart battery management to extend the lifespan of your devices.

### 🔋 Accu Saver
**Version 1.2.0** | Smart battery health management for laptop servers!

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Faccu_saver%2Faccu_saver.yaml)

**Features:**
- 🔋 **Battery Level Monitoring** - Dual threshold monitoring for optimal battery health
- ⚡ **Automatic Charge Control** - Smart plug integration for charging control
- 🎯 **Configurable Limits** - Set your own upper/lower battery thresholds
- 🔄 **Immediate Response** - No delays in charge control
- ⏰ **Periodic Status Checks** - Regular monitoring every 5 minutes
- 🛡️ **Protection** - Prevents overcharging and deep discharge
- 🚀 **Startup Sync** - Correct initial state on startup

**Requirements:** Battery percentage sensor, Smart plug or switch

[📖 Full Documentation](https://github.com/r3mcos3/blueprints/tree/main/accu_saver)

---

## 🔊 Media & Sound

Automate your media players and audio system for the perfect ambiance.

### 🔔 Doorbell Chime
**Version 1.0.4** | Play a chime sound on your media players when the doorbell rings!

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fdoorbell_chime%2Fdoorbell_chime.yaml)

**Features:**
- 🔊 **Adjustable Volume** - Set chime volume with optional restore
- 🔇 **Quiet Hours** - Respect do-not-disturb times
- 🎵 **Custom Sounds** - Use any audio file as your chime
- 📱 **Multiple Speakers** - Play on one or many media players
- 🚪 **Any Trigger** - Works with any doorbell sensor or button
- ⏱️ **Built-in Cooldown** - Prevent chime spam

**Requirements:** Media player entity, Doorbell sensor/button entity, Audio file accessible to HA

[📖 Full Documentation](https://github.com/r3mcos3/blueprints/tree/main/doorbell_chime)

---

### 🔈 Volume Control
**Version 1.0** | Automate volume control for all your speakers!

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fvolumecontrol%2Fvolumecontrol.yaml)

**Features:**
- 🔊 **Volume Automation** - Set volumes automatically
- 🕐 **Time-Based** - Different volumes at different times
- 📱 **Multiple Speakers** - Control multiple media players
- 🔇 **Quiet Hours** - Lower volume at night
- ⚙️ **Custom Actions** - Additional automation support

**Requirements:** Media player entities, Schedule helper

[📖 Full Documentation](https://github.com/r3mcos3/blueprints/tree/main/volumecontrol)

---

## 📦 Repository & Support

### GitHub Repository
All blueprints are open source and available on GitHub:
🔗 **[github.com/r3mcos3/blueprints](https://github.com/r3mcos3/blueprints)**

### Features
✅ **Version Control** - All blueprints use semantic versioning
✅ **Comprehensive Documentation** - Detailed README files for each blueprint
✅ **Easy Import** - One-click import buttons for all blueprints
✅ **Active Maintenance** - Regular updates and improvements
✅ **Community Driven** - Contributions welcome!

### Support & Feedback
- 🐛 **Report Issues**: [GitHub Issues](https://github.com/r3mcos3/blueprints/issues)
- 💡 **Feature Requests**: [GitHub Issues](https://github.com/r3mcos3/blueprints/issues)
- 🤝 **Contribute**: Pull requests welcome!

### Getting Started
1. Click the **Import Blueprint** button for any blueprint above
2. Configure the blueprint with your entities
3. Test and adjust to your needs
4. Check the documentation for advanced configuration

### Telegram Setup (For Telegram Blueprints)
Several blueprints use Telegram for notifications. Quick setup:
1. Create a bot via @BotFather on Telegram
2. Get your Chat ID by messaging your bot and visiting: `https://api.telegram.org/bot<TOKEN>/getUpdates`
3. Configure in Home Assistant `configuration.yaml`:
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

---

**Tags:** `automation`, `blueprints`, `collection`, `ai`, `lighting`, `notifications`, `climate`, `media-player`, `telegram`, `mobile-app`, `battery`

---

*Happy Automating! 🏠✨*

*If you find these blueprints useful, please ⭐ star the repository and share with the Home Assistant community!*
