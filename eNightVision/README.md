---
description: Official Documentation for eNightVision — Modern Client-Side Night Vision Mod with Dynamic Island HUD for Minecraft 26.3.
---

# 👁️ eNightVision Overview

Welcome to the official documentation for **eNightVision** — a sleek, lightweight, client-side utility mod for **Minecraft 26.3** featuring a modern **Dynamic Island notification HUD**, spring physics animations, soft toast sound FX, and strict local-player isolation.

[![Version](https://img.shields.io/badge/version-1.0.0--RELEASE-00D26A.svg?style=for-the-badge)](https://modrinth.com/mod/enightvision)
[![Minecraft](https://img.shields.io/badge/Minecraft-26.3-00F2FE.svg?style=for-the-badge)](https://www.minecraft.net)
[![Loaders](https://img.shields.io/badge/loaders-Fabric%20%7C%20NeoForge%20%7C%20Forge-yellow.svg?style=for-the-badge)](https://fabricmc.net)
[![Java](https://img.shields.io/badge/java-25+-orange.svg?style=for-the-badge)](https://www.oracle.com/java/)
[![Discord](https://img.shields.io/badge/Discord-Join%20Community-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/sVWuc49eYV)
[![Ko-fi](https://img.shields.io/badge/Donate-Ko--fi-FF5E5B.svg?style=for-the-badge&logo=kofi&logoColor=white)](https://ko-fi.com/epromite/tip)
[![Trakteer](https://img.shields.io/badge/Donate-Trakteer-be1e2d.svg?style=for-the-badge)](https://trakteer.id/epromite/tip)

{% hint style="success" %}
**100% Client-Side:** eNightVision runs entirely on your Minecraft client. It does not require any server-side plugins or mod installations, making it safe to use on vanilla multiplayer servers, survival worlds, cave expeditions, and creative building projects.
{% endhint %}

---

## 🌟 Why eNightVision?

Most traditional night vision mods or potion effect hacks suffer from notable shortcomings:
* ❌ **Intrusive Popups:** Plain chat messages or clunky actionbar texts that clash with server announcements or boss bars.
* ❌ **Entity Leak Glitches:** Naive mixin injections in `LivingEntity.hasEffect()` that inadvertently give fake night vision states to villagers, zombies, or nearby players.
* ❌ **Harsh Audio:** Loud, jarring wooden button sounds upon toggling.
* ❌ **Rigid Interfaces:** Stiff animations that glitch out or reset violently when the hotkey is pressed multiple times in quick succession.

**eNightVision** re-imagines client-side utilities from the ground up:
* ✨ **Sleek Dynamic Island HUD:** An organic obsidian pill smoothly glides down from the top of the screen with elastic spring physics, tactile squash & stretch bounce, and glowing shockwave halos.
* ✨ **Color-Morphing Status:** Seamlessly shifts between **Electric Cyan Blue (`#00D2FF`)** for `[ ON ]` and **Coral Red (`#FF5555`)** for `[ OFF ]`.
* ✨ **Spam-Proof Fluidity:** Rapid hotkey presses dynamically pulse the pill with a natural heartbeat animation instead of resetting the animation from scratch.
* ✨ **Strict Local-Player Identity Check:** Only your client player (`Minecraft.getInstance().player`) receives the simulated effect. Other entities remain completely unaffected.
* ✨ **Pleasant Toast SFX:** Gentle vanilla modern toast chimes (`UI_TOAST_IN` and `UI_TOAST_OUT`) provide subtle, satisfying feedback.

---

## 🚀 Feature Highlights

| Feature | Description |
| :--- | :--- |
| **🏝️ Dynamic Island HUD** | Physics-based pill with squash & stretch, shockwave glow ring, and auto-dismiss timer. |
| **🎨 High-Contrast Colors** | Electric Cyan Blue (`#00D2FF`) and Soft Coral Red (`#FF5555`) status styling. |
| **🛡️ Safe Local-Player Mixin** | Zero mob or multiplayer visual glitches; strictly client-player targeted. |
| **🎵 Gentle Audio SFX** | Modern toast chimes with customized pitch curves for ON and OFF states. |
| **⌨️ Vanilla Keybind Menu** | Custom `eNightVision` category in Options -> Controls -> Key Binds (Default: `N`). |
| **💾 Persistent JSON Config** | State preserved across world changes, dimension teleports, and client restarts. |
| **🧩 Mod Menu Integration** | Direct Discord link button and custom Ko-fi & Trakteer donation badges. |

---

## 🧭 Documentation Navigation

Explore the documentation guides below:
* [📥 Installation & Setup](Installation-and-Setup.md) — System requirements, loader setup, and installation steps.
* [🏝️ Dynamic Island & Controls](Dynamic-Island-and-Controls.md) — Deep dive into the Dynamic Island HUD, physics, and keybinds.
* [⚙️ Configuration Guide](Configuration-Guide.md) — Comprehensive guide to `config/enightvision.json` and options.

---

## 💖 Support the Project

eNightVision is free to download and use under **All Rights Reserved (ARR)**. If this mod enhances your Minecraft experience, consider supporting the creator:

* ☕ **Ko-fi:** [https://ko-fi.com/epromite/tip](https://ko-fi.com/epromite/tip)
* 🇮🇩 **Trakteer:** [https://trakteer.id/epromite/tip](https://trakteer.id/epromite/tip)
* 💬 **Discord Support:** [https://discord.gg/sVWuc49eYV](https://discord.gg/sVWuc49eYV)
