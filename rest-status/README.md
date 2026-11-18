# REST / JSON Status Widgets Guide

REST / JSON Status Widgets poll HTTP/HTTPS endpoints (`GET` or `HEAD`), extract values from JSON responses using dot/bracket paths, evaluate health rules (`ok` / `warn` / `err`), and display live status badges—optionally with extra metrics and encrypted authentication headers.

Open **Settings → Custom Widgets** and click **+ Add REST Status** to create one. Once created, place and order it in **Settings → Appearance → Widgets**.

---

## 1. Core Configuration

- **Name & Icon**: Widget label and optional emoji or custom icon (`https://...` URL or uploaded image).
- **Endpoint URL** (`endpointUrl`): `http://` or `https://` URL to poll.
- **Method** (`method`): `GET` (parses JSON body) or `HEAD` (checks HTTP reachability/status).
- **JSON Path** (`jsonPath`): Dot/bracket path into the JSON response (e.g., `status.indicator`, `data.active_queries`, `services[0].state`, `metrics['cpu.load']`).
- **Value Mapping** (`valueMap`): Comma-separated `raw=Display` replacements (case-insensitive key lookup), e.g.:
  ```text
  none=OK, minor=Minor, major=Major, critical=Critical
  ```
- **Value Suffix** (`valueSuffix`): Optional unit/suffix appended to the displayed value (e.g., `%`, `GB`, `d`).
- **Refresh Interval** (`refreshSeconds`): Polling interval in seconds (clamped between `10` and `3600`, default `60`).
- **Link URL** (`linkUrl`): Optional URL opened when clicking the status badge.

---

## 2. Status Rule Matching (`okMatch` & `warnMatch`)

Rules are comma-separated conditions evaluated in order (any matching part triggers the rule). `warnMatch` is checked first; if it does not match and `okMatch` is set, matching `okMatch` produces `ok` and failing it produces `err`.

Supported rule syntax:
- **Exact string** (case-insensitive): `none`, `operational`, `enabled`
- **Substring match** (`~`): `~pve`, `~ok`
- **Numeric / equality operators**: `>=`, `<=`, `>`, `<`, `=`, `!=` (e.g., `<90`, `>=90`, `!=0`)

---

## 3. Extra Metrics, Scaling & Grouping

- **Extra Metrics** (`metrics`, up to **6** per widget): Evaluate additional `jsonPath` values from the same HTTP response. Each metric supports:
  - `label` (up to 24 chars)
  - `jsonPath`
  - `scale` (optional positive multiplier, rounded to 2 decimal places—for example, `100` to turn `0.42` into `42%`, or `9.313225746154785e-10` to convert bytes to GiB)
  - `valueSuffix`, `valueMap`, `okMatch`, `warnMatch`
- **Hide Primary Value** (`hideValue`): Hide the top-level value when you only want to show the status indicator and extra metrics.
- **Collapse Metrics** (`collapseMetrics`): Keep extra metrics collapsed behind a toggle to save space.
- **Grouping** (`groupName`, `hideGroupName`): Widgets sharing the same `groupName` render together in a single grouped card (see [`proxmox-node-stats.json`](./proxmox-node-stats.json)).

---

## 4. Authenticated Endpoints & Secrets Vault

For private/homelab APIs (such as Proxmox, Home Assistant, or Pi-hole):
- Set **Auth Header Name** (`authHeaderName`, e.g., `Authorization`) and **Auth Header Value** (`authHeaderValue`, e.g., `Bearer YOUR_TOKEN` or `PVEAPIToken=...`).
- If the **Secrets Vault** is enabled in Settings, `authHeaderValue` is encrypted at rest (`AES-GCM` with a RAM-only session key).
- When the Vault is locked, the widget displays a `🔐` badge—click the badge to unlock the Vault in place and resume polling.

> **Note:** Browser extensions can only fetch origins permitted by your browser/extension host permissions and network reachability (local/LAN HTTPS endpoints with self-signed certificates must be trusted by your browser).

---

## 5. Examples in This Folder

Import any `.json` file in this folder via **Settings → Custom Widgets → 📤 Import**:

**Public Service Statuses:**
- [`github-status.json`](./github-status.json) — GitHub Status API (`www.githubstatus.com`)
- [`cloudflare-status.json`](./cloudflare-status.json) — Cloudflare Status API
- [`discord-status.json`](./discord-status.json) — Discord Status API
- [`npm-status.json`](./npm-status.json) — npm Status API
- [`reddit-status.json`](./reddit-status.json) — Reddit Status API

**Homelab / Self-Hosted (update URLs & tokens after importing):**
- [`pihole-homelab.json`](./pihole-homelab.json) — Pi-hole summary stats
- [`home-assistant.json`](./home-assistant.json) — Home Assistant API status (uses `Authorization: Bearer ...`)
- [`proxmox-node.json`](./proxmox-node.json) — Single Proxmox VE node version check
- [`proxmox-node-stats.json`](./proxmox-node-stats.json) — Grouped multi-node Proxmox VE stats (`PVE1`, `PVE2`) with scaled CPU, RAM, Swap, Uptime metrics and collapsible details

Remember to click **Save** in Settings to persist changes.
