---
description: Official Terms of Service and End-User License Agreement for eTools.
---

# Terms of Service

Last updated: September 2026

This Terms of Service and End-User License Agreement ("Agreement") is a legal agreement between you ("Licensee", "Customer", or "You") and EproMC ("Licensor", "We", "Us", or "Our") governing your purchase, download, installation, and use of the **eTools** Minecraft server software and any associated documentation, updates, or license keys (collectively, the "Software").

By purchasing a license key, downloading, installing, or executing eTools on a server, you confirm that you have read, understood, and agreed to be bound by the terms outlined in this document. If you do not agree with these terms, do not purchase, install, or use the Software.

---

## 1. Definitions

To ensure complete clarity throughout this document, the following terms are defined:

- **"Software"**: The compiled eTools binary (`.jar`), default configuration files, language assets, and technical documentation provided by EproMC.
- **"License Key"**: The unique cryptographic identifier issued to you upon purchase, required to activate and operate the Software.
- **"Production Server"**: A live Minecraft server instance that is accessible to public players, bound to a public IP address or public domain.
- **"Development / Staging Server"**: A private, non-public server instance used strictly for testing, configuration, or staging purposes, operating exclusively on localhost (`127.0.0.1`) or private local network ranges (RFC 1918: `10.0.0.0/8`, `172.16.0.0/12`, or `192.168.0.0/16`).
- **"Rebind Token"**: A credit associated with your license that allows updating the authorized server IP address registered with our verification system.
- **"Grace Period"**: The temporary offline operational window (up to 48 hours) granted by the Software when communication with the authentication server is temporarily interrupted.

---

## 2. License Grant and Instance Allocation

### 2.1 Scope of License
Upon successful payment and issuance of a License Key, EproMC grants you a non-exclusive, non-transferable, non-sublicensable, and revocable commercial license to run the Software strictly in accordance with this Agreement.

### 2.2 Instance Allocation Limit
Each individual license purchase entitles you to operate the Software on a maximum of **two (2) server instances**:
1. **One (1) Production Server** (public-facing IP address).
2. **One (1) Development or Staging Server** (must reside on a private local IP or localhost).

### 2.3 Network and Proxy Architecture
In Minecraft server network architectures (such as BungeeCord, Waterfall, or Velocity):
- The Software runs as a backend Paper, Purpur, or Folia plugin.
- Each individual backend server instance that loads and executes eTools counts as an active instance against your license allocation.
- If your network runs eTools across multiple backend production servers (for example, separate Survival, Skyblock, and Mining servers), each production server requires its own separate license.

### 2.4 License Non-Transferability
Your License Key is strictly personal. You may not sell, resell, lease, lend, sublicense, assign, or transfer your license or License Key to any third party, individual, or server organization without prior written consent from EproMC.

---

## 3. License Validation and Technical Verification (DRM)

### 3.1 Digital Verification Mechanism
eTools incorporates an automated license validation mechanism to verify authentic ownership and protect against unauthorized distribution. When the server starts, the Software performs an outbound HTTPS handshake with the EproMC verification server.

### 3.2 Periodic Heartbeat
Following initial startup verification, the Software conducts a background heartbeat validation every 12 hours to maintain active license state.

### 3.3 Offline Grace Period
We recognize that temporary network outages, hosting maintenance, or upstream routing interruptions may occur:
- If the Software cannot reach the EproMC verification server during startup or scheduled heartbeat checks, it enters an **Offline Grace Period** of up to **48 hours**, using locally cached cryptographic validation tokens.
- During this 48-hour window, the Software continues to operate normally without interruption.
- If network connectivity is not restored after 48 consecutive hours, the Software will safely disable its custom features until connection with the verification service is re-established.

### 3.4 Protection Against Circumvention
You may not bypass, disable, tamper with, or circumvent the digital verification mechanism. Prohibited actions include, but are not limited to:
- Intercepting, redirecting, or modifying verification traffic via custom DNS, hosts file manipulation, or Man-in-the-Middle (MITM) proxies.
- Decompiling or patching bytecode to remove license validation checks.
- Spoofing server identifiers, hardware signatures, or authorization payloads.

Any detected circumvention attempt will result in immediate and permanent revocation of your license key without refund.

---

## 4. Permitted and Prohibited Uses

### 4.1 Permitted Uses
You are expressly permitted to:
- Install and operate the Software within the instance limits established in Section 2.
- Modify and customize all provided configuration files (`config.yml`, `tools.yml`, `messages.yml`, `license.yml`) to tailor the plugin to your server economy and gameplay.
- Create custom tool archetypes, dimensions, lifespans, sounds, and particle visualizers utilizing the built-in configuration framework.

### 4.2 Prohibited Uses
You may not, under any circumstances:
- Decompile, disassemble, reverse engineer, unpack, decrypt, or attempt to derive the source code of the Software binary.
- Distribute, publish, share, leak, or upload the Software JAR file or your License Key to any public or private file-sharing platforms, Discord servers, leak forums, or software repositories.
- Use the Software for competitive benchmarking, public reverse engineering tutorials, or creating derivative clone works.
- Permit third parties or unauthorized personnel access to your raw license credentials.

---

## 5. IP Rebinding and Token System

### 5.1 Rebind Token Allocation
Every eTools license comes with an allocation of **five (5) Rebind Tokens** valid for the lifetime of that license.

### 5.2 Token Usage
- When your server changes hosting providers, moves to a new dedicated server, or receives a new public IP address, one (1) Rebind Token is consumed to update your registered IP on the verification server.
- Rebind requests are processed via the official EproMC Discord support ticket system.
- Once processed, the previous IP binding is cleared and re-associated with your new server IP.

### 5.3 Token Depletion
- When all 5 rebind tokens have been exhausted, automatic rebind requests will no longer be available.
- Additional rebind tokens may be purchased separately or requested through an administrative review ticket in Discord.
- EproMC reserves the right to deny rebind requests if rapid, alternating IP changes suggest that a single license key is being shared among multiple parties.

---

## 6. Software Updates and Support

### 6.1 Minor Updates and Maintenance
Your license includes access to all **minor updates, maintenance patches, and bug fixes** within the same major version series (e.g., all v0.x releases, or updates within v1.x) at no additional charge. This includes compatibility patches for new minor Minecraft server builds (Paper, Purpur, Folia) during the active lifecycle of the product.

### 6.2 Major Version Upgrades
Major architectural overhauls, complete rewrites, or significant multi-version evolutions (e.g., advancing from v1.x to v2.x) may be designated as major releases and may require an upgrade fee. The availability, pricing, and terms of major upgrades will be announced in advance through official EproMC announcement channels.

### 6.3 Technical Support Scope
- Support is provided on a best-effort basis exclusively through the official EproMC Discord ticket system.
- Support covers bug reports, configuration questions, and plugin activation assistance.
- Support does not cover:
  - Third-party plugin conflicts or unsupported custom server cores.
  - Server lag caused by insufficient server hardware or improper general server optimization.
  - Custom Java bytecode modifications or decompiled environments.
  - Servers running offline/cracked configurations with broken authentication layers.

---

## 7. No Refund Policy (All Sales Final)

### 7.1 Strict No-Refund Policy
Due to the digital, non-returnable nature of the Software and the immediate delivery of digital License Keys and software binaries upon purchase, **all sales are strictly final**. EproMC does not offer, issue, or permit refunds, returns, or exchanges for any purchases under any circumstances.

### 7.2 Pre-Purchase Due Diligence
Before purchasing eTools, you are solely responsible for:
- Reviewing the official documentation, system requirements, and feature guides to ensure the Software meets your specific server requirements.
- Verifying server engine and Java compatibility (Paper, Purpur, or Folia on Java 21+).
- Asking any technical or compatibility questions in the official EproMC Discord pre-purchase channels.

By completing your purchase, you explicitly acknowledge and agree that you waive any statutory or general right of withdrawal or refund once the digital License Key has been issued.

### 7.3 Technical Assistance
Inability to configure, set up, or operate the Software does not qualify for a refund. If you encounter technical issues, unexpected errors, or configuration difficulties, our support team will provide technical assistance through the official Discord support ticket system to assist you in resolving the problem.

### 7.4 Chargebacks and Disputes
Initiating an unauthorized payment dispute, claim, or chargeback through your bank, credit card issuer, or payment processor without prior authorization constitutes fraudulent activity and a material breach of this Agreement. In the event of an unauthorized chargeback or payment reversal:
- Your License Key and all registered server IP addresses will be immediately and permanently blacklisted across the EproMC verification network.
- Your access to the EproMC Discord server, future product updates, and customer support will be terminated immediately.
- EproMC reserves the right to report disputed accounts and associated identifiers to anti-fraud networks and digital blacklist registries.

---

## 8. License Revocation and Termination

### 8.1 Grounds for Revocation
EproMC reserves the right to immediately, unilaterally, and permanently revoke your License Key without prior notice or refund if:
- You violate any provision of Section 2 (Instance Limits and Non-Transferability).
- You violate any provision of Section 3.4 (Circumvention of DRM) or Section 4.2 (Prohibited Uses).
- The Software binary or your License Key is detected on a leak platform, piracy network, or public forum.
- You initiate a payment dispute or chargeback.
- You engage in abusive, harassing, or threatening behavior toward EproMC staff or community members.

### 8.2 Effect of Termination
Upon revocation:
- Your license is terminated with immediate effect.
- The verification server will reject all future connection requests originating from your key or associated IPs.
- You must immediately delete all copies of the Software binary from all servers, storage devices, and backup systems in your possession.

---

## 9. Telemetry and Data Privacy

### 9.1 bStats Metric Collection
eTools utilizes [bStats](https://bstats.org) to collect anonymous, aggregated telemetry regarding plugin usage. This includes general platform information such as Java runtime version, Minecraft server version, server software brand (Paper, Purpur, Folia), and online player count.
- No player usernames, IP addresses, chat logs, or confidential server details are collected through bStats.
- You may disable bStats metrics at any time by setting `enabled: false` in `plugins/bStats/config.yml`.

### 9.2 License Authentication Data
During license verification, the Software transmits minimal operational data necessary to validate the key:
- The configured License Key.
- Outbound server IP address.
- An anonymized server instance identifier generated locally in `.server_id`.
- Plugin version and product name.

This data is stored securely and used solely for license verification, fraud prevention, and IP rebind auditing. We do not sell, rent, or trade your information with external advertising entities.

---

## 10. Disclaimer of Warranties and Limitation of Liability

### 10.1 "As-Is" Provision
The Software is provided on an "AS-IS" and "AS-AVAILABLE" basis, without warranty of any kind, whether express, implied, statutory, or otherwise. EproMC disclaims all implied warranties, including without limitation warranties of merchantability, fitness for a particular purpose, and non-infringement.

### 10.2 Limitation of Damages
In no event shall EproMC, its developers, contributors, or affiliates be liable for any direct, indirect, incidental, special, exemplary, punitive, or consequential damages (including, but not limited to, loss of server data, world file corruption, economic disruption, lost profits, business interruption, or hardware downtime) arising out of the use of or inability to use the Software, even if advised of the possibility of such damages.

### 10.3 Backup Obligation
You acknowledge that maintaining regular, comprehensive, and off-site backups of your Minecraft server worlds, player data, and configurations is exclusively your responsibility. EproMC is not responsible for data loss under any circumstances.

### 10.4 Liability Cap
To the maximum extent permitted by applicable law, EproMC's total aggregate liability for any and all claims arising under or related to this Agreement shall not exceed the actual purchase price paid by you for the eTools license.

---

## 11. Amendments to Terms

EproMC reserves the right to amend or update this Agreement at any time. Any revisions will be published on the official documentation portal and announced in the EproMC Discord server. 

Your continued use of the Software following the announcement of revisions constitutes your acknowledgment and acceptance of the updated terms. If you do not accept the updated terms, you must cease using the Software.

---

## 12. Contact and Support

For questions regarding these Terms of Service, license purchases, rebind requests, or technical support, contact us through our official Discord server:

- **Discord**: [discord.gg/sVWuc49eYV](https://discord.gg/sVWuc49eYV)
- **Support Channel**: Open a ticket in the designated support category.

