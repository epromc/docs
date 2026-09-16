---
description: Guide to server-wide and personal multiplier events, automated event scheduling, additive stacking logic, and BossBar alerts.
---

# 🎉 Events & Multipliers

**eGens** features a dynamic event engine designed to drive player retention. Server operators can run automated or on-demand multiplier events that temporarily boost generation speeds, drop yields, or sell prices server-wide or for individual players.

---

## 🌟 Event Types

Configured in `plugins/eGens/events.yml`:

| Event Identifier | Effect | Stacking Calculation |
| :--- | :--- | :--- |
| `sell_multi` | Multiplies money earned from `/sell` and Sell Wands. | **Additive:** $1 + \sum(m_i - 1)$ |
| `drop_amount` | Generators spawn additional items per drop tick. | **Additive:** $1 + \sum(m_i - 1)$ |
| `drop_tier` | Temporarily promotes generator loot to the next tier up. | **Idempotent:** Any active event enables it |
| `speed_boost` | Reduces the tick interval between generation cycles. | **Max Multiplier:** Prevents thread overloads |
| `mixed_up` | Generators randomly roll loot from any unlocked tier. | **Idempotent:** Any active event enables it |

---

## ⏰ Automated Server Events

In `config.yml`, you can configure automatic event triggers on a set schedule:

```yaml
events:
  enabled: true
  auto-trigger:
    enabled: true
    interval-minutes: 60
    pool: [sell_multi, drop_amount, drop_tier, speed_boost, mixed_up]
```

Every 60 minutes, the plugin randomly draws an event from the pool, announces it server-wide via chat, plays a chime, and broadcasts a colored countdown **BossBar**.

---

## 🧮 Multiplier Stacking Rules

To keep the server economy balanced when running multiple events, eGens enforces **additive stacking**:

$$\text{Effective Multiplier} = 1 + \sum_{i} (\text{Multiplier}_i - 1)$$

> [!TIP]
> **Stacking Example:**
> If a global **$2\times$ Sell Event** and a personal **$3\times$ Sell Booster** are active simultaneously:
> $$\text{Effective} = 1 + (2 - 1) + (3 - 1) = \mathbf{4\times \text{ Sell Value}}$$
> *(Rather than compounding to $6\times$, preserving server economic balance).*

* **Global Stack Cap (`events.stack.max-global`):** Default `1`. Increase to `2–5` if you want admins to run simultaneous global events.
* **Speed Boost Clamping:** Speed boosts evaluate using `max(m1, m2)` to prevent excessive entity spawn rates on Folia region threads.

---

## 👤 Personal Events & Boosters

Players can be granted individual event boosters (e.g., from voting, rank crates, or store purchases) that run independently of global events.

### Starting Events via Command
```bash
# Global Event: 2x Sell Multiplier for 10 minutes (600s)
/egens event give global sell_multi 600 2.0

# Personal Event: 2x Drop Amount for Steve for 5 minutes (300s)
/egens event give personal Steve drop_amount 300 2.0
```

### Personal Slot Permissions
Each player has a concurrent personal event slot capacity:
* **Default:** `1` event at a time.
* **Rank Overrides:** Grant `egens.personal.slots.<number>` (e.g. `egens.personal.slots.3` allows 3 concurrent personal boosters).
* **Safety Bound:** Clamped by `max-cap: 10` in `config.yml`.
