# 🔔 Doorbell Chime

[![version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

Play a chime sound on your media players when the doorbell rings! Perfect for ensuring you never miss a visitor, even when you're in another room or have headphones on. 🔔

## ✨ Features

- 🔊 **Adjustable Volume** - Set the perfect chime volume for your space
- 🔄 **Volume Restore** - Automatically restores original volume after the chime
- 🌙 **Time-Based Conditions** - Only play during specific hours (quiet hours support)
- 🚫 **Do Not Disturb Mode** - Temporarily disable chimes with a helper toggle
- ⏱️ **Built-in Cooldown** - Prevents chime spam with single mode
- 📻 **Multi-Speaker Support** - Play on multiple media players, areas, or devices

## 📋 Requirements

Before using this blueprint, you need:

1. **Doorbell Sensor** - A binary sensor that detects doorbell presses
2. **Media Player(s)** - One or more speakers capable of playing audio
3. **Chime Sound File** - An audio file (MP3) in your Home Assistant media folder

### Setting Up a Chime Sound File

1. Navigate to **Media** in Home Assistant
2. Upload your chime sound file (e.g., `Chime.mp3`) to the local media folder
3. The default path will be: `media-source://media_source/local/Chime.mp3`

### Optional: Do Not Disturb Helper

1. Go to **Settings** → **Devices & Services** → **Helpers**
2. Click **+ CREATE HELPER** → **Toggle**
3. Name it (e.g., "Doorbell Do Not Disturb")
4. When turned ON, the doorbell chime will be silenced

## 🚀 Installation

### Automatic Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fdoorbell_chime%2Fdoorbell_chime.yaml)

### Manual Installation

1. In Home Assistant, navigate to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click the **Import Blueprint** button
3. Enter the blueprint URL:
   ```
   https://github.com/r3mcos3/blueprints/blob/main/doorbell_chime/doorbell_chime.yaml
   ```
4. Click **Preview** and then **Import**

## ⚙️ Configuration

When creating an automation from this blueprint, you'll configure:

| Parameter | Description | Default |
|-----------|-------------|---------|
| 🔔 Doorbell Sensor | Binary sensor for doorbell detection | Required |
| 🔊 Media Players | Target speakers for the chime | Required |
| 🎵 Media File | Path to chime sound file | `media-source://media_source/local/Chime.mp3` |
| 🔉 Chime Volume | Volume level for chime (0.0-1.0) | 0.5 (50%) |
| 🔄 Restore Volume | Restore original volume after chime | Yes |
| 🌙 Enable Time Condition | Only play during specific hours | No |
| ⏰ Start Time | When chime is allowed to start | 08:00 |
| ⏰ End Time | When chime stops being allowed | 22:00 |
| 🚫 Enable Do Not Disturb | Use a helper to silence chimes | No |
| 🚫 Do Not Disturb Helper | Toggle entity to control DND | None |

## 💡 Usage Examples

### Example 1: Simple Doorbell Chime

Basic setup for whole-house notification:

```yaml
Doorbell Sensor: binary_sensor.front_door_doorbell
Media Players: media_player.living_room, media_player.kitchen
Chime Volume: 0.6 (60%)
Restore Volume: Yes
```

Result: When doorbell rings, all selected speakers play the chime at 60% volume, then restore to original volume.

### Example 2: With Quiet Hours

Respect sleeping schedules:

```yaml
Doorbell Sensor: binary_sensor.front_door_doorbell
Media Players: media_player.living_room
Chime Volume: 0.5 (50%)
Enable Time Condition: Yes
Start Time: 08:00
End Time: 22:00
```

Result: Chime only plays between 8 AM and 10 PM. No sound during night hours.

### Example 3: With Do Not Disturb

Manual control for meetings or focus time:

```yaml
Doorbell Sensor: binary_sensor.front_door_doorbell
Media Players: media_player.office
Chime Volume: 0.4 (40%)
Enable Do Not Disturb: Yes
Do Not Disturb Helper: input_boolean.doorbell_dnd
```

Result: Chime plays unless you've turned on the DND toggle. Perfect for video calls!

### Example 4: Full Featured Setup

All features combined:

```yaml
Doorbell Sensor: binary_sensor.front_door_doorbell
Media Players: area.living_room (all speakers in area)
Chime Volume: 0.5 (50%)
Restore Volume: Yes
Enable Time Condition: Yes
Start Time: 07:00
End Time: 23:00
Enable Do Not Disturb: Yes
Do Not Disturb Helper: input_boolean.doorbell_dnd
```

Result: Complete doorbell notification system with time restrictions and manual override capability.

## 🔧 Troubleshooting

### Chime Doesn't Play

1. Verify your doorbell sensor triggers correctly (check in Developer Tools → States)
2. Test media file path by manually playing it via Developer Tools → Services
3. Ensure media player supports `media_player.play_media` service
4. Check Home Assistant logs for any errors

### Volume Not Restoring

1. Ensure "Restore Volume" is enabled
2. Some media players may not report volume level correctly
3. Check that the 3-second delay is sufficient for your chime sound
4. Verify media player supports `media_player.volume_set` service

### Time Condition Not Working

1. Verify "Enable Time Condition" is set to Yes
2. Check start and end times are configured correctly
3. Note: If end time is before start time, it wraps around midnight
4. Check your Home Assistant timezone settings

### Do Not Disturb Not Working

1. Ensure "Enable Do Not Disturb" is set to Yes
2. Verify the helper entity is correctly selected
3. Check the helper state in Developer Tools → States
4. DND should be "on" to silence, "off" to allow chimes

### Multiple Chimes Playing

The blueprint uses `mode: single` to prevent overlapping chimes. If you hear multiple chimes:
1. Check if you have multiple automations using this blueprint
2. Verify the doorbell sensor isn't bouncing (multiple triggers)
3. Consider adding a cooldown to your doorbell sensor

## 📝 Version History

### Version 1.0.0 (2025-12-16)
- 🎉 Initial release
- 🔔 Doorbell sensor trigger support
- 🔊 Adjustable volume with restore option
- 🌙 Time-based condition (quiet hours)
- 🚫 Do Not Disturb mode with helper toggle
- 📻 Multi-target support (entities, areas, devices)

## 🤝 Contributing

Found a bug or have a suggestion? Please [open an issue](https://github.com/r3mcos3/blueprints/issues) on GitHub!

## 📄 License

This blueprint is provided as-is under the MIT License.

## 🙏 Credits

Created by [r3mcos3](https://github.com/r3mcos3)
