# 🛡️ Persistent Motion Light 💡

> **Version:** 1.0

This blueprint turns on a light or switch when motion is detected and ensures it **stays on** as long as motion is present.

## ✨ Features

*   **👀 Motion Activation:** Turns on the light immediately upon motion.
*   **🛡️ Anti-Turn-Off Protection:** If someone manually turns off the switch while motion is still detected, the blueprint will **immediately turn it back on**.
*   **⏳ Smart Delay:** The light only turns off after motion has stopped AND a configurable wait time has passed.
*   **🔄 Restart Logic:** Each new motion event resets the timer, ensuring the light never goes out while you are active.

## ⚙️ Configuration

| Input | Description |
| :--- | :--- |
| **👀 Motion Sensor** | The binary sensor that detects motion. |
| **💡 Light or Switch** | The target entity (light or switch) to control. |
| **⏳ Wait time** | How long to wait (in seconds) after motion stops before turning off. |

## 📝 How it works

1.  The automation triggers when motion starts **OR** when the target light is turned off.
2.  It checks if motion is currently detected.
3.  If motion is detected, it forces the light **ON**.
4.  It waits until the motion sensor reports "no motion".
5.  It waits for the user-defined delay (e.g., 120 seconds).
6.  It turns the light **OFF**.

If motion is detected again during step 5, the automation restarts from step 1, keeping the light on.