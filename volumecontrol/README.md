# 🔈 Volume Control

[![version](https://img.shields.io/badge/version-1.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

This blueprint automates volume control for your media players based on a schedule. Perfect for automatically adjusting speaker volume during different times of the day, like quiet hours at night or louder volume during the day! 🔊

## ✨ Features

- 🗓️ **Schedule-Based Control** - Automatically adjusts volume based on your schedule
- 🔊 **Dual Volume Levels** - Set different volumes for high and low periods
- 📻 **Multi-Speaker Support** - Control multiple media players simultaneously
- 🎬 **Custom Actions** - Execute additional actions when schedule changes
- ⚙️ **Simple Configuration** - Easy slider-based volume settings
- 🔄 **Single Mode** - Prevents overlapping executions

## 📋 Requirements

Before using this blueprint, you need:

1. **Media Player Entities** - One or more media players that support volume control
2. **Schedule Helper** - A schedule entity to control timing

### Setting Up a Schedule Helper

1. Go to **Settings** → **Devices & Services** → **Helpers**
2. Click **+ CREATE HELPER** → **Schedule**
3. Name it (e.g., "Quiet Hours" or "Loud Hours")
4. Configure your time periods:
   - When schedule is **ON**: Volume will be set to "Volume Up Level"
   - When schedule is **OFF**: Volume will be set to "Volume Down Level"

📚 [More information about schedules](https://www.home-assistant.io/integrations/schedule/)

## 🚀 Installation

### Automatic Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fvolumecontrol%2Fvolumecontrol.yaml)

### Manual Installation

1. In Home Assistant, navigate to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click the **Import Blueprint** button
3. Enter the blueprint URL:
   ```
   https://github.com/r3mcos3/blueprints/blob/main/volumecontrol/volumecontrol.yaml
   ```
4. Click **Preview** and then **Import**

## ⚙️ Configuration

When creating an automation from this blueprint, you'll configure:

| Parameter | Description | Default |
|-----------|-------------|---------|
| 📻 Media Players | Speakers or media players to control | - |
| 🗓️ Scheduler | Schedule entity that triggers volume changes | - |
| 🔊 Volume Up Level | Volume level when schedule turns ON (0.1-1.0) | 0.6 (60%) |
| 🔈 Volume Down Level | Volume level when schedule turns OFF (0.1-1.0) | 0.2 (20%) |
| 🎬 Custom Action | Optional additional action to execute | None |

## 💡 Usage Examples

### Example 1: Nighttime Quiet Hours

Automatically lower volume during the night:

```yaml
Media Players: media_player.living_room, media_player.bedroom
Scheduler: schedule.quiet_hours (ON from 10:00 PM to 8:00 AM)
Volume Up Level: 0.6 (60%)
Volume Down Level: 0.2 (20%)
```

Result: At 10 PM, all speakers lower to 20%. At 8 AM, they increase to 60%.

### Example 2: Weekend Party Mode

Boost volume on weekend afternoons:

```yaml
Media Players: media_player.living_room, media_player.kitchen
Scheduler: schedule.weekend_daytime (ON Sat-Sun 12:00 PM to 6:00 PM)
Volume Up Level: 0.8 (80%)
Volume Down Level: 0.4 (40%)
```

Result: Weekend afternoons automatically boost volume to 80% for entertaining, return to 40% after.

### Example 3: Work Focus Hours

Keep office speakers quiet during work hours:

```yaml
Media Players: media_player.office
Scheduler: schedule.focus_time (ON weekdays 9:00 AM to 5:00 PM)
Volume Up Level: 0.3 (30%)
Volume Down Level: 0.6 (60%)
```

Result: During work hours, office speaker stays at 30% for concentration. Outside work hours, louder at 60%.

### Example 4: With Custom Action

Add scene activation when volume changes:

```yaml
Media Players: media_player.living_room
Scheduler: schedule.morning_routine (ON at 7:00 AM)
Volume Up Level: 0.5 (50%)
Custom Action:
  - service: scene.turn_on
    target:
      entity_id: scene.morning_lights
  - service: notify.mobile_app
    data:
      message: "Good morning! Volume adjusted."
```

Result: At 7 AM, speaker volume increases AND morning scene activates with notification.

## 🔧 Troubleshooting

### Volume Doesn't Change

1. Verify your media player supports `media_player.volume_set` service
2. Check that the schedule entity is working correctly
3. Test manually changing the schedule to see if it triggers
4. Check Home Assistant logs for any errors

### Schedule Not Triggering

1. Ensure your schedule helper is properly configured
2. Verify the schedule has active time periods defined
3. Check schedule state in Developer Tools → States
4. Look at Home Assistant automation traces for debugging

### Wrong Volume Level

1. Volume uses 0.0-1.0 scale (not 0-100)
   - 0.1 = 10%
   - 0.5 = 50%
   - 1.0 = 100%
2. Verify your volume_up and volume_down settings
3. Some speakers may have hardware volume limits

### Custom Action Not Executing

1. Check that custom action syntax is correct
2. Verify custom action is not set to empty/none
3. Look at automation traces for action execution
4. Check logs for any action-specific errors

## screenshot

<img width="1049" height="664" alt="Screenshot 2025-12-24 074702" src="https://github.com/user-attachments/assets/456d39df-a0c5-4170-b178-de6dc89ec779" />


## 📝 Version History

### Version 1.0 (2025-12-15)
- 🎉 Initial release
- 🗓️ Schedule-based volume control
- 🔊 Dual volume level support
- 📻 Multi-speaker support
- 🎬 Custom action integration

## 🤝 Contributing

Found a bug or have a suggestion? Please [open an issue](https://github.com/r3mcos3/blueprints/issues) on GitHub!

## 📄 License

This blueprint is provided as-is under the MIT License.

## 🙏 Credits

Created by [r3mcos3](https://github.com/r3mcos3)
