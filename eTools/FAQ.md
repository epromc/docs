---
description: Frequently asked questions about eTools licensing, usage, and support.
---

# FAQ

---

## Purchasing & Licensing

**How do I buy eTools?**
eTools is sold exclusively through the EproMC Discord server. Join the server and open a purchase ticket. You will receive a license key after completing the transaction.

**How many servers can I use one license on?**
One license covers up to two server instances:
- One **production server** (public-facing)
- One **development or test server** (must be on a private/local IP - not publicly accessible)

If you need eTools on a second public server, you will need to purchase an additional license.

**Can I share my license key with someone else?**
No. License keys are strictly personal and non-transferable. Sharing a key will result in immediate revocation without refund. See the [Terms of Service](Terms-of-Service.md) for details.

**My server IP changed. Can I rebind my license?**
Yes. Each license includes **5 rebind tokens** for its lifetime. One token is used per rebind request. Contact EproMC support in Discord to process a rebind. Once all 5 tokens are used, additional rebinds can be purchased separately.

**Do major version updates require a new purchase?**
Minor updates (bug fixes and features within the same major version) are included with your license at no extra cost. Major version upgrades (e.g., v1.x to v2.x) may require a new purchase. This will be announced in advance in the Discord server.

---

## Installation & Activation

**Where do I put my license key?**
Place your key in `plugins/eTools/license.yml` under the `key` field:

```yaml
license:
  key: "EPROMC-XXXX-XXXX-XXXX"
```

Save the file and restart your server.

**The plugin says my license is invalid. What's wrong?**
Common causes:
- The key was copied incorrectly - check for extra spaces or missing characters.
- The license is bound to a different IP and needs a rebind.
- The license was revoked due to a ToS violation.

Open a support ticket in Discord if none of those apply.

**The plugin shows "Invalid digital signature / MITM detected." What does that mean?**
This error appears when the response from the license server cannot be verified. Possible causes:
- A proxy or firewall is intercepting outbound HTTPS traffic.
- The server's system clock is significantly out of sync.

Check your firewall settings and system time, then restart the server.

**Does the plugin need an internet connection to work?**
Yes, on startup. eTools contacts the EproMC license server when the plugin loads. After successful validation, the plugin continues running normally even if the connection drops temporarily. A periodic heartbeat check runs in the background to maintain validation.

**Can I run eTools on a local test server while also running it on my public server?**
Yes, as long as the test server uses a private or local IP address (e.g., `localhost`, `192.168.x.x`). Both count within the same license. Public-facing servers each require their own license.

---

## Usage

**Does eTools support Folia?**
Yes. eTools natively uses Folia region schedulers for all area-breaking operations, tree felling, and utility item handling.

**Can players use area tools on player-placed blocks?**
By default, yes. Players can enable **Natural Only** mode via `/etools settings` to restrict area mining to naturally generated blocks. Admins can enforce this globally in `config.yml`.

**How does the lifespan system work?**
Each tool has a configurable expiry mode:
- `ONLINE_TIME` - counts down only while the player is connected.
- `REAL_TIME` - counts down in real-world time regardless of login status.
- `UNLIMITED` - the tool never expires.

Remaining time is stored per-item in the database and displayed in the item lore.

**What happens when a tool expires?**
Expired tools are removed from the player's inventory and any containers they are stored in. The plugin checks for expired items on startup and periodically during runtime.

**Can I create my own custom tools?**
Yes. All tools are defined in `plugins/eTools/tools.yml`. You can configure area dimensions (`width`, `height`, `depth`), lifespan, display name, lore, particles, sounds, enchantments, and more. See the [Custom Tools Guide](Custom-Tools-Guide.md) for the full reference.

---

## Refunds & Support

**Can I get a refund?**
No. Because eTools is an intangible digital software product delivered immediately upon payment with a unique license key, all sales are strictly final and non-refundable. Please review our documentation and feel free to ask questions in our Discord server before purchasing. See the [Terms of Service](Terms-of-Service.md) for full details.

**Where do I get support?**
All support is handled through the EproMC Discord server. Open a ticket and include your license information and any relevant error logs from your server console.

