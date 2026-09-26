---
description: Documentation for eTools - custom tools and utilities plugin for Paper, Purpur, and Folia.
---

# eTools

**eTools** (`v0.0.1-RELEASE`) is a custom tools plugin for Paper, Purpur, and Folia servers running Minecraft 1.21+. It provides configurable tools with area mining, tree felling, AoE farming, AoE shearing, and infinite utility items, all with an optional lifespan system.

[![bStats Servers](https://img.shields.io/bstats/servers/33947?style=for-the-badge&logo=minecraft&logoColor=white&label=bStats%20Servers&color=00D26A)](https://bstats.org/plugin/bukkit/eTools/33947)
[![bStats Players](https://img.shields.io/bstats/players/33947?style=for-the-badge&logo=minecraft&logoColor=white&label=bStats%20Players&color=1085FF)](https://bstats.org/plugin/bukkit/eTools/33947)

---

## Tool Types

**Drills and Shovels (`DRILL`, `SHOVEL`)**
Break blocks in a configurable area defined by three dimensions: **width x height x depth**. The area automatically rotates to match the face the player is mining:

- Mining a **wall** (facing North/South/East/West) opens a vertical tunnel — width spans horizontal, height spans vertical.
- Mining a **floor or ceiling** (looking up/down) clears a flat horizontal plane — width and height span the X/Z axes relative to the player's facing direction.
- The **depth** field extends the area further into the wall or downward, enabling true 3D shapes like `3x3x3` or `3x3x5`.

Drill target blocks include all stone, ore, deepslate, netherrack, end stone, sandstone, basalt, blackstone, tuff, and similar. Shovel target blocks include dirt, grass, sand, gravel, clay, mud, soul sand, soul soil, and snow.

**Tree Feller (`AXE`)**
Fells a connected tree in one swing using BFS traversal. Continues to adjacent logs of the same type up to a configurable block limit (default: 500, configurable via `max-tree-feller-blocks` or per-tool `max-logs`). Connected leaves are removed automatically after felling if `tree-feller-decay-leaves` is enabled.

**Farming Hoes (`HOE`)**
Two distinct behaviors depending on what the player clicks:

- **Mature crops** — harvests all mature crops (wheat, carrots, potatoes, beetroots, nether wart, cocoa, pitcher crops, torchflowers) in the configured area, then replants seeds at age 0 automatically.
- **Hoe-mineable blocks** — breaks blocks in a directional area using the same `width x height x depth` system as drills. Supported blocks include hay bales, sculk family, moss, leaves, sponges, froglights, melons, pumpkins, and others in the `MINEABLE_HOE` tag.

**AoE Shears (`SHEARS`)**
Shears all adult sheep within range simultaneously or harvests leaves, cobwebs, vines, and tall grass in a directional area.

**Infinite Utility Items**
Items that do not consume the item on use:

- `INFINITE_PEARL` — ender pearl throw with configurable cooldown
- `INFINITE_ROCKET` — elytra boost with configurable cooldown
- `INFINITE_BUCKET` — place water or lava; placed fluid evaporates automatically after `temporary-duration` seconds (default: 10s) to prevent abuse
- `INFINITE_GOLDEN_APPLE` — eat golden apple with cooldown
- `INFINITE_STEAK` — eat steak with cooldown

---

## Lifespan System

Each tool can be configured with one of three expiry modes:

| Mode | Behavior |
|:---|:---|
| `ONLINE_TIME` | Counts down only while the player is online. Pauses on disconnect. |
| `REAL_TIME` | Counts down in real-world time regardless of login status. |
| `UNLIMITED` | No expiry. Tool lasts indefinitely. |

Remaining time is stored per-item UUID in the database and displayed in the item lore via the `<time_remaining>` placeholder.

---

## Natural Only Mode

Players can toggle **Natural Only** mode via `/etools settings`. When enabled, area mining skips any block that was placed by a player (detected via PDC metadata or CoreProtect integration), so the tool only breaks naturally generated terrain.

---

## Pages

- [Installation & Setup](Installation-and-Setup.md)
- [Commands & Permissions](Commands-and-Permissions.md)
- [Custom Tools Guide](Custom-Tools-Guide.md)
- [Configuration Guide](Configuration-Guide.md)
- [Database & Lifespans](Database-and-Lifespans.md)

---

## Purchasing

eTools requires a license key to run. Keys are sold through the EproMC Discord server and are bound to your server's IP address. Open a ticket in the `#purchase` channel. After purchasing, place the key in `plugins/eTools/license.yml`.

---

## Support

- Discord: [discord.gg/sVWuc49eYV](https://discord.gg/sVWuc49eYV)
