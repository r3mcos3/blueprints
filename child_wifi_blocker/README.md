# 📵 Child WiFi Blocker

[![version](https://img.shields.io/badge/version-1.3.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2024.6.0%2B-blue.svg)](https://www.home-assistant.io/)

Automatically block your child's WiFi at bedtime and unblock it in the morning — via the UniFi Network integration. Create one automation per child. Each child can have multiple devices (phone, tablet, laptop) that are all blocked and unblocked at the same time. 🔒

## ✨ Features

- 📵 **Automatic blocking** — Blocks all configured devices at the set bedtime
- ✅ **Automatic unblocking** — Unblocks devices again in the morning
- 📅 **Day schedule** — Choose which days the schedule is active (weekdays, weekend, or any combination)
- 🔁 **Self-correcting** — On HA startup and automation reload, immediately enforces the correct state without needing a manual trigger
- 🏠 **Away blocking** — Optionally block devices immediately when nobody is home, and unblock again when someone returns (only during the allowed time window)
- ⏸️ **Quick toggle** — Enable/disable the schedule without removing the automation

## 📋 Requirements

Before using this blueprint, you need:

1. **UniFi Network integration** — Installed and configured in Home Assistant
2. **UniFi client block switches** — The integration creates a `switch` entity per tracked client device. When the switch is ON, the device is blocked from the network.

### Optional

- **Person / device_tracker / group entity** — For the "block when nobody is home" feature

## ⚙️ Setup

### Finding the UniFi block switches

1. Go to **Settings** → **Devices & Services** → **UniFi Network**
2. Open the integration and browse the entities
3. Look for `switch` entities named after your child's devices
4. Switch ON = device blocked, Switch OFF = device allowed

## 🚀 Installation

### Automatic Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fchild_wifi_blocker%2Fchild_wifi_blocker.yaml)

### Manual Installation

1. In Home Assistant, navigate to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click the **Import Blueprint** button
3. Enter the blueprint URL:
   ```
   https://github.com/r3mcos3/blueprints/blob/main/child_wifi_blocker/child_wifi_blocker.yaml
   ```
4. Click **Preview** and then **Import**

## ⚙️ Configuration

### 👶 Child

| Parameter | Description | Default |
|-----------|-------------|---------|
| 👤 Child's name | Label only — does not affect automation logic | `Child` |
| 📱 Devices to block | UniFi switch entities for this child's devices (multi-select) | — |

### 📅 Schedule

| Parameter | Description | Default |
|-----------|-------------|---------|
| 🌙 Block time | Time at which WiFi is blocked | `21:00:00` |
| ☀️ Unblock time | Time at which WiFi is unblocked | `07:00:00` |
| 📆 Active days | Days on which the schedule applies | All days |

### ⚙️ Options (collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 🏠 Also block when nobody is home | Block immediately when presence goes to `not_home` | Off |
| 👥 Presence entity | Person, device_tracker, group or binary_sensor for away detection | Optional |
| ✅ Enable this automation | Quick on/off without removing the automation | On |

## 🎯 How It Works

### Trigger moments

| Trigger | Action |
|---------|--------|
| 🌙 Block time reached | Turn ON all device switches (block) — only on active days |
| ☀️ Unblock time reached | Turn OFF all device switches (allow) — only on active days |
| 🏠 Presence → `not_home` | Block immediately (if away-blocking is enabled) |
| 🏠 Presence → `home` | Unblock (if away-blocking is enabled and within allowed time window) |
| 🔁 HA startup | Evaluate current time and set correct block/unblock state |
| 🔁 Automation reloaded | Evaluate current time and set correct block/unblock state |

### Time window logic

The blueprint correctly handles schedules that cross midnight (e.g. block at 22:00, unblock at 07:00):

```
If block_time > unblock_time  →  blocked when: now ≥ block_time  OR  now < unblock_time
If block_time < unblock_time  →  blocked when: now ≥ block_time AND now < unblock_time
```

### Away blocking

When the presence entity goes to `not_home`, all devices are blocked immediately regardless of the time schedule.

When someone returns home (`home`), the devices are unblocked — **but only if the current time is within the allowed window** (between unblock time and block time). Outside that window the time schedule takes precedence and the devices stay blocked.

## 💡 Usage Tips

- **Name each automation after the child** — e.g. `📵 WiFi — Emma` and `📵 WiFi — Liam` so they are easy to tell apart in the automations list
- **Multiple devices per child** — Select all of a child's devices (phone, tablet, laptop) in one automation; they all block and unblock together
- **Different schedules per day** — Create two automations per child with different times, each with a different set of active days (e.g. weekdays vs weekend)

## 🔧 Troubleshooting

### The devices are not blocked at the scheduled time

1. Check that the automation is enabled
2. Verify the correct UniFi switch entities are selected
3. Check the automation traces: **Settings → Automations → [name] → Traces**
4. Make sure the day is listed under **Active days**

### The switch state is wrong after a HA restart

The blueprint includes a startup trigger that re-evaluates and corrects the state automatically. If it did not fire, check the automation traces for the `evaluate` trigger.

### The blueprint shows "malformed" on the presence entity

Leave the presence entity field empty if you do not use the away-blocking feature. It is optional and defaults to empty.

### The away feature unblocks at the wrong time

The unblock-on-home trigger only fires when the current time is within the allowed window (between unblock time and block time). Outside that window, the schedule takes precedence.

## 📝 Version History

### Version 1.3.0
- 🔁 Added **self-correcting** behaviour: two new triggers (`homeassistant: start` and `automation_reloaded`) evaluate the correct block/unblock state immediately without needing a manual trigger or HA restart
- 🕛 Fixed time window logic to correctly handle midnight-crossing schedules (e.g. block at 22:00, unblock at 07:00)

### Version 1.2.0
- 🐛 Fixed "malformed" error on presence entity — added `default: {}` to make the field truly optional

### Version 1.1.0
- 🔍 Device selector now filtered to UniFi switches only — no more unrelated switches in the list

### Version 1.0.0
- 🎉 Initial release
- 📵 Time-based WiFi blocking via UniFi switch entities
- 📅 Configurable day schedule
- 🏠 Optional away-blocking with presence entity
- ⏸️ Quick enable/disable toggle

## 🤝 Contributing

Found a bug or have a suggestion? Please [open an issue](https://github.com/r3mcos3/blueprints/issues) on GitHub!

## 📄 License

This blueprint is provided as-is under the MIT License.

## 🙏 Credits

Created by [r3mcos3](https://github.com/r3mcos3)
