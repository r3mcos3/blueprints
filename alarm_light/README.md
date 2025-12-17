# ⏰ Alarm Light

[![version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

Wake up gently with lights that turn on before your alarm! This blueprint uses your phone's next alarm sensor to automatically illuminate your room, making mornings easier. 🌅

## ✨ Features

- ⏰ **Alarm Integration** - Syncs with your phone's next alarm sensor
- 💡 **Gradual Wake-up** - Lights turn on before your alarm rings
- 🏠 **Presence Aware** - Only triggers when you're home
- 🌙 **Darkness Check** - Only activates when it's dark outside
- 📅 **Day Selection** - Choose all days, weekdays only, or weekends only
- ⏱️ **Flexible Offset** - Set lights to turn on 5-60 minutes before alarm
- ✨ **Adjustable Brightness** - Configure the perfect wake-up brightness

## 📋 Requirements

Before using this blueprint, you need:

1. **Next Alarm Sensor** - A sensor with device class `timestamp` containing your next alarm time
   - For Android: Use the Home Assistant Companion app (sensor.phone_name_next_alarm)
   - For iPhone: Requires additional setup (iOS doesn't natively expose alarm data)
2. **Person Entity** - A person entity to check if you're home
3. **Light Entity** - One or more lights to turn on

### Setting Up Next Alarm Sensor (Android)

1. Install the **Home Assistant Companion App** on your Android phone
2. Go to **Settings** → **Companion App** → **Manage Sensors**
3. Enable **Next Alarm** sensor
4. The sensor will appear as `sensor.your_phone_name_next_alarm`

### Setting Up Next Alarm Sensor (iOS / iPhone)

iOS doesn't natively expose alarm data like Android does. However, there are community workarounds using **iOS Shortcuts**:

#### Option 1: iOS Shortcuts + Input Datetime Helper (Recommended)

1. **Create a helper in Home Assistant:**
   - Go to **Settings** → **Devices & Services** → **Helpers**
   - Create an **Input Datetime** helper (e.g., `input_datetime.iphone_next_alarm`)
   - Enable both Date and Time

2. **Create an iOS Shortcut:**
   - Open the **Shortcuts** app on your iPhone
   - Create a new shortcut that sends your alarm time to Home Assistant
   - Use the "Get Upcoming Alarms" action (iOS 17+)
   - Send the result to your HA helper via the Companion App or REST API

3. **Automate the shortcut:**
   - Set the shortcut to run when you set an alarm
   - Or use a Sleep Schedule trigger to sync automatically

#### Option 2: Use iOS Sleep Schedule

If you use the **Sleep Schedule** feature in the iOS Health app:

1. Set up your sleep schedule with a wake-up alarm
2. Create an iOS Shortcut triggered by "Wake Up" event
3. Have the shortcut call a Home Assistant webhook or update a helper

#### Helpful Resources

- [Sync iOS 17 Sleep alarm to HA](https://community.home-assistant.io/t/sync-ios-17-sleep-alarm-to-ha-take-2/715690)
- [iOS 18 Shortcuts Guide](https://community.home-assistant.io/t/sync-home-assistant-alarm-clock-to-iphone-alarms-using-shortcuts-ios-18/805595)
- [iOS 17.1 Push Alarm to HA](https://community.home-assistant.io/t/ios-17-1-push-iphone-alarm-clock-to-ha/623821)

> **Note:** iOS workarounds require more setup than Android. The reliability depends on iOS Shortcuts execution and may not capture all alarm changes immediately.

## 🚀 Installation

### Automatic Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Falarm_light%2Falarm_light.yaml)

### Manual Installation

1. In Home Assistant, navigate to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click the **Import Blueprint** button
3. Enter the blueprint URL:
   ```
   https://github.com/r3mcos3/blueprints/blob/main/alarm_light/alarm_light.yaml
   ```
4. Click **Preview** and then **Import**

## ⚙️ Configuration

| Parameter | Description | Default |
|-----------|-------------|---------|
| ⏰ Next Alarm Sensor | Sensor with your next alarm time (device class: timestamp) | - |
| 👤 Person | Person entity to check if home | - |
| 💡 Target Lights | Lights to turn on | - |
| ⏱️ Offset Before Alarm | Minutes before alarm to turn on lights | 10 min |
| ✨ Brightness | Brightness percentage (0-100%) | 33% |
| 📅 Active Days | All days, weekdays only, or weekends only | All Days |

### Offset Options

- 5 minutes before
- 10 minutes before (default)
- 15 minutes before
- 20 minutes before
- 30 minutes before
- 45 minutes before
- 60 minutes before

## 💡 Usage Examples

### Example 1: Bedroom Wake-up Light

```yaml
automation:
  - alias: "Bedroom Wake-up Light"
    use_blueprint:
      path: r3mcos3/alarm_light
      input:
        alarm_sensor: sensor.pixel_8_next_alarm
        person_entity: person.john
        lights_target:
          entity_id: light.bedroom_ceiling
        offset_before_alarm: "-00:15:00"
        brightness_pct: 50
        weekday_selection: weekdays
```

### Example 2: Multiple Lights Sunrise Simulation

Turn on multiple lights at different times for a gradual sunrise effect by creating multiple automations:

1. **First automation** - Dim light 30 min before at 10%
2. **Second automation** - Brighter light 15 min before at 30%
3. **Third automation** - Full brightness 5 min before at 70%

## 🔧 Troubleshooting

### Lights Not Turning On

1. **Check alarm sensor** - Verify the sensor has a valid timestamp in Developer Tools → States
2. **Check presence** - Ensure your person entity shows "home"
3. **Check darkness** - The automation only runs when `sun.sun` is `below_horizon`
4. **Check day selection** - Make sure today matches your active days setting

### Alarm Sensor Not Updating

1. Ensure the Home Assistant Companion app has the sensor enabled
2. Check battery optimization settings aren't blocking the app
3. Verify the phone has an alarm set

### Wrong Timezone

If lights turn on at the wrong time, check your Home Assistant timezone configuration in **Settings** → **System** → **General**.

## 📝 Version History

### Version 1.0.0 (2025-12-17)
- 🎉 Initial release
- ⏰ Phone alarm integration
- 💡 Configurable brightness and offset
- 📅 Day selection (all/weekdays/weekends)
- 🏠 Presence and darkness conditions

## 🤝 Contributing

Found a bug or have a suggestion? Please [open an issue](https://github.com/r3mcos3/blueprints/issues) on GitHub!

## 📄 License

This blueprint is provided as-is under the MIT License.

## 🙏 Credits

Created by [r3mcos3](https://github.com/r3mcos3)
