# 🔥 Simple Heating

[![version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

The no-nonsense heater controller: **two temperatures** (Home and Away), switched by **who is home** and **when you sleep**. No outdoor temperature, windows or humidity – just robust logic. 🌡️

Looking for more features (outdoor temperature, door/window pause, pre-heating, ...)? See [Smart Heating](../smart_heating/).

## ✨ Features

- 🏠 **Two modes** - Home (default 20°C) and Away (default 15°C), both adjustable
- 👥 **Presence** - 2 required persons + 2 optional persons. Anyone home = Home, nobody home = Away
- ✋ **Manual changes are respected** - Turn the heater up or down yourself and it stays that way
- 🌙 **Sleep = Away temperature** - Fixed bedtime / wake-up times, or an optional sleep switch
- ☀️ **Morning = Home** - Back to the Home temperature at wake-up (if someone is home)
- 🛡️ **Robust** - Restart-safe, ignores unavailable persons and an unavailable thermostat

## 📋 Requirements

1. **Climate Entity** - Your heater/thermostat (e.g. `climate.kachel`), with its HVAC mode on `heat`. The blueprint only sets the target temperature, it never switches the heater on or off.
2. **Person entities** - At least two `person.*` entities (with a device tracker such as the Companion app)

### Optional Components

- **Input Boolean** - A sleep switch (e.g. `input_boolean.sleeping`) as alternative to fixed times
- **Extra persons** - Up to two more `person.*` entities

## 🚀 Installation

### Automatic Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fr3mcos3%2Fblueprints%2Fblob%2Fmain%2Fsimple_heating%2Fsimple_heating.yaml)

### Manual Installation

1. In Home Assistant, navigate to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click the **Import Blueprint** button
3. Enter the blueprint URL:
   ```
   https://github.com/r3mcos3/blueprints/blob/main/simple_heating/simple_heating.yaml
   ```
4. Click **Preview** and then **Import**

## ⚙️ Configuration

### Required Settings

| Parameter | Description | Example |
|-----------|-------------|---------|
| 🌡️ Climate Entity | The heater/thermostat to control | `climate.kachel` |
| 👤 Person 1 | First person to track | `person.alice` |
| 👤 Person 2 | Second person to track | `person.bob` |

### 🌡️ Temperatures (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 🏠 Home Temperature | Target when somebody is home and awake | 20°C |
| 🏃 Away Temperature | Target when nobody is home, and while sleeping | 15°C |

### 🌙 Sleep Schedule (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 🌙 Bedtime | From here on the Away temperature is used | 23:00 |
| ☀️ Wake-up Time | From here on the Home temperature is used again | 07:00 |
| 🛏️ Sleep Switch | Optional `input_boolean`, ON = sleeping. Replaces the fixed times | - |

### 👥 Extra Persons (Collapsed)

| Parameter | Description | Default |
|-----------|-------------|---------|
| 👤 Person 3 | Optional third person | - |
| 👤 Person 4 | Optional fourth person | - |

## 🎯 How It Works

### What the target is

| Situation | Target |
|-----------|--------|
| Sleeping (any presence) | 🏃 Away temperature |
| Awake, at least one person home | 🏠 Home temperature |
| Awake, nobody home | 🏃 Away temperature |
| Awake, all persons unavailable | Nothing is changed |

### When the blueprint writes to the thermostat

The blueprint **only** sets the temperature on these events - and nothing else:

| Event | Action |
|-------|--------|
| 🚪 First person arrives (nobody was home) | → Home (not while sleeping) |
| 🚶 Last person leaves | → Away (clears any manual change) |
| 🌙 Bedtime / sleep switch ON | → Away (clears any manual change) |
| ☀️ Wake-up time / sleep switch OFF | → Home, or Away if nobody is home |
| 🔄 HA restart, automation reload, thermostat back online | Re-sync, see below |

A second person arriving while someone is already home, or one person leaving while another stays, does **nothing** - so your manual setting is kept.

### ✋ How manual overrides work (no false detection)

Because the blueprint **never reacts to temperature changes on the thermostat** and only writes on the events above, there is nothing to "detect" and nothing that can mistake its own change for yours. A value you set stays until:

- (a) you change it again (the new value is held), or
- (b) you go to sleep (→ Away), or
- (c) everybody leaves (→ Away).

The morning wake-up always applies the right target as well.

**Why (c)?** An override is meant for "I'm here and it's too cold". Once everyone is gone, that reason is gone too; keeping e.g. 23°C in an empty house wastes energy. Arriving again starts fresh at Home. If you would rather keep the override until bedtime, remove the `all_left` trigger's write in `is_forced_event` - but the default is the safer choice.

### 🔄 Restart and re-sync

After a Home Assistant restart (or automation reload) the blueprint waits 30 seconds for persons and thermostat to come up, then re-syncs. Since nothing is remembered, it uses a simple rule: if the thermostat still sits on the **Home or Away value** (±0.3°C) it is corrected to what it should be (this repairs a missed bedtime/wake-up while HA was down). Any **other value** is treated as your manual setting and left alone. The same re-sync runs when the thermostat comes back from `unavailable`.

> ⚠️ Limitation: a manual change to *exactly* the Home or Away temperature (e.g. you set 20°C while away) is indistinguishable from the blueprint's own value, so a restart may reset it. Choose e.g. 20.5°C to hold it across restarts.

### ⚙️ Run mode

`mode: queued` (max 10, silent overflow): runs never overlap and a startup run (which waits 30 seconds) is never cancelled by a presence change - `restart` would do exactly that. Every run re-reads the *current* state and checks that it is still relevant, so queued runs are harmless when events pile up.

### 🛡️ Unavailable entities

- **Persons** that are `unavailable`/`unknown` are ignored. If *all* are unavailable nothing changes. Note: if a home person's tracker drops out while the other person is away, the house is treated as empty until the tracker returns.
- **Thermostat** `unavailable`/`unknown`: nothing is sent; when it comes back it is re-synced.

## 🔧 Troubleshooting

| Problem | Check |
|---------|-------|
| Temperature changes but heater does not heat | HVAC mode must be `heat`; this blueprint only sets the target |
| Nothing happens at bedtime | With a sleep switch selected, the fixed times are ignored |
| Manual value gets replaced | Last person left, bedtime, or restart with value equal to Home/Away temp |
| Away at the wrong moment | Check that the person's device tracker is reliable (see automation trace) |

## 📝 Version History

### v1.0.0
- 🎉 Initial release: Home/Away temperatures, presence of 2-4 persons, sleep schedule or sleep switch, stateless manual override, restart-safe re-sync

## ❓ FAQ

**Q: Why no periodic check?**
A: A periodic sync would be unable to tell your manual change from a stale value, and would undo it. Events plus a restart re-sync cover all cases.

**Q: Can I use only one person?**
A: Two are required; select the same person twice if needed.

**Q: Can I get weekday/weekend times?**
A: Use the sleep switch and toggle it from your own automations.

## 🤝 Contributing

Found a bug or have a suggestion? Please [open an issue](https://github.com/r3mcos3/blueprints/issues) on GitHub!

## 📄 License

This blueprint is provided as-is under the MIT License.

## 🙏 Credits

Created by [r3mcos3](https://github.com/r3mcos3)
