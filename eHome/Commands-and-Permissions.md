---
description: Complete reference for all eHome player and administrative commands, sub-commands, aliases, and permissions.
---

# ⌨️ Commands & Permissions

## 📌 Player Commands

### 1. `/home`
* **Permission:** `ehome.use.home` (Default: All players)
* **Description:** The central hub command for all home interactions.
* **Usage & Sub-commands:**
  * `/home` (no arguments) — Opens your personal **Homes GUI**.
  * `/home go <name>` — Teleports to the specified home after a warmup countdown.
  * `/home set <name>` — Official alias for `/sethome <name>`.
  * `/home del <name>` or `/home delete <name>` — Official alias for `/delhome <name>`.
  * `/home pin <name>` — Toggles pinned favorite status for a home.
  * `/home rename <name> <new_name>` — Renames an existing home.
  * `/home share <player> <home>` — Invites a friend to share access to your home.
  * `/home accept <player> <home>` — Accepts an incoming shared home invitation.
  * `/home deny <player> <home>` — Declines an incoming shared home invitation.
  * `/home confirm` — Confirms updating the location of an existing home within 15 seconds.

{% hint style="info" %}
**Direct Name Safety:** Typing `/home <name>` directly will prompt a friendly reminder:  
`ᴜɴᴛᴜᴋ ᴛᴇʟᴇᴘᴏʀᴛ ᴋᴇ ʜᴏᴍᴇ ɪɴɪ, ɢᴜɴᴀᴋᴀɴ: /home go <namahome>`  
This prevents accidental teleportation while typing commands.
{% endhint %}

---

### 2. `/homes`
* **Permission:** `ehome.use.gui` or `ehome.use.home` (Default: All players)
* **Description:** Opens the interactive bed-themed Homes GUI directly.
* **Tab Completion:** Automatically suppressed to ensure a clean chat experience.

---

### 3. `/sethome [name]`
* **Permission:** `ehome.use.sethome` (Default: All players)
* **Description:** Creates a new home at your current player location.
* **Safety & Protections:**
  * **Safe Location Validation:** Blocks creation if the location is unsafe (lava, void, mid-air floating, suffocation).
  * **World Blacklist:** Rejects blacklisted dimensions specified in `config.yml`.
  * **Land Claim Verification:** Checks WorldGuard, GriefPrevention, and Lands regions.
  * **Accidental Overwrite Protection:** If a home with the same name exists, prompts you to run `/home confirm` within 15 seconds.

---

### 4. `/delhome <name>`
* **Permission:** `ehome.use.delhome` (Default: All players)
* **Description:** Removes an existing home from your account and detaches web map markers.
* **Tab Completion:** Automatically suggests your active homes.

---

## 🛡️ Administrative Commands (`/ehome`)

Access to administrative commands requires `ehome.admin` (Default: OP).

### 1. `/ehome reload`
* **Permission:** `ehome.admin.reload` or `ehome.admin`
* **Description:** Instantly reloads `config.yml`, `gui.yml`, and active language files in `locales/` without restarting the server.

### 2. `/ehome admin view <player>`
* **Permission:** `ehome.admin.view` or `ehome.admin`
* **Description:** Opens the targeted player's personal Homes GUI for real-time staff inspection.

### 3. `/ehome admin tp <player> <home>`
* **Permission:** `ehome.admin.tp` or `ehome.admin`
* **Description:** Directly teleports the administrator to the target player's home location (bypasses warmup and cooldowns).

### 4. `/ehome admin delete <player> <home>`
* **Permission:** `ehome.admin.delete` or `ehome.admin`
* **Description:** Force-deletes a specific home belonging to another player.

### 5. `/ehome admin purge [days]`
* **Permission:** `ehome.admin.purge` or `ehome.admin`
* **Description:** Purges all homes of players inactive for longer than the specified threshold (default: 60 days).

---

## 🔑 Permissions Reference

### Basic Player Permissions
| Permission Node | Default | Description |
| :--- | :---: | :--- |
| `ehome.use` | `true` | Parent permission allowing all basic player features. |
| `ehome.use.home` | `true` | Allows opening GUI and using `/home`. |
| `ehome.use.sethome` | `true` | Allows creating homes via `/sethome` or `/home set`. |
| `ehome.use.delhome` | `true` | Allows deleting homes via `/delhome` or `/home del`. |
| `ehome.use.gui` | `true` | Allows opening the Homes GUI via `/homes`. |
| `ehome.use.pin` | `true` | Allows pinning favorite homes to the top of the GUI. |
| `ehome.use.rename` | `true` | Allows renaming existing homes. |
| `ehome.use.share` | `true` | Allows sharing homes with friends via `/home share`. |
| `ehome.use.invite` | `true` | Legacy alias for `/home share` permission. |

### Quota Limit Permissions
| Permission Node | Default | Description |
| :--- | :---: | :--- |
| `ehome.limit.<number>` | `false` | Sets a custom home limit (e.g., `ehome.limit.5`, `ehome.limit.10`). |
| `ehome.limit.unlimited` | `op` | Grants unlimited home slots. |

### Bypass Permissions
| Permission Node | Default | Description |
| :--- | :---: | :--- |
| `ehome.bypass.cooldown` | `op` | Bypasses teleport cooldown timers. |
| `ehome.bypass.warmup` | `op` | Bypasses teleport warmup countdowns. |
| `ehome.bypass.combat` | `op` | Bypasses in-combat teleport cancellation. |
| `ehome.bypass.economy` | `op` | Bypasses Vault economy transaction fees. |

### Admin Permissions
| Permission Node | Default | Description |
| :--- | :---: | :--- |
| `ehome.admin` | `op` | Parent permission granting all administrative controls. |
| `ehome.admin.reload` | `op` | Access to `/ehome reload`. |
| `ehome.admin.view` | `op` | Access to `/ehome admin view <player>`. |
| `ehome.admin.tp` | `op` | Access to `/ehome admin tp <player> <home>`. |
| `ehome.admin.delete` | `op` | Access to `/ehome admin delete <player> <home>`. |
| `ehome.admin.purge` | `op` | Access to `/ehome admin purge [days]`. |
