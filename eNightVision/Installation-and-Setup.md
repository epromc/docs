---
description: Step-by-step instructions for installing eNightVision on Minecraft 26.3 with Fabric Loader.
---

# 📥 Installation & Setup

## 📌 System Requirements

Before installing **eNightVision**, ensure your environment meets the following specifications:

* **Minecraft Version:** `26.3` (Wilderness Bound release)
* **Java Runtime:** Java 25 or newer
* **Mod Loader:**
  * **Fabric Loader:** `0.16.x` or higher (Recommended)
  * **Fabric API:** Matching 26.3 release
* **Optional Enhancements:**
  * **Mod Menu:** For viewing mod metadata and custom donation / website links in-game.

{% hint style="info" %}
**Client-Side Only:** You do not need to install eNightVision on dedicated servers or realms. Simply drop it into your local Minecraft installation.
{% endhint %}

---

## 📥 Installation Steps

Follow these simple steps to install eNightVision:

### 1. Install Fabric Loader
If you haven't already installed Fabric Loader:
1. Visit the official [Fabric Website](https://fabricmc.net/use/installer/).
2. Download and run the Fabric Installer.
3. Select **Minecraft 26.3** and the latest loader version, then click **Install**.

### 2. Download Required Files
Download the corresponding files:
* **eNightVision:** Download `enightvision-1.0.0.jar` (or `enightvision-fabric-1.0.0.jar`) from [Modrinth](https://modrinth.com/mod/enightvision).
* **Fabric API:** Ensure you have the `fabric-api` jar for Minecraft 26.3 in your mods folder.

### 3. Place in Mods Directory
Open your Minecraft game directory:
* **Windows:** Press `Win + R`, type `%appdata%\.minecraft\mods`, and press `Enter`.
* **macOS:** Open Finder, press `Cmd + Shift + G`, enter `~/Library/Application Support/minecraft/mods`.
* **Linux:** Navigate to `~/.minecraft/mods/`.

Drop both `enightvision-1.0.0.jar` and `fabric-api.jar` into the `mods` folder.

```text
.minecraft/
└── mods/
    ├── fabric-api-*.jar
    ├── enightvision-1.0.0.jar
    └── modmenu-*.jar (optional)
```

### 4. Launch the Game
1. Open your Minecraft Launcher.
2. Select the **Fabric Loader 26.3** profile and click **Play**.
3. Once in the main menu, eNightVision is active and ready to use!

---

## 🔍 Verifying the Installation

To verify that eNightVision is running correctly:
1. Join any singleplayer world or multiplayer server.
2. Press the default key **`N`**.
3. You will immediately see the sleek **Dynamic Island HUD** glide down from the top of your screen with a soft chime:
   * **`[ ON ]`** status in bright electric cyan blue with illuminated visibility.
   * Press **`N`** again to toggle back to **`[ OFF ]`** in coral red.

---

## 🧩 Mod Menu Integration

If you have **Mod Menu** installed, eNightVision provides a customized mod info screen:
* **Website Button:** Directly opens our official [Discord Community Server](https://discord.gg/sVWuc49eYV) for instant support and updates.
* **Donate Section:** Under `Donate:`, you will find direct links to [Ko-fi](https://ko-fi.com/epromite/tip) and [Trakteer](https://trakteer.id/epromite/tip).
* **Branded Icon:** Clean high-resolution logo embedded in the mod list.
