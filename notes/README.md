# Simple Notes / Scratchpad Widgets Guide

Simple Notes Widgets provide persistent scratchpads, checklists, and timed reminders directly on your new-tab page—inside any workspace area (**Header**, **Left**, **Center**, **Right**, or **Footer**).

Open **Settings → Custom Widgets** and click **+ Add Notes** to create one. Once created, place and order it in **Settings → Appearance → Widgets**.

---

## 1. Configuration Options

- **Name & Icon**: Widget title and optional emoji or custom icon (`https://...` URL or uploaded image).
- **Compact Mode** (`compactMode`): Renders a slim header/launcher pill (ideal for **Header** or **Footer**), opening the full notes & checklist modal on click. When `false`, the widget renders its entries inline (ideal for **Left**, **Center**, or **Right**).

---

## 2. Notes, Checklists & Reminders

Each Notes widget stores its own list of entries in `chrome.storage.local` (`myspeeddial-widget-notes`):

- **Note Entries**: Each entry supports a **Title** (up to 120 characters), **Body** (up to 2,000 characters), and an independent **To-Do checklist** (each item up to 240 characters).
- **Reminders on To-Dos**: Attach a reminder to any unchecked to-do item using quick presets (in minutes) or a custom time (`HH:MM`—rolled over to the next day if already passed—or full date/time).
- **Live Countdowns & Notifications**: Scheduled reminders show a live countdown (`45m`, `2h`, `1d`), highlight when due soon (`<= 5m`), and trigger an alert (`Due!`) when the target time is reached.

---

## 3. Examples in This Folder

Import any `.json` file in this folder via **Settings → Custom Widgets → 📤 Import**:

- [`quick-scratchpad.json`](./quick-scratchpad.json) — Inline scratchpad widget
- [`work-tasks.json`](./work-tasks.json) — Inline work tasks widget placed in **Right**
- [`compact-reminders.json`](./compact-reminders.json) — Compact reminders widget (`compactMode: true`) placed in **Header**

Remember to click **Save** in Settings to persist changes.
