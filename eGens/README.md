---
description: Documentation for eGens - generator and tycoon plugin for Paper, Purpur, and Folia.
---

# eGens

**eGens** (`v1.0.1-RELEASE`) is a generator and tycoon plugin for Paper, Purpur, and Folia servers. It ships with 28 pre-configured generator types and is designed for Gens, Skyblock, and Prison server gamemodes.

[![Modrinth Version](https://img.shields.io/badge/Modrinth-v1.0.1-00AF5C?style=for-the-badge&logo=modrinth&logoColor=white)](https://modrinth.com/plugin/egens/version/1.0.1)
[![Platform](https://img.shields.io/badge/platform-Paper%20%7C%20Folia%20%7C%20Purpur-00F2FE.svg?style=for-the-badge)](https://papermc.io)
[![Java](https://img.shields.io/badge/java-21+%20%7C%2025-orange.svg?style=for-the-badge)](https://www.oracle.com/java/)

---

## Features

**Generator Configuration**
Each generator is defined in a single YAML file under `generators/<name>_generator.yml`. The file contains all settings for that generator: stats, drop tables, drop tiers, hologram text, and GUI definition. No shared config files.

**Anti-Abuse Drop Lock**
Items dropped by generators use a custom namespaced tag (`egens:drop_id`). Tagged items cannot be placed as blocks, used in crafting, smelted, brewed, or fed to mobs. They can only be stored in chests or sold.

**Corruption and Repair**
Generators can be configured to degrade over time. After a set number of ticks or drops, the generator block changes to a cracked texture and stops producing until the player repairs it. Supports three modes: `CHANCE`, `DURABILITY`, and `HYBRID`.

**Physical World Drops**
Items drop directly into the world at the generator's location with configurable scatter physics and custom glow rendering. No virtual inventory or abstract drop system.

**Economy and Sellwands**
Includes `/sell` and `/egens sell` for direct selling, chest sellwands with configurable multipliers, and an in-game generator shop via `/egens shop`.

**Multiplier Events**
Server-wide and per-player events can boost sell rates, drop amounts, drop tiers, or generator speed. Events can be scheduled or triggered on demand. Multiple events stack additively and are shown via BossBar.

**Performance**
Generators use Folia region schedulers on Folia servers and async tasks on Paper/Purpur. Generator tick timers are rescheduled immediately when a generator is upgraded or promoted, without desync.

---

## Pages

- [Installation & Setup](Installation-and-Setup.md)
- [Commands & Permissions](Commands-and-Permissions.md)
- [Generators & Progression](Generators-and-Tiers.md)
- [Drops, Economy & Sell Wands](Drops-and-Economy.md)
- [GUI Customization Guide](GUI-Customization.md)
- [Events & Multipliers](Events-and-Multipliers.md)
- [Configuration Guide](Configuration-Guide.md)
- [Database, Anti-Dupe & Performance](Database-and-AntiDupe.md)

---

## Support

- Discord: [discord.gg/sVWuc49eYV](https://discord.gg/sVWuc49eYV)
- Trakteer: [trakteer.id/epromite/tip](https://trakteer.id/epromite/tip)
- Ko-fi: [ko-fi.com/epromite/tip](https://ko-fi.com/epromite/tip)
