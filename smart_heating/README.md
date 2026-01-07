# 🔥 Smart Heating Controller

[![version](https://img.shields.io/badge/version-1.3.1-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

Intelligent climate control that adapts to your presence, outdoor conditions, door/window states, and time schedules. Save energy while maintaining comfort with smart temperature management! 🌡️

## ✨ Features

- 🏠 **Presence-Based Control** - Automatically adjusts temperature when you arrive or leave home
- 🌡️ **Outdoor Temperature Factor** - Disables heating when it's warm outside to save energy
- 🚪 **Door/Window Protection** - Pauses heating when doors/windows are open too long
- 🌙 **Night Mode** - Reduces temperature during sleeping hours for comfort and efficiency
- ⏰ **Smart Pre-Heating** - Starts heating before you wake up to reach comfort temperature on time
- 🧊 **Frost Protection** - Maintains minimum temperature to prevent pipe freezing
- 💧 **Humidity Compensation** - Adjusts target temperature based on indoor humidity levels (optional)
- 🔄 **Automatic Synchronization** - Checks and updates heating state every 15 minutes

## 📋 Requirements

Before using this blueprint, you need:

1. **Climate Entity** - A thermostat or climate device (e.g., `climate.tado`)
2. **Temperature Sensors**:
   - Indoor temperature sensor (e.g., `sensor.indoor_temperature`)
   - Outdoor temperature sensor (e.g., `sensor.outdoor_temperature`)
3. **Presence Detection** - A zone entity for home presence (typically `zone.home`)
4. **Door/Window Sensors** - Binary sensors for monitoring doors and windows

### Optional Components

- **Humidity Sensor** - For humidity-based temperature adjustments

## 🚀 Installation

### Automatic Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fsmart_heating%2Fsmart_heating.yaml)

### Manual Installation

1. In Home Assistant, navigate to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click the **Import Blueprint** button
3. Enter the blueprint URL:
   ```
   https://github.com/r3mcos3/blueprints/blob/main/smart_heating/smart_heating.yaml
   ```
4. Click **Preview** and then **Import**

## ⚙️ Configuration

### Required Settings

| Parameter | Description | Example |
|-----------|-------------|---------|
| 🌡️ Climate Entity | The thermostat or climate entity to control | `climate.tado` |
| 🏠 Indoor Temperature Sensor | Sensor measuring indoor temperature | `sensor.indoor_temp` |
| 🌤️ Outdoor Temperature Sensor | Sensor measuring outdoor temperature | `sensor.outdoor_temp` |
| 👥 Presence Zone | Zone to monitor for presence | `zone.home` |
| 🚪 Door/Window Sensors | Binary sensors for doors and windows | `binary_sensor.front_door` |

### 🌡️ Temperature Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 🏠 Comfort Temperature | Target when people are home | 21°C |
| 🏃 Away Temperature | Target when nobody is home | 17°C |
| ❄️ Frost Protection Temperature | Minimum temperature to prevent freezing | 7°C |
| 🌙 Night Temperature | Target during sleeping hours | 18°C |
| 🌡️ Outdoor Temperature Threshold | Disable heating when outdoor exceeds this | 18°C |

### 🚪 Door/Window Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| ⏱️ Door Open Delay | Wait time before pausing heating | 120 seconds |
| ⏱️ Door Closed Resume Delay | Wait time before resuming heating | 60 seconds |

### 🌙 Night Mode Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 🌙 Enable Night Mode | Automatic temperature reduction during sleep | true |
| 🌙 Night Start Time | When night mode begins | 23:00 |
| ☀️ Night End Time | When night mode ends | 07:00 |
| ⏰ Enable Pre-heating | Start heating before wake-up time | true |
| ⏰ Pre-heat Duration | Minutes before night end to start pre-heating | 30 minutes |

### 💧 Humidity Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 💧 Enable Humidity Factor | Adjust temperature based on humidity | false |
| 💧 Humidity Sensor | Indoor humidity sensor (optional) | - |

**Humidity Adjustments:**
- High humidity (>70%): -0.5°C (feels warmer)
- Low humidity (<30%): +0.5°C (feels colder)
- Normal humidity (30-70%): No adjustment

## 🎯 How It Works

The **Smart Heating Controller** is built as a **hierarchy of priorities**. This means that certain conditions (like frost protection) always take precedence over comfort settings (like night temperature).

Here is a step-by-step explanation of how the controller decides what the temperature should be:

### 1. The Decision Hierarchy (From Highest to Lowest Priority)
The blueprint checks the situation in this exact order. As soon as a condition is 'true', that action is executed and the decision-making stops for that moment.

1.  **❄️ Frost Protection (Highest Priority):**
    *   *If* the indoor temperature is dangerously low (below the set frost threshold, default 7°C), the heating turns **on immediately** at that minimum temperature, regardless of whether windows are open or no one is home. Safety comes first.

2.  **🛠️ Manual Override:**
    *   *If* you have turned on the 'Override Helper' (a switch in Home Assistant), the automation ignores the normal schedule.
    *   This remains active for the set duration (default 2 hours) or until you turn it off again.
    *   *Exception:* If you leave the house (`left_home`), the override is automatically cancelled to prevent energy waste.

3.  **☀️ Eco Mode (Warm Outside):**
    *   *If* it is warmer outside than the set threshold value (default 18°C), the heating is completely **switched off** (HVAC mode: off). It makes no sense to heat if it is already warm enough outside.

4.  **🚪 Windows/Doors Open:**
    *   *If* a window or door is open longer than the 'delay time' (default 120 sec), the heating drops to the frost protection temperature.
    *   This prevents heating the outdoors. As soon as everything is closed again, the normal program resumes after a short wait.

5.  **🏃 Away:**
    *   *If* no one is home (detected via the `presence_zone`), the thermostat goes to the 'Away Temperature' (default 17°C).

6.  **⏰ Pre-heat:**
    *   *If* the night is almost over (within the set 'Pre-heat Duration', e.g., 30 min before waking up), the heating starts heating up to the comfort temperature. So you wake up in a warm house.

7.  **🌙 Night Mode:**
    *   *If* it is night (between start and end time, e.g., 23:00 - 07:00), the temperature goes to the 'Night Temperature' (default 18°C) to save energy during sleep.

8.  **🏠 Comfort (Default):**
    *   *If* none of the above situations apply (you are home, windows closed, it is daytime, and cold outside), the heating is set to the 'Comfort Temperature' (default 21°C).

### 💧 Smart Extra: Humidity Correction
If you enable this, the system subtly adjusts the target temperature based on humidity:
*   **High humidity (>70%):** The temperature is **lowered by 0.5°C**. Humid air feels warmer, so you can save energy without losing comfort.
*   **Low humidity (<30%):** The temperature is **raised by 0.5°C**, because dry air feels colder.

### 🔄 When does the automation react?
The blueprint springs into action with every relevant change:
*   Someone comes home or leaves.
*   A window/door opens or closes.
*   The temperature (indoor or outdoor) changes.
*   The clock hits a start/end time (night mode).
*   Home Assistant restarts.
*   **Every 15 minutes:** A periodic check to ensure everything is still in the correct state (e.g., if someone manually adjusted the thermostat).

## 💡 Usage Examples

### Example 1: Basic Setup

Minimal configuration for getting started:

```yaml
automation:
  - alias: "Smart Heating - Living Room"
    use_blueprint:
      path: r3mcos3/smart_heating
      input:
        climate_entity: climate.living_room_thermostat
        indoor_temp_sensor: sensor.living_room_temperature
        outdoor_temp_sensor: sensor.outdoor_temperature
        presence_zone: zone.home
        door_window_sensors:
          - binary_sensor.front_door
          - binary_sensor.back_door
          - binary_sensor.living_room_window
```

**Expected Behavior:**
- Comfort temperature (21°C) when home
- Away temperature (17°C) when away
- Night temperature (18°C) during 23:00-07:00
- Heating pauses if doors/windows open >2 minutes
- Pre-heating starts 30 minutes before 07:00

### Example 2: Advanced Configuration

With humidity compensation:

```yaml
automation:
  - alias: "Smart Heating - Advanced"
    use_blueprint:
      path: r3mcos3/smart_heating
      input:
        climate_entity: climate.main_thermostat
        indoor_temp_sensor: sensor.indoor_temp
        outdoor_temp_sensor: sensor.weather_temperature
        presence_zone: zone.home
        door_window_sensors:
          - binary_sensor.front_door
          - binary_sensor.back_door
        comfort_temp: 22
        away_temp: 16
        night_temp: 19
        outdoor_temp_threshold: 16
        use_humidity: true
        humidity_sensor: sensor.indoor_humidity
        preheat_minutes: 45
```

**Expected Behavior:**
- Custom temperatures (22°C comfort, 16°C away, 19°C night)
- Eco mode when outdoor >16°C
- Temperature adjusts ±0.5°C based on humidity
- Pre-heating starts 45 minutes early (06:15)

### Example 3: Energy Saving Focus

Optimized for maximum energy savings:

```yaml
automation:
  - alias: "Smart Heating - Energy Saver"
    use_blueprint:
      path: r3mcos3/smart_heating
      input:
        climate_entity: climate.heating
        indoor_temp_sensor: sensor.temperature
        outdoor_temp_sensor: sensor.outdoor_temp
        presence_zone: zone.home
        door_window_sensors:
          - binary_sensor.all_doors
        comfort_temp: 20
        away_temp: 15
        night_temp: 17
        outdoor_temp_threshold: 15
        use_night_mode: true
        night_start: "22:00:00"
        night_end: "08:00:00"
        use_preheat: false
        door_open_delay: 60
```

**Expected Behavior:**
- Lower comfort temperature (20°C)
- Aggressive away mode (15°C)
- Extended night mode (22:00-08:00)
- No pre-heating (saves energy)
- Quick door detection (1 minute)
- Lower outdoor threshold (15°C)

## 🔧 Troubleshooting

### Heating Not Switching Modes

1. Check automation is enabled in Home Assistant
2. Verify all required entities exist and are working
3. Check automation traces: Settings → Automations → Smart Heating → Traces
4. Ensure presence zone is correctly reporting occupancy count
5. Check if outdoor temperature is above threshold (causing eco mode)

### Door/Window Detection Not Working

1. Verify binary sensors are in correct state (`on` = open, `off` = closed)
2. Check sensor device_class is set to `door`, `window`, or `opening`
3. Ensure door_open_delay matches your needs (default 120 seconds)
4. Test by opening a door/window and waiting for the configured delay
5. Check automation traces to see if triggers are firing

### Night Mode Not Activating

1. Verify "Enable Night Mode" is turned on in settings
2. Check night start/end times are configured correctly
3. Ensure someone is home (night mode requires presence)
4. For times spanning midnight, the blueprint handles wraparound automatically
5. Check automation traces around the configured night start time

### Pre-Heating Not Working

1. Verify both "Enable Night Mode" and "Enable Pre-heating" are on
2. Check pre-heat duration setting (default 30 minutes)
3. Ensure you're home during pre-heat time (requires presence)
4. Pre-heating triggers on periodic checks (every 15 minutes)
5. Verify indoor temperature is below comfort temperature

### Temperature Not Adjusting

1. Check climate entity is responding to commands
2. Test manually setting temperature via Developer Tools
3. Verify temperature sensors are providing valid readings
4. Check humidity sensor (if enabled) is returning valid values
5. Review Home Assistant logs for climate entity errors

### Eco Mode Always Active

1. Check outdoor temperature sensor reading
2. Verify outdoor_temp_threshold setting isn't too low
3. Ensure outdoor sensor is measuring actual outdoor temperature
4. Test by temporarily increasing outdoor threshold
5. Check if sensor is reporting correct units (°C)

## 📝 Version History

### Version 1.3.1
- 🔧 Improved override handling and startup logic
- ✨ Automatic temperature restoration when override expires
- ✨ Manual override cancellation handling
- 🔧 Better startup logic for expired overrides

### Version 1.3.0
- 🛠️ Manual override feature with configurable timeout
- ✨ Temporary manual temperature control

### Version 1.2.4
- 🗑️ Removed notification settings (simplified configuration)

### Version 1.2.3
- 🔥 Comprehensive intelligent heating control
- 🏠 Presence-based temperature management
- 🌡️ Outdoor temperature eco mode
- 🚪 Door/window protection with delays
- 🌙 Night mode with scheduled reduction
- ⏰ Pre-heating before wake-up
- 💧 Humidity compensation support
- 🔄 15-minute periodic synchronization

## ❓ FAQ

**Q: Can I use this with multiple climate entities?**
A: Create separate automations for each climate entity. Each automation can have different settings optimized for that room.

**Q: What happens if I manually change the temperature?**
A: The automation will override manual changes on the next trigger (arrival home, mode change, or periodic check). To temporarily override, disable the automation.

**Q: Does this work with non-Celsius temperatures?**
A: The blueprint is designed for Celsius. For Fahrenheit, adjust all temperature values accordingly.

**Q: Can I have different temperatures for weekdays vs weekends?**
A: Not directly, but you can create two automations with different schedules and use conditions to enable them based on day of week.

**Q: Why does heating turn off when it's warm outside?**
A: This is the eco mode feature. When outdoor temperature exceeds the threshold (default 18°C), heating is disabled to save energy. Adjust the "Outdoor Temperature Threshold" if needed.

**Q: How does humidity compensation work?**
A: High humidity (>70%) makes it feel warmer, so temperature is reduced by 0.5°C. Low humidity (<30%) makes it feel colder, so temperature is increased by 0.5°C.

**Q: What's the difference between away mode and eco mode?**
A: Away mode activates when nobody is home (sets to away temperature). Eco mode activates when outdoor temperature is high enough (turns heating off completely).

## 🤝 Contributing

Found a bug or have a suggestion? Please [open an issue](https://github.com/r3mcos3/blueprints/issues) on GitHub!

## 📄 License

This blueprint is provided as-is under the MIT License.

## 🙏 Credits

Created by [r3mcos3](https://github.com/r3mcos3)
