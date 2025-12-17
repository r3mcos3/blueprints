# 🚗 AI Parking Spot Counter

[![version](https://img.shields.io/badge/version-2.0.0-blue.svg)](https://github.com/r3mco/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

This blueprint automatically uses AI to analyze camera feeds and count free and occupied parking spaces when you arrive home. Perfect for keeping track of available parking spots in front of your house! 🅿️

## ✨ Features

- 🤖 **AI-Powered Analysis** - Uses your AI integration to intelligently count parking spaces
- 📷 **Camera Integration** - Works with any Home Assistant camera that supports snapshots
- 🏘️ **Multiple Zones** - 1 required + 4 optional zone detection points
- 🧭 **Optional Proximity Check** - Only trigger when approaching home (configurable)
- 💾 **Automatic Updates** - Updates sensor entities with free and occupied counts
- 📱 **Telegram Notifications** - Optional notifications with customizable messages
- 📸 **Snapshot Storage** - Optionally save camera snapshots for review
- 🎯 **Flexible Configuration** - Customize AI instructions and parking space count
- 📦 **Collapsed Sections** - Clean UI with organized, collapsible input sections

## 📋 Requirements

Before using this blueprint, you need:

1. **AI Task Integration** - The AI Task integration configured with a provider (e.g., Google Generative AI, Anthropic)
2. **Camera Entity** - A camera that supports snapshots and has a clear view of parking spaces
3. **Person Entity** - A person entity to track for arrivals
4. **Zone Entities** - At least one zone entity to monitor for arrivals
5. **Input Number Helpers** - Two helpers to store free and occupied counts
6. **Proximity Sensor** (Optional) - A proximity sensor that indicates direction of travel

### Setting Up Input Number Helpers

1. Go to **Settings** → **Devices & Services** → **Helpers**
2. Click **+ CREATE HELPER** → **Number**
3. Create two helpers:
   - **Free Parking Spots**
     - Min: 0
     - Max: (your total parking spaces)
   - **Occupied Parking Spots**
     - Min: 0
     - Max: (your total parking spaces)

### Setting Up Proximity Sensor (Optional)

Create a proximity sensor to track direction of travel. See [Home Assistant Proximity documentation](https://www.home-assistant.io/integrations/proximity/).

## 🚀 Installation

### Automatic Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fai_parking_counter%2Fai_parking_counter.yaml)

### Manual Installation

1. In Home Assistant, navigate to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click the **Import Blueprint** button
3. Enter the blueprint URL:
   ```
   https://github.com/r3mcos3/blueprints/blob/main/ai_parking_counter/ai_parking_counter.yaml
   ```
4. Click **Preview** and then **Import**

## ⚙️ Configuration

When creating an automation from this blueprint, you'll configure:

### Main Settings (Always Visible)

| Parameter | Description | Required |
|-----------|-------------|----------|
| 👤 Person | Person entity to track for zone arrivals | Yes |
| 🏘️ Zone 1 | Primary zone to monitor for arrival | Yes |

### 🧭 Proximity Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| Enable Proximity Sensor | Enable/disable proximity direction check | false |
| Proximity Direction Sensor | Proximity sensor (should be "towards" when approaching) | - |

### 🏘️ Optional Zones 2-5 (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| Enable Zone 2-5 | Enable/disable each additional zone | false |
| Zone 2-5 | Additional zones to monitor for arrival | zone.home |

### 🤖 AI & Camera Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 📷 Camera | Camera to analyze for parking spots | camera.front_door |
| 🤖 AI Task Entity | AI entity for image analysis | ai_task.google_ai_task |
| 📝 AI Instructions | Custom AI instructions (use {total_spaces} placeholder) | "" |

### 🅿️ Parking Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 🅿️ Total Parking Spaces | Total number of parking spaces (1-20) | 3 |
| 🟢 Free Spots Sensor | Input number entity for free spots count | - |
| 🔴 Occupied Spots Sensor | Input number entity for occupied spots count | - |

### 📱 Notification Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 📱 Telegram Bot | Optional Telegram bot for notifications | None |
| 💬 Telegram Message | Message to send (use {free_spots} placeholder) | "There are {free_spots} free parking spots 🚗 available! 🚪" |
| 🏷️ Telegram Title | Optional title for notifications | "" |

### 📸 Snapshot Settings (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 📸 Save Snapshot | Whether to save camera snapshot | true |
| 🗂️ Snapshot Path | File path to save snapshot | /config/www/parking_spot.jpg |

## 💡 Usage Examples

### Example 1: Dashboard Display

Display parking availability on your dashboard:

```yaml
type: entities
entities:
  - entity: input_number.free_parking_spots
    name: Free Spots 🟢
  - entity: input_number.occupied_parking_spots
    name: Occupied Spots 🔴
```

### Example 2: View Saved Snapshot

Display the saved snapshot on your dashboard:

```yaml
type: picture
image: /local/parking_spot.jpg
```

### Example 3: Custom AI Instructions

For more accurate counting, customize the AI instructions:

```
Analyze this image of my driveway. There are {total_spaces} parking spots visible directly in front of the house entrance. Count how many spots are FREE (completely empty with no vehicle) and how many are OCCUPIED (has any vehicle parked). Ignore motorcycles and bicycles.
```

## 🔧 Troubleshooting

### AI Not Analyzing Correctly

1. Check if your AI Task integration is properly configured
2. Verify the camera has a clear view of all parking spaces
3. Improve lighting conditions if analyzing at night
4. Try customizing the AI instructions to be more specific
5. Note: OpenAI may have issues with camera attachments - Google AI is recommended

### Notification Not Sending

1. Verify your Telegram bot is configured correctly in Home Assistant
2. Select the correct Telegram bot from the dropdown
3. Check Home Assistant logs for any errors

### Snapshot Not Saving

1. Ensure the `/config/www/` directory exists and is writable
2. Check that your camera supports the `camera.snapshot` service
3. Verify the snapshot path is correct

### Wrong Parking Count

1. Ensure good lighting and camera angle
2. Customize AI instructions to be more specific about what to count
3. Adjust total parking spaces setting
4. Test during different times of day for consistency

### Trigger Not Working

1. Verify your zone is correctly configured
2. Check if the person entity is tracking correctly
3. If using proximity sensor, ensure it's enabled and showing "towards" when approaching
4. For testing, disable the proximity sensor check

## 📝 Version History

### Version 2.0.0 (2025-12-17)
- 🏘️ Support for 1 required + 4 optional zone detection points
- 🧭 Proximity sensor now optional (with enable toggle)
- 📦 Organized UI with collapsed input sections
- 🎯 Increased max parking spaces from 10 to 20
- 📌 Requires Home Assistant 2025.12.0+

### Version 1.0.5 (2025-12-15)
- 🌐 Translate default Telegram message to English

### Version 1.0.4 (2025-12-15)
- 🐛 Fix decimal formatting in Telegram message

### Version 1.0.3 (2025-12-15)
- ✨ Add Telegram bot config_entry selector

### Version 1.0.2 (2025-12-15)
- ✨ Add customizable Telegram message and optional title

### Version 1.0.1 (2025-12-15)
- 🐛 Fix camera media_content_id to include full entity_id

### Version 1.0.0 (2025-12-15)
- 🎉 Initial release
- 🤖 AI-powered parking spot counting
- 📱 Optional Telegram notifications
- 📸 Camera snapshot support
- 🎯 Customizable AI instructions

## 🤝 Contributing

Found a bug or have a suggestion? Please [open an issue](https://github.com/r3mcos3/blueprints/issues) on GitHub!

## 📄 License

This blueprint is provided as-is under the MIT License.

## 🙏 Credits

Created by [r3mcos3](https://github.com/r3mcos3)
