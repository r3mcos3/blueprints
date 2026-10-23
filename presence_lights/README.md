# 💡 Presence - Home/Away Lights

[![version](https://img.shields.io/badge/version-1.1.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

This blueprint automatically controls your lights based on presence detection. Lights turn on when someone arrives home after sunset, and turn off when the last person leaves. Perfect for a welcoming home and energy savings! 💡

## ✨ Features

- 🏠 **Presence-Based Control** - Automatically responds to arrivals and departures
- 🌅 **Sunset-Aware** - Only turns on lights after sunset for energy efficiency
- ✨ **Customizable Brightness** - Set your preferred arrival brightness level
- 🔌 **Flexible Turn-Off Options** - Choose to turn off all lights or just specific ones
- 👥 **Multi-Person Support** - Works with multiple people: lights turn on when the first person arrives and turn off when the last person leaves
- 🔄 **Restart Mode** - Seamlessly handles overlapping arrivals and departures

## 📋 Requirements

Before using this blueprint, you need:

1. **Zone Entity** - A zone entity to monitor for presence (typically `zone.home`)
2. **Light Entities** - One or more light entities to control
3. **Person Tracking** - Person entities configured in Home Assistant

## 🚀 Installation

### Automatic Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fpresence_lights%2Fpresence_lights.yaml)

### Manual Installation

1. In Home Assistant, navigate to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click the **Import Blueprint** button
3. Enter the blueprint URL:
   ```
   https://github.com/r3mcos3/blueprints/blob/main/presence_lights/presence_lights.yaml
   ```
4. Click **Preview** and then **Import**

## ⚙️ Configuration

When creating an automation from this blueprint, you'll configure:

| Parameter | Description | Default |
|-----------|-------------|---------|
| 💡 Target Lights | Lights to control based on presence | - |
| 🏠 Presence Zone | Zone to monitor for arrivals/departures | - |
| ✨ Arrival Brightness | Brightness percentage when lights turn on (1-100%) | 33% |
| 🔌 Turn off all lights on departure | If enabled, turns off ALL lights when leaving | false |

## 💡 Usage Examples

### Example 1: Basic Home Welcome

Simple setup for welcoming lights:

```yaml
Target Lights: light.living_room, light.hallway, light.kitchen
Presence Zone: zone.home
Arrival Brightness: 50%
Turn off all lights: No
```

Result: When arriving home after dark, living room, hallway, and kitchen turn on at 50%. When leaving, only these lights turn off.

### Example 2: Complete Home Shutdown

Ensure everything is off when leaving:

```yaml
Target Lights: light.entrance, light.hallway
Presence Zone: zone.home
Arrival Brightness: 80%
Turn off all lights: Yes
```

Result: Entrance and hallway turn on bright when arriving. When leaving, ALL lights in the house turn off for complete energy savings.

### Example 3: Subtle Welcome

Low-brightness for a gentle welcome:

```yaml
Target Lights: light.pathway, light.porch
Presence Zone: zone.home
Arrival Brightness: 20%
Turn off all lights: No
```

Result: Pathway and porch lights create a subtle, low-brightness welcome after sunset.

## 🔧 Troubleshooting

### Lights Turn On During Daytime

1. This shouldn't happen - verify that your `sun.sun` entity is working correctly
2. Check the sun elevation in Developer Tools → States
3. Ensure Home Assistant has correct timezone and location settings

### Lights Don't Turn Off When Leaving

1. Verify that person entities are properly tracked in the zone
2. Check your zone configuration in Home Assistant
3. Ensure all household members have person entities configured
4. Test by checking zone.home state in Developer Tools

### Lights Turn Off While Someone Is Still Home

1. Ensure all household members have person entities configured
2. Check that all person entities are tracked by the zone
3. Verify device_tracker entities for each person are working
4. Check that person entities show correct location

### Wrong Brightness Level

1. Verify the brightness percentage is set correctly (1-100)
2. Check that your lights support brightness control
3. Some lights may have minimum brightness limits

## 📝 Version History

### Version 1.1.0
- 🐛 Fixed: arrival brightness 0% switched the lights off — the minimum is now 1%
- 🔧 Modernized syntax (`triggers`/`actions`, `action:` instead of the deprecated `service:`, `filter` entity selector)
- 📝 Documentation: lights turn on for the *first* person arriving (zone goes from 0 to 1+)

### Version 1.0.13 (2025-12-15)
- 🐛 Fix boolean filter issue

### Version 1.0.12 and earlier
- Various improvements and bug fixes

### Version 1.0.0
- 🎉 Initial release
- 🏠 Presence-based light control
- 🌅 Sunset-aware triggering
- ✨ Customizable brightness
- 🔌 Flexible turn-off options

## 🤝 Contributing

Found a bug or have a suggestion? Please [open an issue](https://github.com/r3mcos3/blueprints/issues) on GitHub!

## 📄 License

This blueprint is provided as-is under the MIT License.

## 🙏 Credits

Created by [r3mcos3](https://github.com/r3mcos3)
