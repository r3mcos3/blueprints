# 🚗 AI - Parking Spot Counter

**Version:** 1.0.0

This Home Assistant blueprint uses AI to analyze a camera feed and count free and occupied parking spaces when you arrive home. Perfect for keeping track of available parking spots in front of your house!

## 📋 Description

When you enter one of the configured zones while traveling towards home, this automation:
1. 📷 Captures the current camera feed
2. 🤖 Sends it to an AI task entity for analysis
3. 🔢 Counts free and occupied parking spaces
4. 💾 Updates sensor entities with the counts
5. 📱 Sends a Telegram notification (optional)
6. 📸 Saves a snapshot (optional)

## ✅ Requirements

Before using this blueprint, you need to set up the following:

### 1. 🤖 AI Task Entity
- You need an AI task entity configured in Home Assistant (e.g., `ai_task.google_ai_task`)
- This requires the AI Task integration (available in newer versions of Home Assistant)
- The AI should be capable of analyzing images

### 2. 📊 Input Number Helpers
Create two input number helpers to store the parking spot counts:

1. Navigate to **Settings** → **Devices & Services** → **Helpers**
2. Click **"+ CREATE HELPER"** → **Number**
3. Create two helpers:
   - **Free Parking Spots** (e.g., `input_number.vrije_parkeerplekken`)
     - Min: 0
     - Max: (your total parking spaces)
   - **Occupied Parking Spots** (e.g., `input_number.bezette_parkeerplekken`)
     - Min: 0
     - Max: (your total parking spaces)

### 3. 🧭 Proximity Sensor
- A proximity sensor that tracks your direction of travel
- Should have a state of "towards" when approaching home
- See [Home Assistant Proximity documentation](https://www.home-assistant.io/integrations/proximity/)

### 4. 📷 Camera Entity
- A camera entity that supports both streaming and snapshots
- The camera should have a clear view of the parking spaces

### 5. 📱 Telegram Bot (Optional)
- If you want notifications, configure the Telegram integration
- You'll need the config entry ID (found in Developer Tools → Services → telegram_bot.send_message)

## 🚀 Installation

1. Navigate to **Settings** → **Automations & Scenes** → **Blueprints** in Home Assistant
2. Click **"Import Blueprint"**
3. Enter the URL:
   ```
   https://raw.githubusercontent.com/r3mcos3/blueprints/main/ai_parking_counter/ai_parking_counter.yaml
   ```
4. Click **"Preview"** and then **"Import Blueprint"**

## ⚙️ Configuration

### Required Settings

| Setting | Description | Example |
|---------|-------------|---------|
| 👤 Person | The person entity to track | `person.remco` |
| 🏘️ Zone 1 | First zone to monitor | `zone.huibevendreef` |
| 🏘️ Zone 2 | Second zone to monitor | `zone.moerse_dreef` |
| 🧭 Proximity Direction Sensor | Sensor showing direction of travel | `sensor.proximity_remco_remco_direction_of_travel` |
| 📷 Camera | Camera to analyze | `camera.doorbell_camera_generic` |
| 🤖 AI Task Entity | AI entity for image analysis | `ai_task.google_ai_task` |
| 🟢 Free Spots Sensor | Input number for free spots | `input_number.vrije_parkeerplekken` |
| 🔴 Occupied Spots Sensor | Input number for occupied spots | `input_number.bezette_parkeerplekken` |

### Optional Settings

| Setting | Description | Default |
|---------|-------------|---------|
| 🅿️ Total Parking Spaces | Number of parking spaces to count | 3 |
| 📱 Telegram Config Entry | Telegram bot config ID for notifications | "" (disabled) |
| 📸 Save Snapshot | Save a camera snapshot | true |
| 🗂️ Snapshot Path | Path to save the snapshot | `/config/www/parking_spot.jpg` |
| 📝 AI Instructions | Custom instructions for the AI | "" (use default) |

## 🎯 Custom AI Instructions

If you want to customize the AI analysis, you can provide your own instructions. Use `{total_spaces}` as a placeholder for the total number of parking spaces.

**Example:**
```
Analyze this image of my driveway. There are {total_spaces} parking spots visible.
Count how many spots are FREE (empty) and how many are OCCUPIED (vehicle present).
Ignore motorcycles and bicycles, only count cars.
```

## 📱 Example Notification

When triggered, you'll receive a Telegram message like:
```
Er zijn 2 parkeerplaatsen 🚗 vrij voor de deur! 🚪
```

## 💡 Tips

- **Lighting Conditions**: Make sure your camera has good visibility of the parking spaces, especially at night
- **AI Accuracy**: Test the AI analysis a few times to ensure it correctly counts your parking spaces
- **Multiple Zones**: Use two different zones to catch arrivals from different directions
- **Snapshot Storage**: The snapshot can be viewed later at `http://your-ha-url:8123/local/parking_spot.jpg` (if using default path)

## 🔧 Troubleshooting

### AI not analyzing correctly
- Check if your AI task entity is properly configured
- Verify the camera has a clear view of all parking spaces
- Try customizing the AI instructions to be more specific

### Notification not sending
- Verify your Telegram bot is configured correctly
- Double-check the config entry ID
- Check Home Assistant logs for any errors

### Snapshot not saving
- Ensure the `/config/www/` directory exists and is writable
- Check that your camera supports the `camera.snapshot` service

## 📝 Version History

- **1.0.0** (2025-12-15): Initial release

## 🤝 Contributing

Found a bug or have a suggestion? Please open an issue on the [GitHub repository](https://github.com/r3mcos3/blueprints).

## 📄 License

This blueprint is licensed under the MIT License.
