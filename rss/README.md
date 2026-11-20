# RSS / Atom Feed Widgets Guide

RSS / Atom Feed widgets let you monitor news, security advisories, and blog updates directly from any workspace area (**Header**, **Left**, **Center**, **Right**, or **Footer**), with unread badges and a built-in reader modal.

## Configuration Fields

- **`type`**: `"rss-feed"`
- **`name`**: Display name for the feed
- **`feedUrl`**: `https://...` (or `http://...`) RSS or Atom feed URL
- **`refreshMinutes`**: Polling interval in minutes (`5`–`1440`, default `30`)
- **`maxItems`**: Maximum number of items to keep (`1`–`50`, default `15`)
- **`groupName`** *(optional)*: Combine multiple feeds with the same group name into a single compact widget
- **`icon`** / **`customIcon`** *(optional)*: Emoji fallback and favicon/image URL

## Examples in This Folder

Import any `.json` file via **Settings → Custom Widgets → 📤 Import**:

- [`security-feeds.json`](./security-feeds.json) — Pre-grouped `Security Feeds` bundle (CISA ICS Advisories, The Hacker News, Krebs on Security, Cloudflare Security, Unit 42)
- [`cisa-ics-advisories.json`](./cisa-ics-advisories.json) — Standalone CISA ICS Advisories feed

Remember to grant host permission when prompted and click **Save** in Settings to persist changes.
