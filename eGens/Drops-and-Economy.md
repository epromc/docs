---
description: Comprehensive overview of eGens physical item drops, drop registry, direct selling, Sell Wands, and the Generator Shop.
---

# 💰 Drops, Economy & Sell Wands

**eGens** features an integrated economy loop. Generators drop physical items into the world, which players collect and convert into server currency through direct selling, automated chest Sell Wands, or external shop plugins.

---

## 📦 World-Drop Item Dispatch

Rather than trapping items inside a virtual inventory, eGens generators spawn physical item entities directly into the Minecraft world above the generator block.

```
       [ ✨ Dropped Item Entity ✨ ]
                     ↑
            [ 🟩 Generator Block ]
```

### Physics & Performance Controls
Configured in `config.yml` under the `generation:` section:

* **Drop Scatter (`drop-scatter`):**
  * `0.0` *(Default)*: Items pop straight up with zero horizontal velocity. Perfect for clean hopper or water stream collection systems.
  * `1.0`: Full vanilla item scatter velocity.
  * Values between `0.0` and `1.0` interpolate velocity smoothly.
* **Floating Drop Names (`show-drop-names`):**
  * When set to `true`, items floating on the ground display their custom MiniMessage formatted nameplate.
* **Owner Activity Radius Check (`owner-activity`):**
  * Prevents abandoned generator farms from consuming server tick budgets.
  * If the generator owner is offline or further than `max-distance-blocks` (default 64 blocks / 4 chunks), generation ticks and durability decay are skipped.

---

## 📜 Unified Drop Definitions (Within Each Generator YAML)

In **v1.0.1**, each generator's YAML file (`plugins/eGens/generators/<name>_generator.yml`) contains its own localized `drops:` section:

```yaml
drops:
  oak_log:
    item: OAK_LOG
    display-name: "<gradient:#92400e:#fde68a><bold><sc:Oak Timber></bold></gradient>"
    lore:
      - "<#9ca3af><sc:Freshly harvested forestry log.>"
      - "<#6b7280><sc:Sell Value:> <#9be7a7>$1"
    weight: 90
    min: 1
    max: 3
    price: 1

  stick:
    item: STICK
    display-name: "<gradient:#b45309:#d97706><bold><sc:Hardwood Stick></bold></gradient>"
    lore:
      - "<#9ca3af><sc:Whittled hardwood branch.>"
      - "<#6b7280><sc:Sell Value:> <#9be7a7>$1"
    weight: 40
    min: 1
    max: 4
    price: 1
```

* **Loot Weights & Quantities:** Set drop probabilities using `weight` along with `min` and `max` counts per drop roll.
* **Direct Value:** Each drop designates its direct `price` for `/sell` and Sell Wand calculations.

---

## 🔒 Strict Anti-Abuse Drop Lock (Zero Economy Exploits)

To prevent players from laundering generator drops into vanilla building materials or abusing mechanics:

{% hint style="danger" %}
**All eGens drops carry an internal `egens:drop_id` tag and are strictly restricted:**
* ❌ **No Block Placement:** Cannot be placed on the ground as blocks.
* ❌ **No Crafting:** Cannot be crafted in Crafting Tables or 2x2 player inventory grids.
* ❌ **No Brewing:** Cannot be placed in Brewing Stands.
* ❌ **No Smelting or Fuel:** Cannot be placed in Furnaces, Blast Furnaces, or Smokers.
* ❌ **No Anvil or Enchanting:** Cannot be combined in Anvils or enchanted in Enchanting Tables.
* ❌ **No Entity Feeding:** Cannot be fed to mobs or animals.
* ❌ **No Workstation Abuse:** Blocked from Grindstones, Smithing Tables, Stonecutters, and Composters.
* ✔️ **Allowed Uses:** Safe storage in Chests, Barrels, and Hoppers, and liquidation via `/sell` and Sell Wands!
{% endhint %}

---

## 💸 Direct Selling (`/sell` & `/sell all`)

Players can quickly liquidate their generator drops into currency via Vault:

| Command | Action |
| :--- | :--- |
| `/sell` or `/egens sell` | Sells only the generator drops currently held in the player's main hand. |
| `/sell all` or `/egens sellall` | Scans the player's entire inventory and sells all matching generator drops in a single transaction. |

Upon selling, players receive a formatted breakdown in chat:
```
[eGens] Sold 64x Iron Ingot and 32x Gold Ingot for $2,400.00!
```

---

## 🪄 Sell Wands (`sellwands.yml`)

Sell Wands are specialized items that allow players to sell the entire contents of a storage container with a single right-click.

### Features
* **Multipliers:** Apply bonus earnings on sold items (e.g. `1.2x`, `1.5x`, `2.0x`).
* **Durability:** Limit the number of container sales before the wand breaks, or set `durability: -1` for infinite uses.
* **Cooldown Protection:** Default 5-second cooldown per wand prevents player click-spamming.
* **Container Support:** Works on Chests, Trapped Chests, Double Chests, and Barrels.

### Example Configuration (`sellwands.yml`)
```yaml
wands:
  apprentice_wand:
    material: BLAZE_ROD
    display-name: "<gold><bold>Apprentice Sell Wand</bold></gold>"
    lore:
      - "<gray>Right-click a chest to sell all drops inside.</gray>"
      - "<yellow>Multiplier: <green>1.2x</green></yellow>"
      - "<aqua>Uses: <white>{uses}/{max_uses}</white></aqua>"
    multiplier: 1.2
    max-uses: 100
    glow: true

  master_wand:
    material: NETHER_STAR
    display-name: "<light_purple><bold>Master Sell Wand</bold></light_purple>"
    multiplier: 2.0
    max-uses: -1 # Infinite
    glow: true
```

### Giving Sell Wands
```bash
/egens sellwand give <player> <wand_id> [amount]
```

---

## 🛒 Generator Shop (`/egens shop`)

Players can browse and purchase generators directly through a multi-page graphical shop.

* **Categorized Menus:** Browse generator chains (`Vanilla`, `Mob`, `Elemental`).
* **Vault Transaction Support:** Automatically verifies player balance and inventory space before deducting funds and dispensing generator blocks.
* **Permission Locks:** Restrict advanced chains to specific ranks or player milestones.
