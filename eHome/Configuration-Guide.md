---
description: Complete reference for configuring eHome settings, bed-themed matrix menus, and multi-language locales.
---

# ⚙️ Configuration Guide

All aspects of **eHome** can be fully customized across three modular configuration files located in `/plugins/eHome/`:

{% hint style="tip" %}
All configuration changes can be reloaded on-the-fly without restarting your server by executing `/ehome reload`.
{% endhint %}

---

## 1. `config.yml` (Core Settings & Integrations)

Controls storage engine choices, teleport warmup/cooldowns, visual and audio feedback, and third-party hooks:

```yaml
settings:
  default-locale: "en_US"

storage:
  # Supported: SQLITE, H2, MYSQL, MARIADB, POSTGRESQL
  type: "SQLITE"
  sqlite:
    file: "ehome_data.db"
  remote:
    host: "127.0.0.1"
    port: 3306
    database: "ehome_db"
    username: "root"
    password: "your_password"
    ssl: false

teleport:
  warmup-seconds: 5
  cancel-on-move: true
  move-threshold: 0.5
  cancel-on-damage: true
  cancel-in-combat: true
  cooldown-seconds: 30
  safe-teleport-check: true
  respawn-at-primary-home: true

visuals:
  warmup:
    bossbar:
      enabled: true
      color: "MULTI_COLOR" # Cycles colors or static: BLUE, GREEN, RED, etc.
      style: "PROGRESS"
    actionbar:
      enabled: true
    title:
      enabled: false
    particles:
      enabled: true
      type: "PORTAL"
      count: 25
    sound:
      enabled: true
      sound: "BLOCK_NOTE_BLOCK_HAT"

  success:
    bossbar:
      enabled: false
    actionbar:
      enabled: true
    title:
      enabled: true
    particles:
      enabled: true
      type: "REVERSE_PORTAL"
      count: 50
    sound:
      enabled: true
      sound: "ENTITY_PLAYER_TELEPORT"

homes:
  default-limit: 3
  allow-pinning: true
  invite-timeout-seconds: 60
  blacklisted-worlds:
    - "world_the_end"
    - "world_nether"

geyser:
  enabled: true
  use-native-bedrock-forms: true
  sanitize-custom-fonts-for-bedrock: true

integrations:
  vault:
    enabled: false
    costs:
      set-home: 100.0
      teleport: 25.0
  protection:
    check-worldguard: true
    check-griefprevention: true
    check-lands: true
  combat:
    hook-combatlogx: true
    hook-pvpmanager: true
```

---

## 2. `gui.yml` (GUI Matrix Layout & Bed Colors)

Defines the pattern-based chest GUI matrix and bed customization palette:

```yaml
menu:
  title: "<#4A90E2>✦ <white>ᴇʜᴏᴍᴇ <black>• <#A0AEC0>ʏᴏᴜʀ ʜᴏᴍᴇꜱ"
  rows: 4
  pattern:
    - "#########"
    - "#I#HHHHH#"
    - "#G#######"
    - "###P###N#"

items:
  "#":
    material: BLACK_STAINED_GLASS_PANE
    name: " "
  "I":
    type: PLAYER_INFO
    material: PLAYER_HEAD
    name: "<#4A90E2>✦ <white>{player} <gray>• <#CBD5E0>ᴘʀᴏꜰɪʟᴇ"
  "G":
    type: GUIDE_HELP
    material: BOOK
    name: "<#F6E05E>✦ <white>ᴇʜᴏᴍᴇ <gray>• <#ECC94B>ʜᴇʟᴘ & ɢᴜɪᴅᴇ"
    lore:
      - "<#BEE3F8>• ʟᴇꜰᴛ-ᴄʟɪᴄᴋ: <white>ᴛᴇʟᴇᴘᴏʀᴛ"
      - "<#FEB2B2>• ʀɪɢʜᴛ-ᴄʟɪᴄᴋ: <white>ᴄʜᴀɴɢᴇ ᴄᴏʟᴏʀ"
      - "<#BEE3F8>• ꜱʜɪꜰᴛ + ʟ-ᴄʟɪᴄᴋ: <white>ᴘɪɴ ꜰᴀᴠᴏʀɪᴛᴇ"
      - "<#FED7D7>• ꜱʜɪꜰᴛ + ʀ-ᴄʟɪᴄᴋ: <red>ᴅᴇʟᴇᴛᴇ ʜᴏᴍᴇ"
  "H":
    type: HOME_DYNAMIC_SLOT
    fallback-material: WHITE_BED
    name: "<#63B3ED>✦ <white>{home_name} {pinned_badge}"
  "P":
    type: PREVIOUS_PAGE
    material: ARROW
  "N":
    type: NEXT_PAGE
    material: ARROW

bed-picker:
  title: "<#4A90E2>✦ <white>ꜱᴇʟᴇᴄᴛ ʙᴇᴅ ᴄᴏʟᴏʀ <dark_gray>| <#63B3ED>{home_name}"
  rows: 4
  pattern:
    - "####I####"
    - "#BBBBBBB#"
    - "#BBBBBBB#"
    - "##B#<#B##"
```

---

## 3. `locales/` (Language & Typography Files)

eHome ships with bundled locales in `locales/en_US.yml` (English) and `locales/id_ID.yml` (Indonesian).

{% hint style="info" %}
**Adventure MiniMessage & Tags:**  
Supports rich gradients, hex colors, hover events, and clickable run commands.  
Use the tag `{no_prefix}` at the beginning of titles, bossbars, or actionbars to prevent prepending the chat prefix!
{% endhint %}

```yaml
prefix: "<#4A90E2>✦ <white>ᴇʜᴏᴍᴇ <dark_gray>» <gray>"

teleport:
  warmup: "<#ECC94B>ᴛᴇʟᴇᴘᴏʀᴛɪɴɢ ɪɴ <white>{seconds} <#ECC94B>ꜱᴇᴄᴏɴᴅꜱ... ᴅᴏ ɴᴏᴛ ᴍᴏᴠᴇ!"
  cancelled-movement: "<#F56565>ᴛᴇʟᴇᴘᴏʀᴛᴀᴛɪᴏɴ ᴄᴀɴᴄᴇʟʟᴇᴅ ᴅᴜᴇ ᴛᴏ ᴍᴏᴠᴇᴍᴇɴᴛ."
  bossbar-warmup: "{no_prefix}<#4A90E2>✦ <white>ᴛᴇʟᴇᴘᴏʀᴛɪɴɢ ᴛᴏ <#63B3ED>{home_name} <dark_gray>(<white>{remaining}s<dark_gray>)"

sharing:
  invite-usage: "<#F56565>ᴜꜱᴀɢᴇ: <white>/home share <player> <home>"
  invite-received: "<#63B3ED><white>{player} <#63B3ED>ɪɴᴠɪᴛᴇᴅ ʏᴏᴜ ᴛᴏ ᴛʜᴇɪʀ ʜᴏᴍᴇ <white>{home_name}<#63B3ED>!\n  <green><bold><click:run_command:'/home accept {player} {home_name}'><hover:show_text:'<green>ᴄʟɪᴄᴋ ᴛᴏ ᴀᴄᴄᴇᴘᴛ'>[ᴀᴄᴄᴇᴘᴛ]</hover></click></bold></green>   <red><bold><click:run_command:'/home deny {player} {home_name}'><hover:show_text:'<red>ᴄʟɪᴄᴋ ᴛᴏ ᴅᴇᴄʟɪɴᴇ'>[ᴅᴇᴄʟɪɴᴇ]</hover></click></bold></red>"
```
