---
description: Breakdown of all tool types, area mechanics, and utility items in eTools.
---

# Custom Tools & Utilities

---

## 1. Drills (`DRILL`) and Shovels (`SHOVEL`)

Area-breaking tools that mine or dig in a configurable 3D volume. The shape is defined by three fields in `tools.yml`:

| Field | Description |
|:---|:---|
| `width` | Span perpendicular to the mining direction |
| `height` | Span along the vertical or forward axis depending on face |
| `depth` | How deep the area extends into the surface |

The three fields combine into a `WxH` or `WxHxD` shape that automatically adapts to the face the player is mining:

**Mining a wall** (facing North, South, East, or West)
The area opens as a vertical plane in front of the player. Width expands horizontally, height expands vertically. If `depth > 1`, the area extends further into the wall - for example, `3x3x3` cuts a cube-shaped tunnel three blocks deep.

**Mining a floor or ceiling** (looking up or down)
The area opens as a flat horizontal plane. Width and height both span the X/Z axes aligned with the player's facing direction. Depth extends further up or down.

You can configure non-square shapes too. A `3x1x1` drill clears a horizontal strip; a `1x3x1` drill clears a vertical strip; a `3x3x3` drill cuts a full cube on each swing.

**Target blocks for Drills:** All pickaxe-mineable blocks - stone, ores, deepslate, netherrack, end stone, sandstone, basalt, blackstone, tuff, granite, diorite, andesite, and similar.

**Target blocks for Shovels:** All shovel-mineable blocks - dirt, grass, sand, gravel, clay, mud, soul sand, soul soil, and snow.

---

## 2. Tree Feller (`AXE`)

Fells an entire connected tree in a single swing using BFS (breadth-first search). Starting from the clicked log, it expands to all adjacent logs of the same type. The search stops when it reaches `max-logs` (per-tool) or the global `max-tree-feller-blocks` setting (default: 500).

Leaves adjacent to felled logs are collected into a separate set and removed after the logs, if `tree-feller-decay-leaves` is enabled in `config.yml`. Protection hooks are checked per-block before each break.

Only works when the first block clicked is a log (`Tag.LOGS`). Does not break logs of different types in the same swing.

---

## 3. Hoes (`HOE`)

Hoes have two distinct behaviors depending on what the player clicks:

**Clicking a mature crop**
Harvests all mature `Ageable` crops in the configured area and replants them at age 0. Area uses `width` and `height` relative to the player's horizontal facing direction (same as floor mode for drills). Also checks one block above and below the clicked block to handle elevated farmland. Supported crops include wheat, carrots, potatoes, beetroots, nether wart, cocoa, pitcher crops, and torchflowers.

**Clicking a hoe-mineable block**
Breaks blocks in a directional `WxHxD` area using the same orientation logic as drills. Hoe-mineable blocks include: all blocks in the `MINEABLE_HOE` tag, all leaves, hay bales, sculk family, moss, sponges, froglights, melons, pumpkins, and dried kelp blocks.

---

## 4. Shears (`SHEARS`)

Breaks shearable blocks in a directional `WxHxD` area. Shearable blocks include: leaves, wool, cobweb, vine, glow lichen, hanging roots, short grass, tall grass, seagrass, ferns, and petal blocks.

---

## 5. Infinite Utility Items

Items that do not consume the held item on use:

| Item | Type | Behavior |
|:---|:---|:---|
| `infinite_pearl` | `INFINITE_PEARL` | Throws ender pearl without consuming it. Configurable cooldown. |
| `infinite_rocket` | `INFINITE_ROCKET` | Fires elytra boost rocket without consuming it. Configurable cooldown. |
| `infinite_water` | `INFINITE_BUCKET` | Places water; evaporates after `temporary-duration` seconds (default: 10s). Cooldown applies. |
| `infinite_lava` | `INFINITE_BUCKET` | Places lava; evaporates after `temporary-duration` seconds (default: 10s). Cooldown applies. |
| `infinite_golden_apple` | `INFINITE_GOLDEN_APPLE` | Eats a golden apple without consuming it. Configurable cooldown. |
| `infinite_steak` | `INFINITE_STEAK` | Eats steak without consuming it. Configurable cooldown. |

---

## Natural Only Mode

Players can toggle **Natural Only** mode from `/etools settings`. When enabled:

- If the clicked block was placed by a player (detected via PDC metadata or CoreProtect), the tool breaks only that single block instead of the full area.
- If the block is naturally generated terrain, the full area applies normally.

This prevents players from accidentally destroying their own builds while using area tools in mines or cobblestone generators.
