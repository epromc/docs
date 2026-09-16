---
description: Comprehensive documentation for eGens - Next-Gen Item Generator, Tycoon, and Corruption Engine for Paper & Folia.
---

# ⚡ Overview & Introduction

Welcome to the official **eGens** (`v1.0.1-RELEASE`) documentation on [GitBook](https://epromc.gitbook.io/egens)!

[![Modrinth Version](https://img.shields.io/badge/Modrinth-v1.0.1-00AF5C?style=for-the-badge&logo=modrinth&logoColor=white)](https://modrinth.com/plugin/egens/version/1.0.1)
[![Platform](https://img.shields.io/badge/platform-Paper%20%7C%20Folia%20%7C%20Purpur-00F2FE.svg?style=for-the-badge)](https://papermc.io)
[![Java](https://img.shields.io/badge/java-21+%20%7C%2025-orange.svg?style=for-the-badge)](https://www.oracle.com/java/)

{% hint style="success" %}
**eGens** is an enterprise-grade Minecraft Generator / Tycoon plugin engineered for high-performance **Paper, Purpur, and Folia** servers (supporting Minecraft **1.20.4 – 1.21.x** and **26.1.2 – 26.2** on **Java 21+ & Java 25**). Featuring **28 unified standalone generator configurations**, physical world-drop loot dispatch, an innovative **generator corruption & repair system**, strict anti-abuse drop locking, dynamic tick rescheduling, SuperiorSkyblock2-style YAML GUI DSL, integrated sellwands, server-wide multiplier events, HikariCP SQLite/MySQL storage, and anti-dupe integrity.
{% endhint %}

---

## 🚀 Key Highlights

* **Unified 1-YAML Generator Configs:** Each of the **28 bundled generators** (`wood`, `iron`, `diamond`, `ice`, `lightning`, `wither`, etc.) is fully self-contained in its own YAML file under `generators/<name>_generator.yml`, holding both its stats and custom drop definitions.
* **Strict Anti-Abuse Drop Lock:** Drop items (`egens:drop_id`) cannot be placed, crafted, brewed, used in furnaces, fed to mobs, or placed in workstations—strictly locked for chest storage and selling.
* **Dynamic Tick Rescheduling:** Upgrading or promoting a generator immediately reschedules the generation timer dynamically with zero desync.
* **Generator Obstruction Protection:** Players cannot place blocks directly above active generators, protecting holograms and item drop paths.
* **Hologram & Skin Persistence:** `GeneratorChunkListener` ensures floating TextDisplays and corrupted block skins automatically re-spawn when chunks load or across late-loaded worlds (Multiverse).
* **Generator Corruption & Repair:** Dynamic block wear where generators degrade into cracked blocks (`CHANCE`, `DURABILITY`, or `HYBRID` mode) requiring player maintenance.
* **Physical World-Drop Loot:** Generators drop custom-named, glow-rendered items directly into the world with configurable scatter physics.
* **SuperiorSkyblock2-Style YAML GUI DSL:** Fully customizable matrix-based menus with click sound effects, pagination, and multi-action buttons.
* **Built-in Economy & Sellwands:** Integrated `/sell` & `/egens sell` direct pipelines, chest sellwands with multipliers, and an in-game generator shop (`/egens shop`).
* **Server-Wide & Personal Events:** Scheduled or on-demand multiplier events (`sell_multi`, `drop_amount`, `drop_tier`, `speed_boost`, `mixed_up`) with additive stacking and BossBar notifications.
* **Native Folia Regional Multi-Threading:** Native region-scheduler support ensures zero lag spikes on both single-threaded Paper and multi-threaded Folia cores.
* **Live In-Process Profiler & Automated Backups:** Monitor tick budgets via `/egens perf` and create atomic live database snapshots via `/egens backup`.

---

## 📑 Quick Navigation

* [📥 Installation & Setup](Installation-and-Setup.md) — System requirements, automatic library loader, and soft dependencies.
* [⌨️ Commands & Permissions](Commands-and-Permissions.md) — Complete player and administrator command reference with permission nodes.
* [💎 Generators & Progression](Generators-and-Tiers.md) — Generator tiers, chains, corruption mechanics, repairs, and holograms.
* [💰 Drops, Economy & Sell Wands](Drops-and-Economy.md) — Loot tables, drop velocity, direct selling, sellwands, and shop system.
* [🖼️ GUI Customization Guide](GUI-Customization.md) — Designing menus using the matrix DSL, custom heads, and actions.
* [🎉 Events & Multipliers](Events-and-Multipliers.md) — Global and personal multiplier events, auto-triggers, and BossBars.
* [⚙️ Configuration Guide](Configuration-Guide.md) — Deep dive into `config.yml`, chain files, and localization.
* [🗄️ Database, Anti-Dupe & Performance](Database-and-AntiDupe.md) — HikariCP backends, automated snapshots, profiler, and anti-dupe integrity.

---

## 🔗 Useful Links & Community

* 📖 **Live Documentation:** [https://epromc.gitbook.io/egens](https://epromc.gitbook.io/egens)
* 💬 **Discord Support:** [https://discord.gg/sVWuc49eYV](https://discord.gg/sVWuc49eYV) — For questions, setup assistance, or bug reports, feel free to contact us via Discord.
* 🐛 **Report Issues & Bugs:** [GitHub Issues](https://github.com/epromc/egens-plugins/issues)

---

## 💖 Support the Developer

If **eGens** helps power your server's economy, please consider supporting ongoing development:

[![Trakteer](https://img.shields.io/badge/Support-Trakteer-be1e2d.svg?style=for-the-badge)](https://trakteer.id/epromite/tip)
[![Ko-fi](https://img.shields.io/badge/Support-Ko--fi-FF5E5B.svg?style=for-the-badge&logo=kofi&logoColor=white)](https://ko-fi.com/epromite/tip)

* 🔴 **Trakteer Tip:** [https://trakteer.id/epromite/tip](https://trakteer.id/epromite/tip)
* ☕ **Ko-fi Tip:** [https://ko-fi.com/epromite/tip](https://ko-fi.com/epromite/tip)
