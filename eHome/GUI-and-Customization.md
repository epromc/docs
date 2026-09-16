---
description: Deep dive into eHome's pattern-based matrix GUI, 16-color bed palette, Bedrock touch menus, and sound effects.
---

# 🛏️ Bed-Themed GUI & Customization

**eHome** introduces an innovative bed-themed visual management interface that replaces drab text lists with an intuitive, interactive experience.

---

## 📐 Matrix Pattern Layout Engine

The main Homes GUI (`/homes` or `/home`) is configured in `/plugins/eHome/gui.yml` using a flexible matrix pattern:

```yaml
menu:
  title: "<#4A90E2>✦ <white>ᴇʜᴏᴍᴇ <black>• <#A0AEC0>ʏᴏᴜʀ ʜᴏᴍᴇꜱ"
  rows: 4
  pattern:
    - "#########"
    - "#I#HHHHH#"
    - "#G#######"
    - "###P###N#"
```

### Supported Pattern Tokens:
* `#` — **Filler / Border:** Custom material (e.g. `BLACK_STAINED_GLASS_PANE`).
* `I` — **Player Info Head:** Renders the player's skull with real-time home count, limit, and pinned favorite.
* `G` — **Guide & Help:** Explains all interactive click controls.
* `H` — **Dynamic Home Slots:** Automatically paginates through active homes. Available slots show lime glass, while locked quota slots display red glass.
* `P` — **Previous Page Button:** Appears when earlier pages exist.
* `N` — **Next Page Button:** Appears when more homes exceed the current page.
* `A` — **Optional Action Slot:** Dedicated button for renaming, pinning, or deleting a specific home.

---

## 🎮 Interactive Click Controls

Every home icon in the GUI supports intuitive multi-action clicks:

| Action | Control | Result |
| :--- | :--- | :--- |
| **Teleport** | `Left-Click` | Initiates safe teleportation with warmup countdown and sound feedback. |
| **Change Color** | `Right-Click` | Opens the **16-Color Bed Picker** GUI to choose a new bed icon. |
| **Pin Favorite** | `Shift + Left-Click` | Toggles pinned status. Pinned homes appear first and receive a golden star badge (`⭐`). |
| **Delete Home** | `Shift + Right-Click` | Immediately deletes the home with an acoustic bass drop confirmation sound. |

---

## 🎨 16-Color Bed Picker Palette

Players can customize their home icons using any of Minecraft's 16 official bed colors:

* `WHITE_BED`, `LIGHT_GRAY_BED`, `GRAY_BED`, `BLACK_BED`
* `BROWN_BED`, `RED_BED`, `ORANGE_BED`, `YELLOW_BED`
* `LIME_BED`, `GREEN_BED`, `CYAN_BED`, `LIGHT_BLUE_BED`
* `BLUE_BED`, `PURPLE_BED`, `MAGENTA_BED`, `PINK_BED`

---

## 📱 Geyser & Floodgate Support (Bedrock Touch Menus)

For cross-play servers using **Geyser** and **Floodgate**:

* **Native Cumulus Forms:** When a player on Bedrock (Mobile, Xbox, PlayStation, Switch) types `/home` or `/homes`, eHome bypasses the chest inventory and opens a native Bedrock Form dialog.
* **Touch-Friendly Buttons:** Each home appears as a large touchable button showing world, coordinates, and distance.
* **Font Sanitization:** eHome automatically sanitizes Unicode Small Caps typography for Bedrock clients if enabled in `config.yml`, preventing missing character squares (`□`).

---

## 🔊 Immersive Audio Cues

Every interaction features a tailored sound effect:

* **Menu Opening:** Soft book page turn (`ITEM_BOOK_PAGE_TURN`).
* **Button Clicks & Paging:** Crisp mechanical click (`UI_BUTTON_CLICK`).
* **Color Choice & Notifications:** High-pitched bell note (`BLOCK_NOTE_BLOCK_PLING`).
* **Pinning Favorites:** Harmonious bell chime (`BLOCK_NOTE_BLOCK_CHIME`).
* **Deleting Homes:** Low resonant bass tone (`BLOCK_NOTE_BLOCK_BASS`).
* **Teleport Arrival:** Classic teleport shimmer (`ENTITY_PLAYER_TELEPORT`).
* **Safety Violations / Errors:** Rejection tone (`ENTITY_VILLAGER_NO`).
