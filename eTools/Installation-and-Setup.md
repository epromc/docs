---
description: Step-by-step instructions for installing and setting up eTools on Paper, Purpur, or Folia.
---

# 📥 Installation & Setup

## 🖥️ System Requirements

* **Java Version:** Java 21 or higher.
* **Server Software:**
  * **Paper** 1.21.x (Recommended)
  * **Purpur** 1.21.x
  * **Folia** 1.21.x (Native support with Region & Entity Schedulers)
  * **Spigot** 1.21.x

{% hint style="info" %}
**Folia Compatibility:** eTools automatically detects Folia and hooks into regionized multithreading. No manual flags or configurations are required!
{% endhint %}

---

## 🔑 License Activation

eTools uses a **premium license system**. A valid license key is required to run the plugin.

### Step 1: Obtain a License Key
Purchase eTools via our **Discord community server** to receive your personal license key.

### Step 2: Create `license.yml`
Upon first launch (before any license is configured), the plugin will generate a `license.yml` file inside `/plugins/eTools/`:

```yaml
license:
  # Enter the license key you received upon purchasing eTools from EproMC
  key: "YOUR-LICENSE-KEY-HERE"
```

Replace `YOUR-LICENSE-KEY-HERE` with your actual key. Make sure to keep the **double quotes** — they are required.

### Step 3: Restart or Reload
Restart your server after placing the key. If the license is valid, the startup banner will confirm:

```text
[eTools] ========================================================
[eTools]   eTools Premium License Verified!
[eTools]   Licensed to: YourName
[eTools] ========================================================
```

{% hint style="warning" %}
**IP Binding:** Your license key is bound to your server's IP address. If you migrate servers, contact us via Discord to reset your IP binding.
{% endhint %}

{% hint style="danger" %}
**License Security:** Do not share your license key. Each key is tied to a specific buyer and limited to a set number of server IPs. Unauthorized sharing will result in key revocation.
{% endhint %}

---

## 📦 Installation Steps

1. **Download the Plugin:**
   Download `eTools-0.0.1-RELEASE.jar` from the purchase channel in our Discord after completing your purchase.
2. **Place in Server:**
   Copy the JAR file into your server's `/plugins/` directory.
3. **Start the Server (First Launch):**
   Launch your server. The plugin will:
   * Generate `license.yml` in `/plugins/eTools/`.
   * Display a license prompt in the console.
4. **Configure License:**
   Enter your license key into `license.yml` as described above.
5. **Restart the Server:**
   After placing your key, restart the server. On successful verification:
   * Runtime dependencies (`HikariCP` and `sqlite-jdbc`) are downloaded automatically.
   * Default configuration files are generated in `/plugins/eTools/`:
     * `config.yml`
     * `messages.yml`
     * `tools.yml`
     * `database.db` (when using SQLite mode)
6. **Verification:**
   Check your server console for the eTools startup banner:
   ```text
    ______     ______   ______     ______     __         ______    
   /\  ___\   /\__  _\ /\  __ \   /\  __ \   /\ \       /\  ___\   
   \ \  __\   \/_/\ \/ \ \ \/\ \  \ \ \/\ \  \ \ \____  \ \___  \  
    \ \_____\    \ \_\  \ \_____\  \ \_____\  \ \_____\  \/\_____\ 
     \/_____/     \/_/   \/_____/   \/_____/   \/_____/   \/_____/ 
      by epromite & epromc — v0.0.1-RELEASE
   ```

---

## 🗄️ Database Setup (SQLite vs. MySQL)

Open `/plugins/eTools/config.yml`:

### Option 1: SQLite (Default - Recommended for Single Servers)
Requires zero external setup. All data is saved locally to `database.db`.
```yaml
database:
  type: SQLITE
  sqlite:
    file: "database.db"
```

### Option 2: MySQL / MariaDB (Recommended for Networks / Proxies)
If you operate a multi-server network (BungeeCord / Velocity) and wish to synchronize tool ownership and usage across instances:
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

## 🔗 Optional Integrations (Hooks)

eTools automatically detects and hooks into the following plugins:

* **WorldGuard (v7.0+):**
  Prevents area tools (3x3 / 5x5) from breaking blocks inside protected regions without break permissions (`canBreak` flag).
* **GriefPrevention:**
  Respects player land claims. Unauthorized players cannot mine, dig, or till within another player's claim.
* **CoreProtect:**
  Examines historical player block-placement logs to enhance the **Natural Blocks Only** protection mode (`/etools settings`).

{% hint style="success" %}
All hooks are soft-dependencies. If these plugins are not installed, eTools will run standalone without any issues.
{% endhint %}
