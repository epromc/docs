---
description: System requirements, automated library dependencies, soft-dependencies, and first-boot installation steps for eGens.
---

# 📥 Installation & Setup

Setting up **eGens** on your Minecraft server takes less than two minutes. The plugin utilizes Paper's modern runtime library loader to keep the binary lightweight while delivering enterprise-grade database and caching capabilities.

---

## 📋 System Requirements

| Requirement | Minimum / Recommended | Notes |
| :--- | :--- | :--- |
| **Java Version** | **Java 21+ or Java 25** | Required for modern virtual thread & record patterns. |
| **Server Software** | **Paper, Purpur, or Folia** | Supported versions: **1.20.4 – 1.21.x** & **26.1.2 – 26.2**. |
| **Multi-Threading** | Native **Folia** Support | Region schedulers handled seamlessly. |
| **Memory** | 2 GB+ RAM | Standard server RAM allocation. |

{% hint style="info" %}
**Lightweight Library Loader:**
eGens utilizes Paper's built-in library loader to automatically resolve runtime libraries (`HikariCP`, `Caffeine`, `sqlite-jdbc`, and `mysql-connector-j`) on initial server boot. Libraries are cached globally under `plugins/.paper/libraries/`, keeping the plugin `.jar` file under **1 MB**!
{% endhint %}

---

## 🧩 Compatibility & Soft-Dependencies

eGens runs out of the box with zero external dependencies using SQLite and native Paper TextDisplays. However, installing optional companion plugins unlocks richer functionality:

### 1. Economy & Value
* **Vault** *(Highly Recommended)*: Enables player economy transactions for generator upgrades, promotions, repairs, and the `/sell` and `/egens shop` systems.

### 2. Holographic Displays
The floating nameplate above generators dynamically switches between providers via `config.yml` (`generator.hologram.provider: AUTO`):
* **NATIVE (Built-in)**: Paper 1.20+ `TextDisplay` entities (high-performance, zero plugins required).
* **DecentHolograms**
* **FancyHolograms**
* **HolographicDisplays**

### 3. Claim & Territory Protections
Prevents unauthorized players from placing, corrupting, or breaking generators on protected land:
* **WorldGuard**
* **GriefPrevention**
* **Lands**
* **Towny**

### 4. Custom Items & Custom Heads
* **HeadDatabase (HDB)**: Use `hdb:<id>` in GUI configs and generator blocks.
* **ItemsAdder** & **Oraxen**: Integrate custom models, blocks, and furniture seamlessly into generator tiers.

### 5. Economy & Shop Hooks
* **ShopGUIPlus** & **EconomyShopGUI**: Synchronize drop pricing from existing shop configurations.
* **DeluxeSellwands**: Interoperable wand events and chest multipliers.

---

## 🛠️ Step-by-Step Installation

1. **Download the Latest Release:**
   Obtain `eGens-1.0.1.jar` from [Modrinth](https://modrinth.com/plugin/egens/version/1.0.1) or GitHub Releases.
2. **Place in Plugins Directory:**
   Copy the `.jar` file into your server's `plugins/` directory:
   ```text
   /your-server/
   └── plugins/
       ├── eGens-1.0.1.jar
       └── Vault.jar (optional)
   ```
3. **Start / Restart Server:**
   Start your server to allow eGens to extract default configurations and download cached libraries:
   ```bash
   [eGens] Loading eGens v1.0.1
   [eGens] [Storage] Initializing SQLite connection pool (HikariCP)...
   [eGens] [Generators] Loaded 28 generator configurations.
   [eGens] [Holograms] Attached display provider: NATIVE (TextDisplay).
   [eGens] Successfully enabled eGens v1.0.1!
   ```
4. **Configure Settings:**
   Customize `plugins/eGens/config.yml`, generator chains in `plugins/eGens/generators/`, and language files in `plugins/eGens/lang/`.
5. **Reload Configuration:**
   Apply modifications without server restarts using:
   ```text
   /egens reload
   ```
