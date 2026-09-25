---
description: Documentation for eTools - custom tools and utilities plugin for Paper, Purpur, and Folia.
---

# eTools

**eTools** (`v0.0.1-RELEASE`) is a custom tools plugin for Paper, Purpur, and Folia servers running Minecraft 1.21+. It lets you configure and distribute custom tools with area effects, tree felling, farming automation, and infinite utility items — all with an optional lifespan tied to player playtime or real-world time.

[![bStats Servers](https://img.shields.io/bstats/servers/33947?style=for-the-badge&logo=minecraft&logoColor=white&label=bStats%20Servers&color=00D26A)](https://bstats.org/plugin/bukkit/eTools/33947)
[![bStats Players](https://img.shields.io/bstats/players/33947?style=for-the-badge&logo=minecraft&logoColor=white&label=bStats%20Players&color=1085FF)](https://bstats.org/plugin/bukkit/eTools/33947)

---

## Features

**Area Mining and Digging**
Drills and shovels break blocks in a 3x3 or 5x5 area based on the direction the player is facing. Horizontal swings clear walls, downward swings clear floors. Target block lists and area sizes are configurable per tool.

**Tree Felling**
Axes fell entire trees in a single swing using BFS traversal, up to a configurable block limit (default: 500). Leaves decay naturally after the trunk is removed.

**Farming Hoes**
Right-clicking tills soil in a 3x3 or 5x5 area. Clicking on a mature crop harvests everything in radius and replants seeds automatically. Supports wheat, carrots, potatoes, beetroot, nether wart, cocoa, and more.

**Infinite Utility Items**
Ender pearls, firework rockets, water and lava buckets, golden apples, and steak can all be configured as infinite-use items with cooldowns. Placed water and lava evaporate after 10 seconds to prevent abuse.

**Tool Lifespans**
Each tool can be set to count down only while the player is online (`ONLINE_TIME`), count down in real-world time regardless of login status (`REAL_TIME`), or have no expiry at all (`UNLIMITED`). Remaining time is shown in the item lore and saved to the database.

**Admin Commands**
`/etools give`, `/etools duration`, and `/etools recall` let you distribute tools, adjust lifespans, and confiscate all active tools across the server — including items stored in containers and unloaded chunks.

**License System**
eTools requires a valid license key to run. Keys are sold through our Discord server and are bound to your server's IP address. The plugin validates the license on startup and runs a periodic heartbeat check.

---

## Pages

- [Installation & Setup](Installation-and-Setup.md)
- [Commands & Permissions](Commands-and-Permissions.md)
- [Custom Tools Guide](Custom-Tools-Guide.md)
- [Configuration Guide](Configuration-Guide.md)
- [Database & Lifespans](Database-and-Lifespans.md)

---

## Purchasing

eTools is sold exclusively through our Discord server. Open a ticket in the `#purchase` channel to get started. After completing the purchase, you will receive a license key to place in `plugins/eTools/license.yml`.

---

## Live Statistics

[![bStats Statistics](https://bstats.org/signatures/bukkit/eTools.svg)](https://bstats.org/plugin/bukkit/eTools/33947)

---

## Support

- Discord: [discord.gg/sVWuc49eYV](https://discord.gg/sVWuc49eYV)
- Trakteer: [trakteer.id/epromite/tip](https://trakteer.id/epromite/tip)
- Ko-fi: [ko-fi.com/epromite/tip](https://ko-fi.com/epromite/tip)
