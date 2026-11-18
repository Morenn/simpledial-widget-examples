# TimeZone Widgets Guide

TimeZone Widgets display live clocks for multiple IANA time zones inside any workspace area (**Header**, **Left**, **Center**, **Right**, or **Footer**), and include an interactive **TimeZone Calculator** directly on the new-tab page.

Open **Settings → Custom Widgets** and click **+ Add TimeZone** to create one. Once created, place and order it in **Settings → Appearance → Widgets**.

---

## 1. Configuration Options

- **Name**: Optional header title (for example, `World Clocks` or `Global Ops`). If both Name and Icon are left empty, the header is hidden in live clock mode.
- **Icon**: Optional emoji or custom icon (`https://...` URL or uploaded image).
- **Time Zones** (`timeZones`): List of `{ label, timeZone }` entries using standard IANA time zone identifiers (such as `UTC`, `Europe/London`, `America/New_York`, `Asia/Tokyo`). Invalid time zones are automatically ignored, and if `label` is omitted, the city name from the IANA identifier is used.
- **24-Hour Format** (`use24Hour`): Toggle between 24-hour (`true`, default) and 12-hour AM/PM (`false`) display.
- **Show Seconds** (`showSeconds`): Toggle seconds display (`false` by default).

---

## 2. Interactive TimeZone Calculator

Every TimeZone Widget doubles as a quick meeting/timezone converter:

1. **Click any displayed time** in the widget to edit it inline (for example, enter `14:30` or `09:00:00`).
2. Press **Enter** (or blur the input) to pin that time in that zone's wall clock—all other zones in the widget immediately recalculate to the matching instant.
3. Zones that fall on the previous or next calendar day relative to the pinned base zone automatically show a **`-1d`** or **`+1d`** day-shift badge.
4. Click the **Reset** button (`↺`) in the widget header to return to live clocks.

---

## 3. Export, Import & Load from URL

TimeZone widgets use the same `simple-dial-custom-widgets` JSON format as all other custom widgets and can be exported, imported from `.json`, or loaded/updated from an `https://...` URL in **Settings → Custom Widgets**.

---

## 4. Examples in This Folder

Import any `.json` file in this folder via **Settings → Custom Widgets → 📤 Import**:

- [`world-clocks-24h.json`](./world-clocks-24h.json) — 24-hour world clocks (UTC, London, New York, Tokyo) placed in **Left**
- [`us-tech-hubs-12h.json`](./us-tech-hubs-12h.json) — 12-hour US & UTC clocks
- [`global-ops-with-seconds.json`](./global-ops-with-seconds.json) — 24-hour operations clocks with seconds enabled, placed in **Header**

Remember to click **Save** in Settings to persist changes.
