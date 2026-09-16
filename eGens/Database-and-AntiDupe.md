---
description: High-performance HikariCP storage, automated backups, in-process tick profiler, Folia regional scheduling, and anti-dupe integrity.
---

# 🗄️ Database, Anti-Dupe & Performance

**eGens** is engineered from the ground up to withstand production Minecraft networks handling thousands of simultaneous generator blocks without causing tick lag or duplication exploits.

---

## 💾 Storage Backends (HikariCP)

All database operations execute asynchronously through an isolated I/O worker pool backed by **HikariCP**, ensuring zero main-thread or region-thread hitches.

### 1. SQLite (Default)
* **Zero Configuration:** Perfect for single-server setups.
* **Storage Path:** `plugins/eGens/egens.db`.
* **WAL Mode:** Operates in Write-Ahead Logging (WAL) mode for fast concurrent reads and writes.

### 2. MySQL & MariaDB
* **Network Ready:** Essential for high-concurrency environments, cross-server networks, or containerized Docker setups.
* **Prepared Statement Caching:** Pre-configured with optimal cache sizes (`cachePrepStmts: true`, `prepStmtCacheSize: 250`).
* **Connection Pooling:** Dynamic pool sizing (`pool-size: 10`) with automatic health checking and reconnect logic.

---

## 🛡️ Anti-Dupe Engine & Exploit Protections

Economy generators are frequent targets for duplication exploits. eGens implements strict preventative controls configured under `anti-dupe:` in `config.yml`:

| Protection Feature | Config Setting | Description |
| :--- | :--- | :--- |
| **Explosion Proofing** | `cancel-explosion: true` | TNT, Creepers, and Withers cannot destroy or pop generator blocks. |
| **Piston Immunity** | `cancel-piston: true` | Sticky and regular pistons are blocked from pushing or retracting generators. |
| **Fluid Protection** | `cancel-fluid-flow: true` | Flowing water or lava cannot wash away or break generators. |
| **PDC Identity Tracking** | Built-in | Every placed generator is tagged with a cryptographically unique `UUID` in its PersistentDataContainer (PDC). |
| **Anti-Abuse Drop Lock** | Built-in (v1.0.1) | Generator drops cannot be placed, crafted, brewed, smelted, fed, or used in anvils/workstations. |
| **Obstruction Protection** | Built-in (v1.0.1) | Blocks cannot be placed directly above generators, preventing hologram and drop clipping. |
| **Chunk Load Persistence** | Built-in (v1.0.1) | `GeneratorChunkListener` instantly re-attaches holograms and skins on chunk loads & late worlds. |
| **Concurrent Tick Locks** | Built-in | Per-generator reentrant locks prevent race conditions during simultaneous region ticks on Folia. |
| **Chunk Unload Flushes** | Built-in | Generator state is synchronously serialized to the database queue before chunks unload. |

---

## 🗃️ Automated Database Backup Service

eGens features an automated, non-blocking backup service that writes atomic snapshots to `plugins/eGens/backups/`.

* **SQLite Backups:** Executes `VACUUM INTO` against the live connection, producing a pristine snapshot without locking writers.
* **MySQL Backups:** Streams `mysqldump --single-transaction` into a compressed `.sql.gz` archive on the background I/O thread.
* **Retention Pruning:** Automatically purges the oldest snapshots once the count exceeds `backup.retention-count` (default: 7).
* **On-Demand Snapshots:** Run anytime without restarting:
  ```bash
  /egens backup
  ```

---

## ⏱️ In-Process Tick Profiler (`/egens perf`)

Monitor how much time eGens consumes per server tick directly in-game using the zero-overhead profiler.

```
[eGens] ─── Tick Profiler Digest ───
  • loot_dispatch:    0.042 ms avg (max: 0.180 ms) [12,400 samples]
  • hologram_update:  0.015 ms avg (max: 0.092 ms) [12,400 samples]
  • db_async_flush:   0.008 ms avg (max: 0.045 ms) [620 samples]
```

### Profiler Commands
* `/egens perf` *(or `/egens profile`)*: Displays the top-N hot paths sorted by total execution time.
* `/egens perf reset`: Resets sample counts to start a fresh measurement window.

---

## 🌿 Folia Regional Multi-Threading

eGens natively supports Paper's regional multi-threaded server software, **Folia**:

* **Region Schedulers:** Generator tick timers and item entity drops are scheduled on the specific region thread owning the generator's chunk.
* **Thread-Safe State:** All shared state is safeguarded by lock-free concurrent maps and atomic counters.
* **Zero Synchronous Cross-Thread Calls:** Prevents Folia thread deadlocks or main-thread stalls.
