# 🔋 Accu Saver - Battery Health Manager

[![version](https://img.shields.io/badge/version-1.3.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

Smart battery health management for laptop servers! Automatically controls charging via smart plug to maintain optimal battery levels and extend battery lifespan. 🔌⚡

## ✨ Features

- 🔋 **Battery Level Monitoring** - Continuously monitors battery percentage
- ⚡ **Automatic Charge Control** - Smart plug controls charging automatically
- 🎯 **Configurable Thresholds** - Customize upper/lower battery limits
- 🔄 **Immediate Response** - No delays, instant switching
- ⏰ **Periodic Status Checks** - Automatic sync every 5 minutes
- 🛡️ **Battery Protection** - Prevents overcharging and deep discharge
- 🚀 **Startup Sync** - Correct state even after HA restarts

## 📋 Requirements

1. **Battery Sensor** - Entity reporting battery percentage (0-100)
   - Example: `sensor.laptop_battery_level`
   - Any `sensor` that reports a number between 0 and 100
2. **Smart Plug/Switch** - Controls charger power
   - Example: `switch.laptop_charger_plug`
   - Must be switch domain

## 🚀 Installation

### Automatic Installation

[![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Faccu_saver%2Faccu_saver.yaml)

### Manual Installation

1. In Home Assistant: **Settings** → **Automations & Scenes** → **Blueprints**
2. Click **Import Blueprint**
3. Enter URL: `https://github.com/r3mcos3/blueprints/blob/main/accu_saver/accu_saver.yaml`

## ⚙️ Configuration

| Parameter | Description | Default |
|-----------|-------------|---------|
| 🔋 Battery Sensor | Battery percentage sensor | Required |
| 🔌 Smart Plug | Switch controlling charger | Required |
| ⬆️ Upper Threshold | Stop charging at this % | 80% |
| ⬇️ Lower Threshold | Start charging at this % | 20% |

## 🎯 How It Works

1. **Battery Reaches 80%** → Plug turns OFF (stops charging)
2. **Battery Drops to 20%** → Plug turns ON (resumes charging)
3. **Battery in Range 20-80%** → No action (maintains current state)

This creates a healthy charge cycle that significantly extends battery lifespan!

### Why These Thresholds?

- **80% Maximum**: Charging to 100% stresses lithium batteries, reducing lifespan. Studies show 80% max charge can double battery cycle life.
- **20% Minimum**: Deep discharge below 20% damages lithium batteries. Provides safety margin above critical 10% level.
- **Result**: Optimal balance between usable capacity and battery longevity!

## 💡 Usage Example

```yaml
automation:
  - alias: "Battery Saver - Laptop Server"
    use_blueprint:
      path: r3mcos3/accu_saver
      input:
        battery_sensor: sensor.laptop_battery_level
        smart_plug: switch.laptop_charger_plug
        upper_threshold: 80
        lower_threshold: 20
```

## 🔧 Troubleshooting

**Q: Plug not switching at threshold?**
- Verify battery sensor reports 0-100 values
- Check automation is enabled
- Review automation traces in HA

**Q: Can I use different thresholds?**
- Yes! Adjust in blueprint settings
- Upper threshold: 50-100% (step 5%)
- Lower threshold: 5-50% (step 5%)
- Keep 20-30% gap between thresholds for best results
- The upper threshold must be higher than the lower threshold: otherwise the automation does nothing (safety guard against constant switching)

**Q: Works with any battery sensor?**
- Yes, as long as it reports a percentage (0-100) as a number

**Q: What happens during Home Assistant restart?**
- Blueprint includes startup sync: it waits 10s and only then reads the battery level
- Automatically corrects plug state based on current battery level
- Battery at 85%? Plug turns OFF
- Battery at 15%? Plug turns ON
- Battery at 50%? No change (maintains current state)

**Q: Can I manually override the plug?**
- Yes! You can manually turn the plug on/off anytime
- Blueprint will correct the state at next trigger or restart
- Not aggressive - allows temporary manual control

**Q: What if battery sensor becomes unavailable?**
- Blueprint detects sensor states that are not a number (`unavailable`, `unknown`, ...)
- No actions taken on invalid data
- When sensor recovers, state syncs automatically

**Q: How does the periodic check work?**
- Checks and syncs battery/plug state every 5 minutes
- Ensures correct state even after manual overrides
- Useful for maintaining consistent state without waiting for threshold triggers
- Runs automatically in the background

## 🔄 Advanced Scenarios

### Scenario: Battery in Middle Range (50%)
- Plug state remains unchanged
- Prevents oscillation and unnecessary switching
- This is hysteresis behavior - intentional and optimal!

### Scenario: Sensor Temporarily Offline
- No plug changes during sensor outage
- State syncs when sensor comes back online
- Ensures battery protection even with sensor issues

### Scenario: Rapid Threshold Crossing
- Single mode prevents overlapping executions
- State checks prevent redundant ON/OFF commands
- Smooth operation even with sensor fluctuations

## 📊 Battery Health Tips

For optimal battery lifespan with this blueprint:
- **Conservative**: Use 30-70% thresholds (very gentle on battery)
- **Balanced**: Use 20-80% thresholds (recommended, default)
- **Extended**: Use 15-85% thresholds (more capacity, still healthy)

## 📝 Version History

### Version 1.3.0
- 🐛 Fixed: startup sync read the battery level *before* its 10 s delay, so it could act on stale values
- 🐛 Fixed: startup sync was skipped when the sensor was unavailable at the moment of boot, even if it became available during the delay
- 🛡️ Added: guard that does nothing when the upper threshold is not higher than the lower threshold
- 🔧 Sensor check now uses `is_number` instead of only excluding `unavailable`/`unknown`
- 🧹 Merged three duplicated sync blocks into one (same behaviour, ~80 lines shorter)
- 📝 README no longer claims `device_class: battery` is required (it was never enforced)

## 📄 License

MIT License

---

Made with ❤️ by r3mcos3
