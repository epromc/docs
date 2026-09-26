---
description: Frequently asked questions about eTools licensing, usage, and support.
---

# FAQ

---

## Purchasing & Licensing

**How do I buy eTools?**
eTools is sold exclusively through the EproMC Discord server. Join the server and open a purchase ticket in the appropriate channel. You will receive a license key after completing the transaction.

**What does one license cover?**
One license covers one server IP address. If you run multiple servers, you need a separate license for each one.

**Can I use one license on my test server and my production server at the same time?**
No. The license is bound to one IP at a time. You can request a rebind if you need to move the key to a different server, but you cannot run it on two IPs simultaneously.

**Can I transfer my license to someone else?**
No. Licenses are non-transferable. See the [Terms of Service](Terms-of-Service.md) for details.

**My server IP changed. What do I do?**
Contact EproMC support in Discord before or as soon as possible after the change. We will rebind the license to your new IP. One free rebind is included per license.

---

## Installation & Activation

**Where do I put my license key?**
Place your key in `plugins/eTools/license.yml` under the `key` field:

```yaml
license:
  key: "EPROMC-XXXX-XXXX-XXXX"
```

Restart the server after placing the key.

**The plugin says my license is invalid. What's wrong?**
Common causes:
- The key was typed or copied incorrectly. Make sure there are no extra spaces and the quotes are preserved.
- The license is already bound to a different IP.
- The license was revoked.

If none of those apply, open a support ticket in Discord.

**The plugin says "Invalid digital signature / MITM detected." What does that mean?**
This error means the license server response could not be verified. It usually happens when:
- A proxy or firewall is intercepting HTTPS traffic between your server and the license endpoint.
- The system clock on your server is significantly out of sync.

Check your server's outbound HTTPS access and system time, then restart.

**Do I need an internet connection for the plugin to work?**
Yes, on startup. eTools validates the license against the EproMC license server when the plugin loads. After validation, the plugin continues to run even if the connection drops temporarily. A periodic heartbeat check runs in the background.

---

## Usage

**Can I use eTools on a Folia server?**
Yes. eTools natively supports Folia region schedulers for all area-breaking operations, tree felling, and utility item handling.

**Can players mine player-placed blocks with area tools?**
By default, yes. However, players can enable **Natural Only** mode via `/etools settings`, which restricts area mining to naturally generated blocks only. Admins can also force this server-wide in the configuration.

**How does the lifespan system work?**
Each tool can have a configurable expiry:
- `ONLINE_TIME` — counts down only while the player is connected. Pauses when they log off.
- `REAL_TIME` — counts down in real-world time regardless of whether the player is online.
- `UNLIMITED` — the tool never expires.

Remaining time is shown in the item lore and saved to the database per-item.

**What happens to a player's tools when they expire?**
Expired tools are automatically removed from the player's inventory and any containers they are stored in. The plugin scans containers on startup and periodically during runtime.

**Can I create custom tool configurations?**
Yes. All tools are defined in `plugins/eTools/tools.yml`. You can change area sizes (`width`, `height`, `depth`), lifespan settings, display names, lore, particles, sounds, enchantments, and more. Refer to the [Custom Tools Guide](Custom-Tools-Guide.md) for the full configuration reference.

---

## Refunds & Support

**Can I get a refund?**
Refunds are available within 48 hours of purchase, provided the license has not been actively used on a live server more than once. See the [Terms of Service](Terms-of-Service.md) for the full refund policy.

**Where do I get support?**
All support is handled through the EproMC Discord server. Open a ticket and describe your issue with your license information and any relevant error logs.
