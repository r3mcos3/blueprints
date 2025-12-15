# 💡 Presence - Home/Away Lights

**Version:** 1.0.13

This Home Assistant blueprint automatically controls your lights based on presence detection. Lights turn on when someone arrives home after sunset, and turn off when the last person leaves.

## 📋 Description

When you arrive home after sunset, this automation:
1. 🏠 Detects arrival in your configured zone
2. 🌅 Checks if the sun is below the horizon
3. 💡 Turns on specified lights with custom brightness
4. 🚪 Turns off lights when everyone leaves (with option to turn off all lights)

## ✅ Requirements

Before using this blueprint, you need:

### 1. 🏠 Zone Entity
- A zone entity to monitor for presence (typically `zone.home`)
- This is usually configured by default in Home Assistant

### 2. 💡 Light Entities
- One or more light entities to control
- These can be individual lights, groups, or areas

## 🚀 Installation

1. Navigate to **Settings** → **Automations & Scenes** → **Blueprints** in Home Assistant
2. Click **"Import Blueprint"**
3. Enter the URL:
   ```
   https://raw.githubusercontent.com/r3mcos3/blueprints/main/presence_lights/presence_lights.yaml
   ```
4. Click **"Preview"** and then **"Import Blueprint"**

## ⚙️ Configuration

### Required Settings

| Setting | Description | Example |
|---------|-------------|---------|
| 💡 Target Lights | Lights to control based on presence | `light.living_room`, `light.hallway` |
| 🏠 Presence Zone | Zone to monitor for arrivals/departures | `zone.home` |

### Optional Settings

| Setting | Description | Default |
|---------|-------------|---------|
| ✨ Arrival Brightness | Brightness percentage when lights turn on | 33% |
| 🔌 Turn off all lights on departure | If enabled, turns off ALL lights (not just selected ones) | false |

## 🎯 How It Works

### Arrival (After Sunset)
- **Trigger:** Someone enters the configured zone
- **Condition:** Sun is below the horizon
- **Action:** Turn on selected lights at configured brightness

### Departure
- **Trigger:** Last person leaves the zone
- **Action:**
  - If "Turn off all lights" is **enabled**: Turns off ALL lights in your home
  - If "Turn off all lights" is **disabled**: Only turns off the selected target lights

## 💡 Tips

- **Arrival Brightness**: Set to 33% for a gentle welcome, or higher for brighter lighting
- **Turn Off All Lights**: Useful if you want to ensure everything is off when leaving home
- **Multiple People**: Works automatically with multiple people - lights only turn off when the LAST person leaves
- **Daytime Arrivals**: Lights will NOT turn on during daytime (sun above horizon)

## 📖 Examples

### Example 1: Basic Home Arrival
- **Target Lights:** Living room, hallway, kitchen
- **Zone:** zone.home
- **Brightness:** 50%
- **Turn off all:** No

Result: When arriving home after dark, living room, hallway, and kitchen turn on at 50%. When leaving, only these lights turn off.

### Example 2: Complete Shutdown
- **Target Lights:** Entrance lights
- **Zone:** zone.home
- **Brightness:** 80%
- **Turn off all:** Yes

Result: Entrance lights turn on bright when arriving. When leaving, ALL lights in the house turn off.

### Example 3: Subtle Welcome
- **Target Lights:** Pathway lights, porch light
- **Zone:** zone.home
- **Brightness:** 20%
- **Turn off all:** No

Result: Low-brightness pathway and porch lights create a subtle welcome.

## 🔧 Troubleshooting

### Lights turn on during the day
- This shouldn't happen - the blueprint checks if the sun is below the horizon
- Verify that your `sun.sun` entity is working correctly

### Lights don't turn off when leaving
- Check that people are properly tracked in the zone
- Verify your zone configuration in Home Assistant
- Make sure person entities are correctly set up

### Lights turn off while someone is still home
- Ensure all household members have person entities configured
- Check that all person entities are included in your zone

## 📝 Version History

- **1.0.13** (Current): Latest stable version with boolean filter fix
- Earlier versions: Various improvements and bug fixes

## 🤝 Contributing

Found a bug or have a suggestion? Please open an issue on the [GitHub repository](https://github.com/r3mcos3/blueprints).

## 📄 License

This blueprint is licensed under the MIT License.
