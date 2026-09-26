---
description: Complete reference for configuring eTools settings, messages, and custom tool archetypes.
---

# Configuration Guide

All aspects of **eTools** can be easily customized across three primary configuration files located in `/plugins/eTools/`:

{% hint style="tip" %}
All configuration changes can be reloaded on-the-fly without restarting your server by running `/etools reload`.
{% endhint %}

---

## 1. `config.yml` (Server-Wide Settings)

Controls core performance thresholds, scheduler frequencies, database connections, and audio-visual cues:

```yaml
settings:
  # How often (in seconds) the timer task checks online players' active items
  timer-interval-seconds: 1

  # Enable instant expiration checks when players open containers (Chests, Barrels, Shulkers, etc.)
  container-validation: true

  # Merge nearby drop items to prevent entity lag when breaking large areas
  batch-drops: true

  # Max log blocks an axe can fell in a single swing (prevents freezing on massive trees)
  max-tree-feller-blocks: 500

  # Lifespan warning thresholds (in seconds) that trigger sound and action bar alerts
  # 300 = 5 minutes, 60 = 1 minute
  alert-thresholds:
    - 300
    - 60

# Region & Claim Protection Integrations
hooks:
  worldguard: true
  griefprevention: true

# Database Configuration (SQLite for local file, MySQL/MariaDB for remote network)
database:
  type: SQLITE # Options: SQLITE or MYSQL
  sqlite:
    file: "database.db"

# Sound effects for lifespan alerts & destruction
sounds:
  alert:
    name: "BLOCK_NOTE_BLOCK_PLING"
    volume: 1.0
    pitch: 1.8
  expired:
    name: "BLOCK_AMETHYST_CLUSTER_BREAK"
    volume: 1.2
    pitch: 0.9
```

---

## 2. `messages.yml` (Localization & Styling)

Every message, prefix, alert, and notification can be tailored to match your server's theme.

{% hint style="info" %}
**Formatting Engines:** Full support for modern **Adventure MiniMessage** tags (e.g. `<gradient:#HEX1:#HEX2>`, `<#HEX>`, `<hover>`, `<click>`) and legacy color codes (`&a`, `&b`, etc.).
{% endhint %}

```yaml
prefix: "<gradient:#B983FF:#7F00FF><b>eTools</b></gradient> <dark_gray>»</dark_gray> "

messages:
  no-permission: "<red>You do not have permission to execute this command.</red>"
  player-not-found: "<red>Player <gold>{player}</gold> was not found online.</red>"
  tool-given-sender: "<gray>You gave <gold>{amount}x</gold> <yellow>{tool}</yellow> to <aqua>{player}</aqua> <dark_gray>(</dark_gray><gray>Lifespan: <light_purple>{duration}</light_purple></gray><dark_gray>)</dark_gray></gray>"
  tool-given-receiver: "<gray>You received <gold>{amount}x</gold> <yellow>{tool}</yellow>! <dark_gray>(</dark_gray><gray>Lifespan: <light_purple>{duration}</light_purple></gray><dark_gray>)</dark_gray></gray>"
  # ... (all in-game messages are fully customizable)
```

---

## 3. `tools.yml` (Custom Tool Creation)

You have total freedom over custom tools. You are never limited to default templates - create any custom tool archetype with unique models, sounds, particles, and enchantments.

### Dimension Flexibility:
Area tools (drills, shovels, hoes, shears) support flexible dimension configurations:
- `radius: 3` - Standard 3x3 square area (depth 1)
- `radius: "3x3x3"` - Full 3D cube (3 wide, 3 high, 3 blocks deep into wall/floor)
- `radius: "3, 3, 1"` - Comma-separated (width, height, depth)
- `radius: "3x2"` - Custom dimensions (3 wide, 2 high)

### Configuration Specification:

```yaml
tools:
  amethyst_drill:
    # Tool archetype: DRILL, SHOVEL, AXE, HOE, SHEARS, INFINITE_PEARL, INFINITE_ROCKET,
    # INFINITE_BUCKET, INFINITE_GOLDEN_APPLE, INFINITE_STEAK
    type: DRILL

    # Base Minecraft item material
    base-item: NETHERITE_PICKAXE

    # Custom Model Data for custom resource pack models / textures (optional)
    custom-model-data: 10001

    # Display name with MiniMessage gradient support
    display-name: "<gradient:#B983FF:#7F00FF><b>Amethyst Drill</b></gradient>"

    # Custom lore lines (<time_remaining> placeholder automatically updates)
    lore:
      - "<dark_gray>----------------</dark_gray>"
      - "<gray>Mines a <#B983FF>3x3</#B983FF> area instantly in the"
      - "<gray>direction you are looking."
      - ""
      - "<dark_gray>»</dark_gray> <gray>Type:</gray> <#B983FF>Directional Drill</#B983FF>"
      - "<dark_gray>»</dark_gray> <gray>Radius:</gray> <#B983FF>3x3 blocks</#B983FF>"
      - "<dark_gray>»</dark_gray> <gray>Lifespan:</gray> <#B983FF><time_remaining></#B983FF>"
      - "<dark_gray>----------------</dark_gray>"

    # Mining / digging dimensions (supports 3, "3x3", "3x3x3", "3x2", etc.)
    radius: "3x3x3"

    # Lifespan rules
    lifespan:
      mode: "ONLINE_TIME" # ONLINE_TIME, REAL_TIME, or UNLIMITED
      default-duration: "4h" # Default granted lifespan (e.g., 30m, 1h, 4h, 7d, permanent)

    # Item flags & safeguards
    unbreakable: true # Prevents vanilla durability depletion
    keep-on-death: true # Retained in inventory upon player death
    prevent-anvil: true # Disallows renaming or repair exploits in anvils
    prevent-grindstone: true # Disallows stripping enchantments or XP farming
    glow: true # Displays enchantment shimmer

    # Aesthetic visual particle effects
    particle:
      enabled: true
      type: "DUST"
      color: "#B983FF"
      size: 1.0
      count: 12
      speed: 0.05

    # Aesthetic sound feedback on use
    sound:
      enabled: true
      name: "BLOCK_AMETHYST_BLOCK_CHIME"
      volume: 1.0
      pitch: 1.5

    # Custom enchantments and flags
    enchantments:
      - "EFFICIENCY:6"
      - "FORTUNE:3"
    hide-enchantments: true
    hide-attributes: true
```