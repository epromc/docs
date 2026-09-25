---
description: Detailed reference for the eNightVision configuration file (enightvision.json).
---

# ⚙️ Configuration Guide

**eNightVision** features a lightweight, persistent JSON configuration file designed for instant loading with zero game startup overhead.

---

## 📁 File Location

The configuration file is automatically generated upon first launch at:

📁 **`.minecraft/config/enightvision.json`**

{% hint style="tip" %}
You can edit this file while the game is running. When modified, restart your game or re-toggle your hotkey to save the new defaults.
{% endhint %}

---

## 📄 Default Configuration

```json
{
  "enabled": false,
  "rememberStateAcrossSessions": true,
  "playToggleSound": true,
  "showActionBarMessage": false,
  "showHudIndicator": true,
  "dynamicIslandNotification": true
}
```

---

## ⚙️ Configuration Reference

| Option | Type | Default | Description |
| :--- | :---: | :---: | :--- |
| **`enabled`** | `boolean` | `false` | The current active state of night vision. Automatically toggled and persisted when pressing your keybind in-game. |
| **`rememberStateAcrossSessions`** | `boolean` | `true` | When set to `true`, eNightVision preserves your night vision state across server hops, dimension teleports (Nether/End), and world reconnects. |
| **`playToggleSound`** | `boolean` | `true` | Plays a soft, modern toast audio chime (`UI_TOAST_IN` / `UI_TOAST_OUT`) whenever night vision is toggled. Set to `false` for silent operation. |
| **`showActionBarMessage`** | `boolean` | `false` | Whether to display legacy text in the Minecraft action bar above the hotbar. Kept `false` by default in favor of the cleaner Dynamic Island HUD. |
| **`showHudIndicator`** | `boolean` | `true` | Displays a persistent, minimalist `✦ NV` status indicator badge in the top-left corner of the screen while night vision is active. |
| **`dynamicIslandNotification`** | `boolean` | `true` | Enables the animated Dynamic Island pill notification at the top-center of the screen. |

---

## 💡 Recommended Configurations

### 🎯 Minimalist Clean Setup
If you prefer zero on-screen notifications and complete immersion, with only audio feedback:
```json
{
  "enabled": false,
  "rememberStateAcrossSessions": true,
  "playToggleSound": true,
  "showActionBarMessage": false,
  "showHudIndicator": false,
  "dynamicIslandNotification": false
}
```

### 🏝️ Full Dynamic Island Experience (Default)
Optimal balance of modern aesthetics, responsive audio cues, and discreet corner tracking:
```json
{
  "enabled": false,
  "rememberStateAcrossSessions": true,
  "playToggleSound": true,
  "showActionBarMessage": false,
  "showHudIndicator": true,
  "dynamicIslandNotification": true
}
```
