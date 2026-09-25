---
description: Documentation for eHome - home management plugin for Paper, Purpur, and Folia.
---

# eHome

**eHome** (`v0.0.1-RELEASE`) is a home management plugin for Paper, Purpur, and Folia servers running Minecraft 1.21+. It replaces the standard `/sethome` and `/home` commands with a bed-themed GUI and adds features like home sharing and multi-database support.

[![bStats Servers](https://img.shields.io/badge/bStats%20Servers-Active-00D26A?style=for-the-badge&logo=minecraft&logoColor=white)](https://bstats.org)
[![Platform](https://img.shields.io/badge/platform-Paper%20%7C%20Folia%20%7C%20Purpur-00F2FE.svg?style=for-the-badge)](https://papermc.io)
[![Java](https://img.shields.io/badge/java-21+-orange.svg?style=for-the-badge)](https://www.oracle.com/java/)

---

## Features

**Bed-Themed GUI**
The `/homes` command opens a chest GUI where each home is represented by a colored bed. Players can choose from 16 colors, pin favorites, and browse multiple pages if they have many homes.

**Safe Teleportation**
Before teleporting, eHome checks the destination for hazards — lava, fire, suffocation blocks, and drops into the void. If the saved location is unsafe, the plugin looks for a nearby safe spot before teleporting.

**Home Sharing**
Players can invite others to their homes using `/home share <player> <home>`. The invited player receives a clickable **[ACCEPT]** / **[DECLINE]** prompt in chat. Accepted shares grant a one-time or persistent teleport depending on configuration.

**Bedrock Support**
eHome integrates with Geyser and Floodgate to show native Bedrock UI forms for players connecting from mobile or console clients.

**Database Support**
Supports SQLite (default), MySQL, MariaDB, PostgreSQL, and H2 through HikariCP connection pooling. Migrations run automatically on startup.

**Folia and Paper**
Uses Folia region schedulers when running on Folia, and Paper's async task system otherwise. No main-thread blocking.

---

## Pages

- [Installation & Setup](Installation-and-Setup.md)
- [Commands & Permissions](Commands-and-Permissions.md)
- [GUI & Customization](GUI-and-Customization.md)
- [Configuration Guide](Configuration-Guide.md)
- [Database & Storage](Database-and-Storage.md)

---

## Support

- Discord: [discord.gg/sVWuc49eYV](https://discord.gg/sVWuc49eYV)
- bStats: [bstats.org/plugin/bukkit/eHome](https://bstats.org/plugin/bukkit/eHome)
- Trakteer: [trakteer.id/epromite/tip](https://trakteer.id/epromite/tip)
- Ko-fi: [ko-fi.com/epromite/tip](https://ko-fi.com/epromite/tip)
