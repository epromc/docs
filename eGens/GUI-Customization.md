---
description: Guide to customizing eGens menus using the SuperiorSkyblock2-style YAML matrix DSL, button actions, custom heads, and sounds.
---

# 🖼️ GUI Customization Guide

**eGens** features a modular GUI layout engine modeled after the industry-standard **SuperiorSkyblock2 pattern matrix DSL**. You have full control over menu rows, item positions, button actions, head textures, and sound feedback.

---

## 📐 The Pattern Matrix DSL

Every GUI file inside `plugins/eGens/gui/` defines its layout using a visual ASCII character grid where each character corresponds to a slot on the chest inventory.

```yaml
title: "<gray>Generator Management</gray>"
rows: 5

pattern:
  - "#########"
  - "#.......#"
  - "#.R.I.U.#"
  - "#.......#"
  - "####C####"
```

### Slot Mapping Matrix
Each character in `pattern` maps to a definition in the `items:` block:

```yaml
items:
  '#':
    material: GRAY_STAINED_GLASS_PANE
    name: " "
    action: NONE

  'I':
    material: "<generator-material>"
    name: "<gold><bold><tier-display> Generator</bold></gold>"
    lore:
      - "<gray>Owner: <white><owner></white></gray>"
      - "<gray>Level: <aqua><level>/<max_level></aqua></gray>"
      - "<gray>Durability: <green><durability>/<max_durability></green></gray>"
    action: NONE

  'U':
    material: EMERALD
    name: "<green><bold>Upgrade Generator</bold></green>"
    lore:
      - "<gray>Cost: <gold>$<upgrade_cost></gold></gray>"
      - "<yellow>Click to upgrade level!</yellow>"
    action: UPGRADE
    click-sound: ENTITY_EXPERIENCE_ORB_PICKUP:1.0:1.0

  'R':
    material: ANVIL
    name: "<red><bold>Repair Generator</bold></red>"
    lore:
      - "<gray>Repair Cost: <gold>$<repair_cost></gold></gray>"
      - "<yellow>Click to restore durability!</yellow>"
    action: REPAIR
    click-sound: BLOCK_ANVIL_USE:1.0:1.0

  'C':
    material: BARRIER
    name: "<red>Close Menu</red>"
    action: CLOSE
```

---

## ⚡ Button Actions

Buttons in eGens GUIs support diverse built-in interactive actions:

| Action | Description |
| :--- | :--- |
| `UPGRADE` | Initiates generator level upgrade or tier promotion. |
| `REPAIR` | Initiates corruption repair and restores durability. |
| `SETTINGS` | Opens the personal preferences menu. |
| `CLOSE` | Closes the player's active inventory. |
| `OPEN_GUI:<gui_name>` | Opens another GUI file (e.g. `OPEN_GUI:shop`). |
| `COMMAND:<cmd>` | Forces the player to execute a command (e.g. `COMMAND:egens help`). |
| `CONSOLE_COMMAND:<cmd>` | Executes a command from the server console with `{player}` replacement. |
| `NONE` | Static decorative item; cancels clicks without action. |

---

## 💀 Custom Heads & Textures

eGens natively supports three formats for custom head items in menus:

1. **HeadDatabase (HDB):**
   ```yaml
   material: PLAYER_HEAD
   head-texture: "hdb:12345"
   ```
2. **Base64 Skins:**
   ```yaml
   material: PLAYER_HEAD
   head-texture: "eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6Imh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUv..."
   ```
3. **Player Head by Username:**
   ```yaml
   material: PLAYER_HEAD
   owner: "{player}" # Resolves to the viewing player's skin
   ```

---

## 🎵 Click Audio Feedback

Attach audio feedback to any button by specifying `click-sound:` with `<sound>:<volume>:<pitch>`:

```yaml
click-sound: UI_BUTTON_CLICK:0.8:1.2
```

---

## 🔄 Live Hot Reloading

All GUI files are re-evaluated live. After editing any YAML file in `plugins/eGens/gui/`, reload changes in-game instantly:

```bash
/egens reload
```
