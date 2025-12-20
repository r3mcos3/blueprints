# ☀️ Sun-aware Motion Light

[![version](https://img.shields.io/badge/version-1.0-blue.svg)](https://github.com/r3mcos3/blueprints)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.12.0%2B-blue.svg)](https://www.home-assistant.io/)

This blueprint creates an automation that turns on a light when motion is detected. It can optionally use different brightness levels based on the sun's position.

## Version

-   **1.0**: Initial release.

## Requirements

Requires Home Assistant 2025.12.0 or newer.

## Inputs

| Input | Description | Default |
| --- | --- | --- |
| `motion_sensor` | The 🏃‍♂️ motion sensor that detects presence. | (required) |
| `target_light` | The 💡 light or group of lights controlled by this automation. | (required) |
| `default_brightness`| The 🔆 brightness percentage to use when sun-aware mode is disabled. | `80` |
| `sun_aware_settings` | **Collapsible Section:** Configure brightness levels 🌓 based on the sun's position ☀️🌙. | |
| &nbsp;&nbsp;&nbsp;&nbsp;`sun_aware_enabled` | Enable 🟢 to use different brightness levels for day and night. If 🔴 disabled, a single brightness level is used. | `true` |
| &nbsp;&nbsp;&nbsp;&nbsp;`brightness_day` | The ✨ brightness percentage for when the sun ☀️ is up. | `100` |
| &nbsp;&nbsp;&nbsp;&nbsp;`brightness_night`| The ✨ brightness percentage for when the sun 🌙 is down. | `10` |
| `turn_off_delay` | The ⏱️ wait time in minutes before the light turns off after no motion is detected. Set to 0 for no delay. | `5` |

## How it works

-   When motion is detected (`on`), the light turns on.
    -   If "Sun-aware Mode" is enabled (within "Sun-aware Settings"):
        -   If the sun is `above_horizon`, it uses the "Brightness (Day)".
        -   Otherwise, it uses the "Brightness (Night)".
    -   If "Sun-aware Mode" is disabled, it uses the "Default Brightness".
-   When motion stops (`off`) for the specified `turn_off_delay` duration (in minutes), the light turns off. If the delay is 0, it turns off immediately.
