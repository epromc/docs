---
description: Comprehensive guide to the Dynamic Island HUD animation, spring physics, color morphing, and keybind controls.
---

# 🏝️ Dynamic Island & Controls

The hallmark feature of **eNightVision** is its bespoke **Dynamic Island notification HUD**, inspired by modern mobile operating system interactions and engineered with spring physics and tactile feedback.

---

## ⌨️ Controls & Keybinds

eNightVision integrates seamlessly into vanilla Minecraft's keybinding registry:

| Action | Default Key | Category in Settings | Rebindable |
| :--- | :---: | :---: | :---: |
| **Toggle Night Vision** | **`N`** | **`eNightVision`** | ✅ Yes |

### Customizing Keybinds
To change the hotkey:
1. Open the game menu (`Esc`) and navigate to **Options...** → **Controls...** → **Key Binds...**.
2. Scroll down until you see the dedicated category header: **`eNightVision`**.
3. Click on **Toggle Night Vision** and press your desired keyboard key or mouse button (e.g., `G`, `V`, or Mouse 4).
4. Click **Done** to save your preferences.

{% hint style="tip" %}
Your custom keybind is stored in your standard Minecraft `options.txt` and remains persistent across launcher updates.
{% endhint %}

---

## 🏝️ The Dynamic Island HUD

Whenever you toggle night vision, an obsidian pill descends gracefully from the top-center of the screen:

```text
┌────────────────────────────────────────────────────────────┐
│                  ✦ eNightVision   [ ON ]                   │  <- Electric Cyan Blue (#00D2FF)
└────────────────────────────────────────────────────────────┘
```
```text
┌────────────────────────────────────────────────────────────┐
│                  ○ eNightVision   [ OFF ]                  │  <- Soft Coral Red (#FF5555)
└────────────────────────────────────────────────────────────┘
```

### 🧬 Physics & Animation Lifecycle

The HUD uses real-time nanosecond interpolation (`System.nanoTime`) rather than fixed frame ticks, ensuring buttery 144Hz+ and 240Hz+ fluidity regardless of in-game framerate:

1. **Entrance Spring & Expansion:**
   * Rapidly drops down from off-screen (`y = -30px`) to its resting position (`y = 12px`).
   * Horizontally stretches (+22px) and squashes vertically (-3px) to create an organic, tactile rubber-band effect.
2. **Shockwave Halo Glow:**
   * An animated neon halo ring radiates outwards around the pill border, colored according to the active status.
3. **State Color Morphing:**
   * **Active (`ON`):** Bright Electric Cyan Blue (`#00D2FF`) with a radiant star icon (`✦`).
   * **Inactive (`OFF`):** Soft Coral Red (`#FF5555`) with a sleek hollow circle (`○`).
   * State changes transition smoothly in RGB space without visual artifacts.
4. **Hold Duration & Exit Transition:**
   * Remains pinned on-screen for ~2.2 seconds.
   * Smoothly slides back up into the bezel with an exponential decay exit curve.

---

## ⚡ Spam-Proof Interaction

In many mods, pressing a hotkey repeatedly triggers jarring resets, screen tearing, or overlapping HUD layers.

**eNightVision** solves this through intelligent stateful animation tracking:
* When toggled while the island is already visible, the island **does not** snap back to the top or stutter.
* Instead, it absorbs the impact:
  * Triggers an elastic **heartbeat pulse** (downward +4px tactile bounce and horizontal expansion).
  * Instantly begins morphing the text, badges, and glow colors to match the new state.
  * Resets the dismissal timer so the current state remains clearly readable.

---

## 🎵 Dynamic Audio Feedback (SFX)

Complementing the visual HUD, eNightVision uses subtle modern audio cues:

| State | Sound Event | Pitch | Description |
| :--- | :--- | :---: | :--- |
| **Turning ON** | `SoundEvents.UI_TOAST_IN` | `1.25x` | Cheerful, crisp ascending chime. |
| **Turning OFF** | `SoundEvents.UI_TOAST_OUT` | `0.95x` | Gentle, soft descending dismissal. |

{% hint style="info" %}
Audio feedback respects Minecraft's master volume and UI volume sliders. It can also be disabled entirely in `config/enightvision.json`.
{% endhint %}

---

## 📌 Minimal HUD Corner Indicator

In addition to the Dynamic Island popup, eNightVision includes an optional persistent status indicator:
* Positioned in the top-left corner of the screen: `✦ NV`.
* Gives you quiet, permanent reassurance of whether your night vision is active without cluttering the screen.
* Can be toggled on or off in the configuration file.
