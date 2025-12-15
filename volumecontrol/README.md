# 🔈 Volume Control 3.0

**Version:** 2.0

This Home Assistant blueprint automates volume control for your media players based on a schedule. Perfect for automatically adjusting speaker volume during different times of the day (e.g., quiet hours at night, louder during the day).

## 📋 Description

When your schedule changes state, this automation:
1. 🗓️ Monitors your configured schedule entity
2. 🔊 Increases volume when schedule turns ON
3. 🔉 Decreases volume when schedule turns OFF
4. 🎬 Optionally executes custom actions

## ✅ Requirements

Before using this blueprint, you need:

### 1. 📻 Media Player Entities
- One or more media player entities (speakers, receivers, etc.)
- These must support the `media_player.volume_set` service

### 2. 🗓️ Schedule Helper
- A schedule helper entity to control timing
- This determines when volume should be high or low

**How to create a Schedule Helper:**
1. Go to **Settings** → **Devices & Services** → **Helpers**
2. Click **"+ CREATE HELPER"** → **Schedule**
3. Name it (e.g., "Quiet Hours")
4. Configure your time periods (when schedule is ON, volume will be high)

📚 [More info about Schedules](https://www.home-assistant.io/integrations/schedule/)

## 🚀 Installation

1. Navigate to **Settings** → **Automations & Scenes** → **Blueprints** in Home Assistant
2. Click **"Import Blueprint"**
3. Enter the URL:
   ```
   https://raw.githubusercontent.com/r3mcos3/blueprints/main/volumecontrol/volume_control3.yaml
   ```
4. Click **"Preview"** and then **"Import Blueprint"**

## ⚙️ Configuration

### Required Settings

| Setting | Description | Example |
|---------|-------------|---------|
| 📻 Media Players | Speakers or media players to control | `media_player.living_room_speaker` |
| 🗓️ Scheduler | Schedule entity that triggers volume changes | `schedule.quiet_hours` |

### Optional Settings

| Setting | Description | Default |
|---------|-------------|---------|
| 🔊 Volume Up Level | Volume level when schedule turns ON | 0.6 (60%) |
| 🔉 Volume Down Level | Volume level when schedule turns OFF | 0.2 (20%) |
| 🎬 Custom Action | Additional action to execute on schedule change | None |

## 🎯 How It Works

### Schedule Turns ON
- **Trigger:** Configured schedule changes to "on"
- **Action:** Set media player volume to "Volume Up Level"
- **Example:** At 8:00 AM, volume increases to 60%

### Schedule Turns OFF
- **Trigger:** Configured schedule changes to "off"
- **Action:** Set media player volume to "Volume Down Level"
- **Example:** At 10:00 PM, volume decreases to 20%

### Custom Actions (Optional)
- Executed whenever the schedule changes state (ON or OFF)
- Can be used for additional automations like notifications, scenes, etc.

## 💡 Tips

- **Volume Levels:** Use 0.1-1.0 range (0.1 = 10%, 1.0 = 100%)
- **Quiet Hours:** Create a schedule for nighttime to automatically lower volume
- **Multiple Speakers:** Select multiple media players to control them all simultaneously
- **Custom Actions:** Use this to trigger scenes, send notifications, or adjust other settings

## 📖 Examples

### Example 1: Nighttime Quiet Hours
- **Schedule:** "Quiet Hours" (ON from 10:00 PM to 8:00 AM)
- **Media Players:** All speakers in the house
- **Volume Up:** 0.6 (60%) - During the day
- **Volume Down:** 0.2 (20%) - During quiet hours

Result: At 10 PM, all speakers lower to 20%. At 8 AM, they increase to 60%.

### Example 2: Weekend Party Mode
- **Schedule:** "Weekend Daytime" (ON Sat-Sun 12:00 PM to 6:00 PM)
- **Media Players:** Living room and kitchen speakers
- **Volume Up:** 0.8 (80%) - Party time!
- **Volume Down:** 0.4 (40%) - Normal listening

Result: Weekend afternoons automatically boost volume for entertaining.

### Example 3: Work Focus Hours
- **Schedule:** "Focus Time" (ON weekdays 9:00 AM to 5:00 PM)
- **Media Players:** Office speaker
- **Volume Up:** 0.3 (30%) - Quiet background music
- **Volume Down:** 0.6 (60%) - Louder when not working

Result: During work hours, office speaker stays quiet for concentration.

### Example 4: With Custom Action
- **Schedule:** "Morning Routine" (ON at 7:00 AM)
- **Volume Up:** 0.5
- **Custom Action:** Turn on morning scene + send notification

Result: At 7 AM, speakers increase volume AND your morning scene activates.

## 🔧 Troubleshooting

### Volume doesn't change
- Verify your media player supports `media_player.volume_set` service
- Check that the schedule entity is working correctly
- Test manually changing the schedule to see if it triggers

### Schedule not triggering
- Ensure your schedule helper is properly configured
- Check the schedule has active time periods defined
- Look at Home Assistant logs for any errors

### Wrong volume level
- Volume uses 0.0-1.0 scale (not 0-100)
- 0.5 = 50%, 0.8 = 80%, etc.
- Verify your volume_up and volume_down settings

## 🎬 Custom Actions Examples

### Send Notification When Volume Changes
```yaml
service: notify.mobile_app
data:
  message: "Volume adjusted for {{ trigger.to_state.state }} period"
```

### Activate Scene When Schedule Starts
```yaml
service: scene.turn_on
target:
  entity_id: scene.evening_mode
```

### Adjust Multiple Devices
```yaml
service: light.turn_on
target:
  entity_id: light.living_room
data:
  brightness_pct: 50
```

## 📝 Version History

- **2.0** (Current): Latest version with custom action support
- Earlier versions: Basic volume control functionality

## 🤝 Contributing

Found a bug or have a suggestion? Please open an issue on the [GitHub repository](https://github.com/r3mcos3/blueprints).

## 📄 License

This blueprint is licensed under the MIT License.
