---
description: Comprehensive configuration reference for config.yml, generator chain YAMLs, events.yml, and language files in eGens.
---

# ⚙️ Configuration Guide

This guide details the major configuration files inside `plugins/eGens/`. All files support hot-reloading via `/egens reload` without restarting the server.

---

## 🗂️ File Directory Structure

```
plugins/eGens/
├── config.yml            # Core settings, database, corruption, limits, and backup
├── events.yml            # Multiplier event definitions and sound triggers
├── sellwands.yml         # Custom sellwand items and chest multipliers
├── generators/           # 28 Unified standalone generator configuration files
│   ├── wood_generator.yml
│   ├── stone_generator.yml
│   ├── iron_generator.yml
│   ├── diamond_generator.yml
│   ├── netherite_generator.yml
│   ├── zombie_generator.yml
│   ├── wither_generator.yml
│   ├── lightning_generator.yml
│   └── ... (28 standalone generator files)
├── gui/
│   ├── main_hub.yml      # Main eGens hub GUI
│   ├── shop.yml          # Generator shop GUI
│   ├── settings.yml      # Player preferences GUI
│   └── repair.yml        # Generator repair menu
└── lang/
    ├── messages_en.yml   # English localization
    └── messages_id.yml   # Indonesian localization
```

---

## ⚙️ Core Configuration (`config.yml`)

### 1. Storage Backend
```yaml
storage:
  type: SQLITE                  # SQLITE | MYSQL | MARIADB
  mysql:
    host: localhost
    port: 3306
    database: egens
    username: root
    password: ""
    pool-size: 10
    use-ssl: false
  sqlite:
    file: "egens.db"
```

### 2. Generator Appearance & Holograms
```yaml
generator:
  default-material: IRON_BLOCK
  corrupted-material: BLACK_WOOL
  hologram:
    enabled: true
    provider: AUTO              # AUTO | NATIVE | DECENT | FANCY | HD
    view-distance: 32
    show-level: true            # Displays "ʟᴇᴠᴇʟ x/y"
    show-durability: false      # Displays "ʜɪᴛs n/max"
    text-shadow: true           # Adds dark drop-shadow for contrast
```

### 3. Generation Physics & AFK Defense
```yaml
generation:
  drop-scatter: 0.0             # 0.0 = straight up; 1.0 = vanilla scatter
  show-drop-names: true         # Floating MiniMessage nameplate over drops
  owner-activity:
    enabled: true               # Skips ticks if owner is offline/distant
    max-distance-blocks: 64     # 4 chunk radius
```

### 4. Corruption Engine
```yaml
corruption:
  mode: HYBRID                  # CHANCE | DURABILITY | HYBRID
  chance: 0.01                  # 1% per-tick base corruption chance
  chance-at-max-level: -1       # -1 disables level scaling
  durability-max: 100
  damage-per-tick: 1
  cracked-material: COBBLESTONE
  repair:
    cooldown-seconds: 5
    cost-formula: "12.5 * tier"
```

### 5. Level Upgrades & Promotions
```yaml
upgrade:
  level:
    max: 10
    cost-formula: "500 * level^1.8"
  promotion:
    cost-formula: "10000 * tier"
```

### 6. Generator Placement Limits
```yaml
limits:
  default-max-per-player: 50
  additive-permission-prefix: "egens.addlimit."
  bypass-permission: "egens.limit.bypass"
  per-chunk: 8                  # Max generators per 16x16 chunk (-1 to disable)
  per-world:
    creative_world: 10
```

### 7. Automated Backups
```yaml
backup:
  auto-backup: true
  interval-hours: 6
  retention-count: 7            # Prunes oldest snapshots automatically
  directory: "backups"
```

---

## ⛓️ Unified Generator Files (`generators/<name>_generator.yml`)

Each generator has its own configuration file that houses both block settings and drop tables:

```yaml
generator:
  id: wood
  display-name: "<gradient:#c6884c:#ecc287><bold>Wood Generator</bold></gradient>"
  material: OAK_LOG
  base-capacity: 500
  base-durability: 75
  tick-interval: 2400
  max-level: 10
  next-tier: stone
  repair-cost: 1000
  repair-cost-per-level: 0.5
  shop-price: 2000
  lore:
    - "<#c6884c><bold><sc:Generator>"
    - "<#cfcfcf><sc:Hewn from the forest's heart.>"

drops:
  oak_log:
    item: OAK_LOG
    display-name: "<gradient:#92400e:#fde68a><bold><sc:Oak Timber></bold></gradient>"
    weight: 90
    min: 1
    max: 3
    price: 1

  stick:
    item: STICK
    display-name: "<gradient:#b45309:#d97706><bold><sc:Hardwood Stick></bold></gradient>"
    weight: 40
    min: 1
    max: 4
    price: 1
```

---

## 🌐 Localization (`lang/messages_*.yml`)

Every message displayed in chat, action bars, or boss bars can be customized with MiniMessage tags:

```yaml
prefix: "<gradient:#00F2FE:#4FACFE><bold>eGens</bold></gradient> <dark_gray>»</dark_gray> "
generator:
  placed: "<green>Successfully placed a <tier-display> generator!</green>"
  corrupted: "<red>Your <tier-display> generator has become corrupted!</red>"
  repaired: "<green>Repaired generator for <gold>${cost}</gold>!</green>"
sell:
  success: "<gray>Sold <white>{count}</white> items for <gold>${total}</gold>!</gray>"
```
