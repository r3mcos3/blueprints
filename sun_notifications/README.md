# ☀️ Sun Notifications

## 🌅 Get notified at sunrise and sunset.

This Home Assistant blueprint allows you to receive notifications at sunrise and/or sunset, with configurable offsets and custom messages.

### ✨ Features:
-   Enable/disable sunrise and sunset notifications independently.
-   Set custom time offsets for both sunrise and sunset events.
-   Define personalized notification messages, supporting Jinja2 templating.
-   Specify a notification target (device or group).

### 🛠️ Configuration:
1.  **Notification Target:** Select the device or group that will receive the notifications.
2.  **Enable Sunrise Notification:** Toggle to enable or disable notifications for sunrise.
3.  **Sunrise Offset:** Adjust the time relative to sunrise (e.g., `-00:30:00` for 30 minutes before sunrise).
4.  **Sunrise Message:** Customize the message sent at sunrise.
5.  **Enable Sunset Notification:** Toggle to enable or disable notifications for sunset.
6.  **Sunset Offset:** Adjust the time relative to sunset (e.g., `00:15:00` for 15 minutes after sunset).
7.  **Sunset Message:** Customize the message sent at sunset.

---
**Version:** 1.0.0
**Source:** https://github.com/r3mcos3/blueprints/blob/main/sun_notifications/sun_notifications.yaml
