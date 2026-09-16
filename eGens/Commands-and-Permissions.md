---
description: Complete command reference, aliases, usage arguments, and permission hierarchy for eGens.
---

# ⌨️ Commands & Permissions

All **eGens** functionality is managed through the root `/egens` command (with convenient aliases `/gens` and `/eg`), along with direct shorthand commands like `/sell`.

---

## 👤 Player Commands

| Command | Aliases | Description | Permission |
| :--- | :--- | :--- | :--- |
| `/egens help` | `/gens help`, `/eg help` | Displays the help menu listing available commands. | `egens.use` |
| `/egens shop` | `/gens shop` | Opens the graphical Generator Shop to purchase new tiers. | `egens.shop.use` |
| `/egens sell` | `/sell`, `/sell hand` | Sells eligible generator drops held in the player's main hand. | `egens.sell` |
| `/egens sellall` | `/sell all` | Sells all eligible generator drops from the player's inventory. | `egens.sell` |
| `/egens settings` | `/gens settings` | Opens the personal preferences GUI (Holograms, Sounds, BossBar). | `egens.use` |
| `/egens info` | `/gens info` | Displays tier, owner, level, and durability of the targeted generator. | `egens.use` |
| `/egens upgrade` | `/gens upgrade` | Upgrades the level or promotes the tier of the targeted generator. | `egens.use` |
| `/egens repair` | `/gens repair` | Repairs a corrupted generator within looking distance. | `egens.use` |

---

## 🛡️ Administrator Commands

Administrator commands allow operators and server scripts to distribute generators, sellwands, trigger multiplier events, and maintain database health.

| Command | Description | Permission |
| :--- | :--- | :--- |
| `/egens give <player> <tier> [amount]` | Gives generator placement items to the target player. | `egens.admin.give` |
| `/egens sellwand give <player> <wand_id> [amount]` | Grants custom sellwands defined in `sellwands.yml`. | `egens.admin.sellwand` |
| `/egens event give global <type> <seconds> [multiplier]` | Starts a server-wide multiplier event (e.g. `sell_multi 300 2.0`). | `egens.admin.event` |
| `/egens event give personal <player> <type> <seconds> [mult]` | Grants a personal multiplier event to a specific player. | `egens.admin.event` |
| `/egens backup` | Forces an immediate atomic database snapshot into `backups/`. | `egens.admin.backup` |
| `/egens perf` *(alias: `/egens profile`)* | Displays live in-process tick-time profiling metrics. | `egens.admin.perf` |
| `/egens perf reset` | Resets the accumulated profiling sample window. | `egens.admin.perf` |
| `/egens reload` | Hot-reloads `config.yml`, generator chains, GUIs, and language files. | `egens.admin.reload` |
| `/egens debug` | Toggles verbose diagnostic logging in server console. | `egens.admin.debug` |

---

## 🔑 Permissions Hierarchy

### 1. General & Player Permissions

```yaml
egens.use:
  default: true
  description: Base permission for using player-facing eGens features.

egens.shop:
  default: true
  description: Parent permission for the generator shop GUI.
  children:
    egens.shop.use: true

egens.sell:
  default: true
  description: Grants access to /sell, /egens sell, and /egens sellall.
```

### 2. Generator Limits & Bypasses

eGens features an **additive limit permission system**. Server admins can assign rank-based generator placement limits cleanly through LuckPerms or any permissions manager.

```yaml
egens.addlimit.<number>:
  description: Increases the player's generator placement cap by <number>.
  example: "A player with base cap 50 and egens.addlimit.20 can place 70 generators."

egens.limit.bypass:
  default: false
  description: Bypasses per-player, per-chunk, and per-world placement limits.

egens.world.bypass:
  default: false
  description: Bypasses world whitelist or blacklist restrictions for generator placement.

egens.personal.slots.<number>:
  description: Overrides personal concurrent event slots (up to max-cap 10).
```

### 3. Administrator Permissions

```yaml
egens.admin:
  default: op
  description: Grants all administrative capabilities.
  children:
    egens.admin.give: true
    egens.admin.sellwand: true
    egens.admin.event: true
    egens.admin.backup: true
    egens.admin.perf: true
    egens.admin.reload: true
    egens.admin.debug: true
    egens.admin.break: true        # Break any generator regardless of ownership
    egens.admin.bypass: true       # Bypass ownership verification
    egens.admin.open.others: true  # Open and inspect other players' generator menus
    egens.admin.update: true       # Receive update alerts upon joining
```
