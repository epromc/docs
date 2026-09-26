---
description: Step-by-step instructions for installing and setting up eTools on Paper, Purpur, or Folia.
---

# Installation & Setup

## System Requirements

| Requirement | Supported / Recommended | Notes |
| :--- | :--- | :--- |
| **Java Version** | **Java 21+ or Java 25** | Required for modern virtual threads and record patterns. Compiled on Java 21 LTS with full forward-compatibility for Java 25 runtimes. |
| **Server Software** | **Paper, Purpur, or Folia** | Supported versions: **1.21.x** and **26.1.2 - 26.2**. |
| **Multi-Threading** | Native **Folia** Multi-Threading | Region and entity schedulers handled seamlessly with zero manual flags or extra configuration required. |
| **Memory** | 2 GB+ RAM | Standard server RAM allocation for dedicated environments. |

{% hint style="info" %}
**Folia Compatibility:** eTools automatically detects Folia and hooks into regionized multithreading. No manual flags or configurations are required.
{% endhint %}

---

## License Activation

eTools uses a commercial license system. A valid license key is required to run the plugin.

### Step 1: Obtain a License Key
Purchase an eTools license through the official **EproMC Discord server** to receive your personal license key.

### Step 2: Configure `license.yml`
Upon first launch (before a license is configured), the plugin generates a `license.yml` file inside `/plugins/eTools/`:

```yaml
license:
  # Enter the license key received from EproMC
  key: "YOUR-LICENSE-KEY-HERE"
```

Replace `YOUR-LICENSE-KEY-HERE` with your actual key, retaining the double quotation marks.

### Step 3: Restart the Server
Restart your server after placing the key. Once verified, the startup console confirms activation:

```text
[eTools] ========================================================
[eTools]   eTools Premium License Verified!
[eTools]   Licensed to: YourName
[eTools] ========================================================
```

{% hint style="warning" %}
**IP Binding:** Your license key is bound to your server IP address (covering 1 production server and 1 private local development server). If you migrate hosting providers or servers, contact support via Discord to process an IP rebind using your allocated rebind tokens.
{% endhint %}

{% hint style="danger" %}
**License Security:** Do not share or publish your license key. Each key is tied to a specific buyer. Unauthorized redistribution, sharing, or tampering will result in immediate and permanent key revocation.
{% endhint %}

---

## Installation Steps

1. **Download the Plugin:**
   Download `eTools-0.0.1-RELEASE.jar` from your dedicated purchase ticket in the EproMC Discord server.
2. **Place in Server Directory:**
   Copy the JAR file into your server's `plugins/` directory:
   ```text
   /your-server/
   |-- plugins/
       |-- eTools-0.0.1-RELEASE.jar
       |-- WorldGuard.jar (optional)
   ```
3. **Start the Server (First Launch):**
   Start your server. The plugin will:
   * Generate `license.yml` in `plugins/eTools/`.
   * Display a license configuration notice in the console.
4. **Configure License:**
   Enter your license key into `plugins/eTools/license.yml` as described in the License Activation section.
5. **Restart the Server:**
   After configuring your key, restart the server. Upon successful verification:
   * Runtime dependencies (`HikariCP` and `sqlite-jdbc`) are loaded automatically.
   * Default configuration files are generated in `plugins/eTools/`:
     * `config.yml`
     * `messages.yml`
     * `tools.yml`
     * `database.db` (when using SQLite mode)
6. **Console Verification:**
   Verify successful initialization in your server console:
   ```text
    ______     ______   ______     ______     __         ______    
   /\  ___\   /\__  _\ /\  __ \   /\  __ \   /\ \       /\  ___\   
   \ \  __\   \/_/\ \/ \ \ \/\ \  \ \ \/\ \  \ \ \____  \ \___  \  
    \ \_____\    \ \_\  \ \_____\  \ \_____\  \ \_____\  \/\_____\ 
     \/_____/     \/_/   \/_____/   \/_____/   \/_____/   \/_____/ 
      by epromite & epromc - v0.0.1-RELEASE
   ```

---

## Database Setup (SQLite vs. MySQL)

Open `plugins/eTools/config.yml`:

### Option 1: SQLite (Default - Recommended for Single Servers)
Requires zero external setup. All data is saved locally to `database.db`.
```yaml
database:
  type: SQLITE
  sqlite:
    file: "database.db"
```

### Option 2: MySQL / MariaDB (Recommended for Networks and Proxies)
For multi-server networks (BungeeCord or Velocity) synchronizing tool ownership across instances:
```yaml
database:
  type: MYSQL
  mysql:
    host: "localhost"
    port: 3306
    database: "etools"
    username: "your_username"
    password: "your_password"
    ssl: false
  pool:
    maximum-pool-size: 10
    minimum-idle: 5
    maximum-lifetime: 1800000
    connection-timeout: 5000
```

---

## Optional Integrations (Hooks)

eTools automatically detects and integrates with the following companion plugins:

* **WorldGuard (v7.0+):**
  Prevents area tools (drills, shovels, feller axes) from modifying blocks inside protected regions without appropriate build or break permissions (`canBreak` flag).
* **GriefPrevention:**
  Respects claim boundaries. Unauthorized players cannot mine, dig, or harvest within another player's claimed territory.
* **CoreProtect:**
  Inspects historical player block-placement logs to enforce the **Natural Blocks Only** protection mode (`/etools settings`).

{% hint style="success" %}
All hooks operate as soft-dependencies. If these plugins are not present, eTools functions standalone with zero issues.
{% endhint %}