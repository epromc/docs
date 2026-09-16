---
description: Step-by-step instructions for installing and setting up eHome on Paper, Purpur, or Folia.
---

# 📥 Installation & Setup

## 📌 System Requirements

* **Java Version:** Java 21 or higher (Compiled with modern Java 25 toolchain).
* **Server Software:**
  * **Paper** 1.21.x (Recommended)
  * **Purpur** 1.21.x
  * **Folia** 1.21.x (Native support with Region & Entity Schedulers)
  * **Spigot** 1.21.x

{% hint style="info" %}
**Folia Multi-Threading Compatibility:** eHome dynamically detects Folia regional threading on startup and switches its scheduler from Paper to `FoliaScheduler`. No manual configuration or command-line flags are required!
{% endhint %}

---

## 📥 Installation Steps

1. **Download the Plugin:**
   Download `eHome-0.0.1.jar` from your official release source or Modrinth.
2. **Place in Server:**
   Copy the JAR file into your server's `/plugins/` directory.
3. **Start the Server:**
   Launch your server (`java -jar paper.jar`). The plugin will automatically:
   * Bundle and initialize its shaded `HikariCP` connection pool.
   * Auto-resolve data folder paths (guaranteeing compatibility with Linux hosting & Pterodactyl container environments).
   * Generate default configuration files in `/plugins/eHome/`:
     * `config.yml`
     * `gui.yml`
     * `locales/en_US.yml`
     * `locales/id_ID.yml`
     * `ehome_data.db` (when using SQLite mode)
4. **Verification:**
   Check your server console. You will be greeted by the eHome startup banner:
   ```text
    ███████╗██╗  ██╗ ██████╗ ███╗   ███╗███████╗
    ██╔════╝██║  ██║██╔═══██╗████╗ ████║██╔════╝
    █████╗  ███████║██║   ██║██╔████╔██║█████╗  
    ██╔══╝  ██╔══██║██║   ██║██║╚██╔╝██║██╔══╝  
    ███████╗██║  ██║╚██████╔╝██║ ╚═╝ ██║███████╗
    ╚══════╝╚═╝  ╚═╝ ╚═════╝ ╚═╝     ╚═╝╚══════╝
   ```

---

## 🗄️ Database Setup (Multi-Storage Support)

Open `/plugins/eHome/config.yml` under the `storage:` section:

### Option 1: SQLite (Default - Recommended for Single Servers)
Requires zero external setup. All data is saved locally to `ehome_data.db`. Proactively resolves directory paths to eliminate Linux permission and case-sensitivity issues.
```yaml
storage:
  type: "SQLITE"
  sqlite:
    file: "ehome_data.db"
```

### Option 2: MySQL / MariaDB (Recommended for Multi-Server Networks)
Ideal for cross-server synchronization behind BungeeCord or Velocity proxies:
```yaml
storage:
  type: "MYSQL" # Or MARIADB
  remote:
    host: "127.0.0.1"
    port: 3306
    database: "ehome_db"
    username: "root"
    password: "your_password"
    ssl: false
    pool:
      maximum-pool-size: 10
      minimum-idle: 2
      connection-timeout: 10000
      max-lifetime: 1800000
```

### Option 3: PostgreSQL or H2
* **PostgreSQL:** Set `type: "POSTGRESQL"` and configure port `5432`.
* **H2 Database:** Set `type: "H2"` for high-performance file-based local storage.

---

## 🔌 Optional Integrations (Hooks)

eHome automatically discovers and integrates with your installed ecosystem:

* **Land Protection (Anti-Grief):**
  * **WorldGuard (v7.0+):** Enforces region permissions and flags before allowing `/sethome`.
  * **GriefPrevention:** Restricts `/sethome` to players' own claim areas.
  * **Lands:** Prevents creating homes inside foreign nations, lands, or areas without member trust.
* **Combat & Anti-PvP Logging:**
  * **CombatLogX & PvPManager:** Cancels active teleport warmup countdowns if a player is tagged in combat.
* **Economy (Vault):**
  * Charge configurable in-game currency fees for `/sethome` creation or `/home go` teleports.
* **Bedrock Support (Geyser & Floodgate):**
  * Automatically detects Bedrock players and presents native touch-friendly Cumulus dialogs instead of chest GUIs.
* **PlaceholderAPI:**
  * Exposes placeholders for custom scoreboards, tablists, and chats (`%ehome_total%`, `%ehome_max%`).

{% hint style="success" %}
All external integrations are soft-dependencies. If a hooked plugin is missing or uninstalled, eHome gracefully runs standalone without any errors.
{% endhint %}
