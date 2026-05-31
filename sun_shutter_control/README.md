# ☀️ Sun-Aware Shutter Control

[![version](https://img.shields.io/badge/version-1.7.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

Automatic shutter control based on sun position. Closes shutters when the sun shines on the front or back of your house, and opens them again once the sun moves away. Respects manual operation so you always stay in control! 🌞

## ✨ Features

- ☀️ **Automatic closing** - Closes shutters when the sun shines on that facade
- 🔄 **Automatic opening** - Opens shutters once the sun moves to another direction (optional)
- 🖐️ **Manual override** - Detects manual shutter operation and leaves those shutters alone until the sun moves away
- 🌤️ **Cloud detection** - Optional weather integration: open shutters when it's overcast, close again when it clears up
- ⏱️ **Anti-oscillation cooldown** - Minimum wait between moves, prevents rapid up/down on partly cloudy days
- 📍 **Position awareness** - Skips the command if shutters are already at the target position
- 📐 **Configurable sun window** - Set how many degrees of margin the sun may be on a facade
- 🌅 **Minimum sun elevation** - No action during low morning or evening sun
- 🔽 **Flexible positions** - Configure close and open position (e.g. half-close at 50%)
- 🏠 **Front and back separately** - Independent shutter groups per facade side

## 📋 Requirements

Before using this blueprint, you need:

1. **Cover entities** - Shutters or blinds as `cover` domain in Home Assistant
2. **Sun integration** - Built-in HA sun integration (`sun.sun`), available by default
3. **Front facade azimuth** - The compass direction your front facade faces (see tip below)

### Optional

- **Input Boolean helpers** - For manual override detection (one per facade side)

## 🌐 Finding your house azimuth

Go to **[suncalc.org](https://www.suncalc.org/)**, find your house and determine which direction your front door faces:

| Direction | Azimuth |
|-----------|---------|
| North | 0° |
| East | 90° |
| South | 180° |
| West | 270° |

The back of your house is calculated automatically as front + 180°.

## 🚀 Installation

### Automatic Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fsun_shutter_control%2Fsun_shutter_control.yaml)

### Manual Installation

1. In Home Assistant, navigate to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click the **Import Blueprint** button
3. Enter the blueprint URL:
   ```
   https://github.com/r3mcos3/blueprints/blob/main/sun_shutter_control/sun_shutter_control.yaml
   ```
4. Click **Preview** and then **Import**

### Creating override helpers (optional)

For the manual override feature, create a toggle helper per facade side:

1. Go to **Settings** → **Devices & Services** → **Create Helper**
2. Choose **Toggle**
3. Give it a name, e.g. `Shutter front manual`
4. Link the helper to the blueprint under the **Manual Override** section

## ⚙️ Configuration

### Required Settings

| Parameter | Description |
|-----------|-------------|
| 🏠 Front facade direction | Azimuth of the front facade in degrees (0–359°) |
| 🏠 Front shutters | Cover entities on the front of the house |
| 🏡 Back shutters | Cover entities on the back of the house |

### 🌤️ Weather Settings (collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 🌤️ Weather entity | Your weather integration entity (optional) | — |
| ☁️ When to close | Which conditions allow closing: always / sunny+partly cloudy / sunny only | Sunny or partly cloudy |

### ☀️ Sun Settings (collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 📐 Sun window angle | Degrees left/right of the facade that count as "sun on facade" | 90° |
| 🌅 Minimum sun elevation | Minimum sun height above the horizon | 10° |

### ⚙️ Shutter Settings (collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 🔽 Close position | Position when sun is on the facade (0% = fully closed) | 0% |
| 🔼 Automatically open | Open when sun moves away | On |
| 🔼 Open position | Position when automatically opening | 100% |
| ⏱️ Cooldown between moves | Minimum minutes between two movements (0 = disabled) | 20 min |

### 🖐️ Manual Override (collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 🖐️ Override helper front | Input Boolean helper for the front facade | Optional |
| 🖐️ Override helper back | Input Boolean helper for the back facade | Optional |

## 🎯 How It Works

### Sun position calculation

The blueprint uses the **azimuth** of `sun.sun` — the compass direction of the sun (0–360°). Every 5 minutes it calculates whether the sun is on the front or back facade:

```
Angle difference = ((sun azimuth − facade direction + 180) % 360) − 180
Sun on facade    = angle difference < sun window AND elevation > minimum
```

This formula works correctly for all directions, including the wrap-around near North (359° → 1°).

### Decision logic

For each facade side (front/back):

```
If sun on facade AND weather allows AND no manual override
  → Move shutters to close position

If (sun NOT on facade OR cloudy) AND sun above min elevation AND auto-open is on AND no manual override
  → Move shutters to open position
  → Reset manual override

If (sun NOT on facade OR cloudy) AND sun above min elevation AND auto-open is on AND manual override active
  → Do NOT move shutters (respects manual close)
  → Reset manual override (so next day works normally)

If sun below min elevation (evening/night)
  → Do nothing — shutters stay wherever they are
```

### Manual override

HA records **who** initiated every state change. When a user manually operates a shutter (via the app, dashboard or physical switch), the context contains a `user_id`. The blueprint detects this and turns the override helper on.

The override works in **both directions**:
- **Manually opened** while sun is shining → automation won't close them
- **Manually closed** in the evening → automation won't open them again at the next check

The override is **automatically reset** once the sun moves away from that facade (regardless of whether auto-open moves the shutters) — so everything works normally again the next day.

### Trigger moments

| Trigger | When |
|---------|------|
| ☀️ Sun position change | Every time the sun's azimuth updates (event-driven, typically every few minutes while the sun moves) |
| 🏠 HA restart | On Home Assistant startup |
| 🖐️ Cover state change | Immediately on manual shutter operation (override detection only) |

## 💡 Usage Examples

### Example 1: Front door faces East

House with front door facing East (morning sun on the front):

```yaml
automation:
  - alias: "Shutters based on sun position"
    use_blueprint:
      path: r3mcos3/sun_shutter_control
      input:
        front_facing_azimuth: 90
        front_covers:
          - cover.shutter_living_room_front
          - cover.shutter_bedroom_front
        back_covers:
          - cover.shutter_kitchen_back
```

**Expected behavior:**
- Morning (sun in the East): front shutters close
- Afternoon/evening (sun in the West): back shutters close
- Evening: everything opens

### Example 2: Half-close with manual override

Shutters go to 50% when sun shines, with manual override:

```yaml
automation:
  - alias: "Shutters based on sun position"
    use_blueprint:
      path: r3mcos3/sun_shutter_control
      input:
        front_facing_azimuth: 180
        front_covers:
          - cover.shutter_living_room
        back_covers:
          - cover.shutter_bedroom
        close_position: 50
        open_position: 100
        front_override_helper: input_boolean.shutter_front_manual
        back_override_helper: input_boolean.shutter_back_manual
```

**Expected behavior:**
- Sun on facade: shutters move to 50%
- Someone manually opens: override on, automation leaves it alone
- Sun moves away: shutters go to 100% open, override resets

### Example 3: Close only, never auto-open

Only close automatically, open manually:

```yaml
automation:
  - alias: "Shutters close at sun"
    use_blueprint:
      path: r3mcos3/sun_shutter_control
      input:
        front_facing_azimuth: 270
        front_covers:
          - cover.shutter_front
        back_covers:
          - cover.shutter_back
        auto_open: false
        close_position: 0
```

**Expected behavior:**
- Sun on facade: shutters close fully
- Sun moves away: nothing, shutters stay where they are

## 🔧 Troubleshooting

### Shutters not moving

1. Check cover entities exist and respond via **Developer Tools → States**
2. Verify the automation is enabled
3. Check the sun azimuth via `sun.sun` → attribute `azimuth`
4. View traces: **Settings → Automations → [name] → Traces**
5. Verify sun elevation (`elevation`) is above the minimum threshold

### Wrong direction calculated

1. Verify the configured azimuth using [suncalc.org](https://www.suncalc.org/)
2. Increase the sun window (default 90°) if the sun is just outside the margin
3. Check the automation traces to see what values `v_sun_on_front` and `v_sun_on_back` contain

### Manual override not working

1. Verify the input_boolean helper exists and is correctly linked
2. Check in **States** whether the helper toggles on/off after manual operation
3. Make sure the shutters are configured as `cover` entities (not `switch`)
4. Note: Alexa/Google voice actions don't carry a `user_id` and are not seen as manual

### Override not resetting automatically

1. Check that **Automatically open** is enabled in the shutter settings
2. The override only resets when the sun moves AWAY from that facade (not at night or low sun)
3. You can always manually turn off the helper from your HA dashboard

## 📝 Version History

### Version 1.7.0
- ⏱️ Added cooldown between moves to prevent rapid oscillation on partly cloudy days
- 📍 Added position check: skips cover commands when already at the target position

### Version 1.6.0
- 🌙 Auto-open no longer fires when the sun is below the minimum elevation — shutters closed at night stay closed

### Version 1.5.0
- 🌤️ Added optional weather/cloud detection: shutters stay open when overcast

### Version 1.4.0
- ✨ Replaced 5-minute polling trigger with event-driven sun azimuth trigger

### Version 1.3.0
- 🐛 Fixed: manually closing shutters in the evening no longer causes them to be re-opened by the automation

### Version 1.2.0
- 🌐 Translated all descriptions and labels to English

### Version 1.1.0
- 🖐️ Manual override detection via context `user_id`
- 🔄 Automatic override reset when sun moves away
- ✨ Optional input_boolean helpers per facade side

### Version 1.0.1
- 📝 Added [suncalc.org](https://www.suncalc.org/) tip to description

### Version 1.0.0
- 🎉 Initial release
- ☀️ Azimuth-based shutter control
- 📐 Configurable sun window with wrap-around correction
- 🌅 Minimum sun elevation setting
- 🔽 Configurable close and open positions

## 🤝 Contributing

Found a bug or have a suggestion? Please [open an issue](https://github.com/r3mcos3/blueprints/issues) on GitHub!

## 📄 License

This blueprint is provided as-is under the MIT License.

## 🙏 Credits

Created by [r3mcos3](https://github.com/r3mcos3)
