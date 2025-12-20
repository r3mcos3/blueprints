# ☀️ Sun-aware Motion Light

[![version](https://img.shields.io/badge/version-1.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

Smart motion-activated lighting that adapts to the sun's position! Turn on lights when motion is detected with different brightness levels for day and night. Perfect for hallways, bathrooms, and outdoor areas! 💡

## ✨ Features

- 🏃‍♂️ **Motion Detection** - Automatically turns lights on when motion is detected
- ☀️ **Sun-Aware Mode** - Different brightness levels for day and night
- 🌓 **Flexible Brightness** - Customizable brightness for both day and night
- ⏱️ **Auto Turn-Off** - Configurable delay before lights turn off
- 🔆 **Default Brightness** - Option to use single brightness level instead of sun-aware mode
- 🔄 **Restart Mode** - Seamlessly handles continuous motion detection

## 📋 Requirements

Before using this blueprint, you need:

1. **Motion Sensor** - A binary sensor with device class `motion`
2. **Light Entity** - One or more lights to control
3. **Sun Integration** - Built-in Home Assistant sun integration (automatically available)

## 🚀 Installation

### Automatic Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fsun_aware_motion_light%2Fsun_aware_motion_light.yaml)

### Manual Installation

1. In Home Assistant, navigate to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click the **Import Blueprint** button
3. Enter the blueprint URL:
   ```
   https://github.com/r3mcos3/blueprints/blob/main/sun_aware_motion_light/sun_aware_motion_light.yaml
   ```
4. Click **Preview** and then **Import**

## ⚙️ Configuration

When creating an automation from this blueprint, you'll configure:

| Parameter | Description | Default |
|-----------|-------------|---------|
| 🏃‍♂️ Motion Sensor | Binary sensor that detects motion | Required |
| 💡 Target Light | Light or group of lights to control | Required |
| 🔆 Default Brightness | Brightness when sun-aware mode is disabled | 80% |
| ☀️ Sun-aware Mode | Enable different brightness for day/night | Enabled |
| ☀️ Brightness (Day) | Brightness when sun is above horizon | 100% |
| 🌙 Brightness (Night) | Brightness when sun is below horizon | 10% |
| ⏱️ Turn-off Delay | Minutes before turning off after no motion | 5 min |

## 💡 Usage Examples

### Example 1: Hallway Light

Bright during day, dim at night:

```yaml
automation:
  - alias: "Hallway Motion Light"
    use_blueprint:
      path: r3mcos3/sun_aware_motion_light
      input:
        motion_sensor: binary_sensor.hallway_motion
        target_light: light.hallway
        sun_aware_enabled: true
        brightness_day: 100
        brightness_night: 10
        turn_off_delay: 3
```

**Expected Behavior:**
- Motion detected during day: 100% brightness
- Motion detected at night: 10% brightness
- Lights turn off after 3 minutes of no motion

### Example 2: Bathroom with Single Brightness

Always the same brightness, regardless of time:

```yaml
automation:
  - alias: "Bathroom Motion Light"
    use_blueprint:
      path: r3mcos3/sun_aware_motion_light
      input:
        motion_sensor: binary_sensor.bathroom_motion
        target_light: light.bathroom
        sun_aware_enabled: false
        default_brightness: 70
        turn_off_delay: 5
```

**Expected Behavior:**
- Motion detected: 70% brightness (any time of day)
- Lights turn off after 5 minutes of no motion

### Example 3: Outdoor Path Light

Adaptive lighting for outdoor areas:

```yaml
automation:
  - alias: "Outdoor Path Light"
    use_blueprint:
      path: r3mcos3/sun_aware_motion_light
      input:
        motion_sensor: binary_sensor.path_motion
        target_light: light.path_lights
        sun_aware_enabled: true
        brightness_day: 50
        brightness_night: 30
        turn_off_delay: 2
```

**Expected Behavior:**
- Motion during day: 50% brightness (enough visibility)
- Motion at night: 30% brightness (safety lighting)
- Quick turn-off after 2 minutes to save energy

### Example 4: Multi-Light Group

Control multiple lights together:

```yaml
automation:
  - alias: "Living Room Motion Lights"
    use_blueprint:
      path: r3mcos3/sun_aware_motion_light
      input:
        motion_sensor: binary_sensor.living_room_motion
        target_light:
          - light.living_room_ceiling
          - light.living_room_floor_lamp
        sun_aware_enabled: true
        brightness_day: 80
        brightness_night: 20
        turn_off_delay: 10
```

**Expected Behavior:**
- Both lights turn on together with appropriate brightness
- Extended 10-minute delay for longer activities

## 🔧 Troubleshooting

### Lights Not Turning On

1. Check motion sensor is working in Developer Tools → States
2. Verify motion sensor device class is set to `motion`
3. Ensure light entity is available and controllable
4. Check automation is enabled in Settings → Automations

### Wrong Brightness Level

1. Verify sun-aware mode setting (enabled/disabled)
2. Check current sun position in Developer Tools → States → `sun.sun`
3. Ensure brightness values are set correctly (0-100%)
4. Test by manually triggering the motion sensor

### Lights Not Turning Off

1. Check turn-off delay is not set to 0
2. Verify motion sensor returns to "off" state
3. Ensure no other automations are controlling the same lights
4. Check automation traces for debugging

### Sun-Aware Mode Not Working

1. Verify sun integration is working (`sun.sun` entity exists)
2. Check Home Assistant has correct location and timezone configured
3. Test by checking sun state during day and night
4. Ensure "Sun-aware Mode" toggle is enabled in configuration

## 📝 Version History

### Version 1.0 (2025-12-15)
- 🎉 Initial release
- 🏃‍♂️ Motion-activated light control
- ☀️ Sun-aware brightness modes
- 🌓 Day/night brightness customization
- ⏱️ Configurable turn-off delay
- 🔆 Optional single brightness mode

## 🤝 Contributing

Found a bug or have a suggestion? Please [open an issue](https://github.com/r3mcos3/blueprints/issues) on GitHub!

## 📄 License

This blueprint is provided as-is under the MIT License.

## 🙏 Credits

Created by [r3mcos3](https://github.com/r3mcos3)
