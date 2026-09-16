---
description: Technical architecture of eHome database connection pools, Linux hosting path resolution, and safe teleportation mechanics.
---

# 🗄️ Database & Storage Architecture

eHome is backed by an asynchronous database engine powered by **HikariCP**, engineered to manage tens of thousands of homes across high-population servers with zero main-thread hitching.

---

## ⚡ HikariCP Connection Pooling

eHome shades **HikariCP 6.2.0** to provide rapid, fail-safe connection handling:
* **Connection Timeout:** Enforces a 5-second fail-fast timeout to prevent blocking server threads during connection drops.
* **Leak Detection:** Built-in connection lifecycle monitors prevent memory and pool leaks.
* **Non-Blocking Async DAOs:** All database operations run asynchronously using `CompletableFuture` dispatched via the platform's scheduler.

---

## 🐧 Linux Hosting & Container Self-Healing

On cloud hosting environments (such as Pterodactyl, Docker containers, and Linux VPS), standard SQLite drivers can fail with `path to database does not exist` if directories have case-sensitivity differences or parent directories do not exist prior to pool connection.

eHome incorporates an intelligent **Self-Healing Path Resolver**:
1. Inspects `/plugins/` to locate the exact plugin folder (case-insensitively).
2. Recursively ensures parent directories are created using modern NIO (`Files.createDirectories`).
3. Explicitly initializes the database file (`createNewFile()`) before HikariCP touches the disk.
4. Guarantees 100% plug-and-play operation across any cloud host without manual permission fixes.

---

## 📊 Database Schema & Automatic Migrations

Upon startup, eHome's built-in migrator automatically deploys schema definitions:

### 1. `eh_homes` Table
Stores all player home coordinates, world dimensions, and customization states:
* `player_uuid` (VARCHAR 36) — Unique identifier of the home owner.
* `name` (VARCHAR 32) — Normalized home name.
* `world` (VARCHAR 64) — World identifier.
* `x`, `y`, `z` (DOUBLE) — Exact coordinate locations.
* `yaw`, `pitch` (FLOAT) — Player view angle orientation.
* `bed_icon` (VARCHAR 32) — Selected bed color material name (default: `WHITE_BED`).
* `is_pinned` (BOOLEAN) — Pinned favorite priority flag.
* `created_at`, `updated_at` (BIGINT) — Unix epoch timestamps for activity tracking and purge calculations.

### 2. `eh_pending_invites` Table
Tracks active invitations for the `/home share` system:
* `target_uuid` (VARCHAR 36) — Invited player's UUID.
* `sender_uuid` (VARCHAR 36) — Inviting host's UUID.
* `home_name` (VARCHAR 32) — Target home name.
* `expires_at` (BIGINT) — Auto-expiration timestamp (default: 60 seconds).

---

## 🛡️ Safe Teleportation Scanner

To protect player equipment and hardcore gameplay, eHome executes a rigorous safety scan before initiating teleports:

1. **Suffocation Checks:** The destination feet and head blocks must not be solid, suffocating blocks.
2. **Hazard Detection:** Destination and surrounding blocks cannot be lava, fire, campfire, sweet berry bushes, or wither roses.
3. **Void & Liquid Checks:** Teleportation into open void or hazardous liquids is automatically aborted.
4. **Adaptive Bed Placement:** If the location is safe, the player spawns centered facing their saved yaw and pitch.
