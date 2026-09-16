---
description: Comprehensive guide to eGens generator tiers, premade chains, corruption mechanics, repair costs, and holographic displays.
---

# 💎 Generators & Progression

Generators are the core gameplay mechanic in **eGens**. Players place generator blocks that automatically produce valuable resources, gain levels, and advance through progression tiers.

---

## 🔗 Unified Generator Configurations (28 Bundled Generators)

In **eGens v1.0.1**, generator configurations are unified into a clean **1-file-per-generator** architecture. Each generator is entirely self-contained inside its own YAML file located under `plugins/eGens/generators/<name>_generator.yml`:

```
plugins/eGens/generators/
├── wood_generator.yml
├── stone_generator.yml
├── iron_generator.yml
├── diamond_generator.yml
├── netherite_generator.yml
├── zombie_generator.yml
├── wither_generator.yml
├── lightning_generator.yml
└── ... (28 standalone generator YAMLs)
```

Each YAML file houses both the **generator block properties** and its **custom drops**, eliminating the need to coordinate between separate chains and drop files.

### The 3 Thematic Progression Paths:
1. 🪵 **Vanilla Progression (10 Tiers):** `wood → stone → copper → iron → gold → redstone → lapis → diamond → emerald → netherite`.
2. 💀 **Mob Progression (10 Tiers):** `zombie → skeleton → spider → creeper → enderman → blaze → ghast → witch → shulker → wither`.
3. ⚡ **Elemental Progression (8 Tiers):** `earth → water → fire → air → ice → lightning → ender → void`.

---

## 📈 Leveling & Tier Promotion

Generators feature a two-phase progression system: **Intra-Tier Leveling** and **Tier Promotion**.

```
[Tier: Iron (Lvl 1)] ──► [Level 2..10] ──► [PROMOTION] ──► [Tier: Gold (Lvl 1)]
```

### 1. Intra-Tier Leveling (Levels 1 – 10)
* Each tier can be upgraded up to `max-level` (default 10).
* Upgrading increases item drop rates and decreases generation intervals.
* Upgrade cost formula (configured in `config.yml`):
  $$\text{Cost} = 500 \times \text{level}^{1.8}$$

### 2. Tier Promotion & Dynamic Tick Rescheduling
* When a generator reaches level 10 and has a `next-tier` specified in its YAML, the player can promote it directly in the GUI or via `/egens upgrade`.
* **Dynamic Tick Rescheduling:** The instant a generator is promoted (e.g. from *Iron* to *Gold*), eGens dynamically unregisters the old timer task and reschedules the new tier's `tick-interval` immediately without server restarts or reload delay.
* Promotion cost formula:
  $$\text{Cost} = 10000 \times \text{tier}$$

### 3. Generator Obstruction Protection
To protect item spawn paths and floating TextDisplays, players are prohibited from placing any block directly above an active generator block. Attempts to place a block above a generator are automatically cancelled.

---

## ⚠️ Generator Corruption & Repair

To prevent infinite passive AFK generation and create gold-sink mechanics, eGens includes a robust **Corruption Engine**.

### Corruption Modes
Configured in `config.yml` under `corruption.mode`:

| Mode | Description |
| :--- | :--- |
| `CHANCE` | Fixed probability per generation tick to become corrupted. |
| `DURABILITY` | Generator loses durability on every drop cycle until hitting 0. |
| `HYBRID` *(Default)* | Combines durability wear with escalating corruption probability at lower durability. |

### What Happens When Corrupted?
1. **Block Material Transformation:** The generator block visually transforms into `corrupted-material` (e.g. `BLACK_WOOL` or `COBBLESTONE`).
2. **Halt Production:** Generation halts completely; no items or drops will spawn until repaired.
3. **Floating Alert:** Holographic display switches to an alert (e.g. `<red><bold>CORRUPTED</bold></red>`).

### Repairing Generators
* **Interaction:** Players right-click the corrupted block to open the Repair menu or run `/egens repair` while looking at it.
* **Repair Cost Formula:**
  $$\text{Cost} = 12.5 \times \text{tier}$$
* **Cooldown:** Configurable cooldown between repair attempts (default: 5 seconds) to prevent spam.

---

## 🔮 Holographic Floating Displays

Every placed generator projects a real-time floating status display:

```
[💎 Diamond Generator]
ʟᴇᴠᴇʟ 4/10  •  ʜɪᴛs 84/100
```

### Supported Hologram Providers
Set via `generator.hologram.provider` in `config.yml`:
* `AUTO` *(Default)*: Probes installed plugins (`DecentHolograms` $\rightarrow$ `FancyHolograms` $\rightarrow$ `HolographicDisplays`) and automatically falls back to `NATIVE`.
* `NATIVE`: Built-in Paper 1.20+ `TextDisplay` entities. Extremely lightweight, requires zero third-party hologram plugins.
* `DECENT`, `FANCY`, `HD`: Explicitly forces the respective third-party provider adapter.

### Display Features
* **Unicode Small Caps Typography:** Elegant native formatting (`ʟᴇᴠᴇʟ`, `ʜɪᴛs`).
* **Text Shadows:** Crisp readability over bright lava, leaves, or sunlight backgrounds.
* **Toggleable Lines:** Individually enable or disable level and durability lines in `config.yml`.
