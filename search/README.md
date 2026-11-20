# Custom Search Widgets Guide

Custom Search Widgets let you add your own search bars—from simple query links to multi-filter JSON-encoded searches—directly into any workspace area (**Header**, **Left**, **Center**, **Right**, or **Footer**).

Open **Settings → Custom Widgets** to create, edit, delete, export, or import custom search widgets. Once created, each widget appears in **Settings → Appearance → Widgets** so you can choose its workspace area, alignment, row break, and display order.

---

## 1. Simple Search Mode (Default)

Use **Simple** mode when the target site accepts a regular URL with placeholders in the path or query string.

### Step-by-step: Wikipedia Search
1. Open **Settings → Custom Widgets** and click **+ Add Search**.
2. Set:
   - **Name**: `Wikipedia`
   - **Icon**: `📚` (or paste an `https://...` image URL, or upload an image file)
   - **Mode**: `Simple`
   - **URL Template**: `https://en.wikipedia.org/w/index.php?search={query}`
3. In **Variables**, keep the default variable:
   - **Key**: `query`
   - **Label**: `Search Wikipedia...`
   - **Type**: `Text`
4. Check the **Live Preview** at the bottom—typing `solar system` produces:
   `https://en.wikipedia.org/w/index.php?search=solar%20system`
5. Click **Save Widget**, then **Save** in Settings.

> **Tip:** Every `{variableKey}` in the URL template is automatically URL-encoded (`encodeURIComponent`) when submitted.

---

## 2. JSON Mode (Structured Multi-Filter Search)

Use **JSON** mode when a target web app expects a URL-encoded JSON object inside its URL (for example, `https://example.com/search/{json}` or `https://example.com/search?filter={json}`).

### How JSON Mode works
1. **URL Template** contains `{json}` where the serialized JSON should go.
2. **JSON Template** defines the exact JSON structure using `{variableKey}` placeholders.
3. **Empty-key omission (smart cleanup)**:
   - If a variable is left empty by the user, its JSON key is **omitted** from the output.
   - If an entire nested object or array becomes empty because all its child variables were left empty, that parent object/array is also **omitted**.
   - If *all* variables are empty, `{json}` resolves to `{}`.

### Example: Multi-Filter Search
Suppose your app accepts URLs like `https://example.com/search/{json}`:

- **URL Template**:
  ```text
  https://example.com/search/{json}
  ```
- **JSON Template**:
  ```json
  {
    "q": "{query}",
    "filters": {
      "category": "{category}",
      "updated": "{updated}",
      "tags": "{tags}"
    }
  }
  ```
- **Variables**:
  - `query` — **Text** (`Search keyword...`)
  - `category` — **Multi-select** (`Guides=guides, API Reference=api, Release Notes=releases`)
  - `updated` — **Dropdown** (`Any time=, Last 7 days=7d, Last 30 days=30d`)
  - `tags` — **Comma list** (`Tags (comma-separated)...`)

**Resulting output:**
- If you only type `authentication` and leave all filters empty, `filters` is omitted completely:
  ```json
  { "q": "authentication" }
  ```
  → `https://example.com/search/%7B%22q%22%3A%22authentication%22%7D`
- If you leave `query` empty and pick **Guides** + **API Reference**, **Last 7 days**, and tags `oauth, jwt`:
  ```json
  {
    "filters": {
      "category": ["guides", "api"],
      "updated": "7d",
      "tags": ["oauth", "jwt"]
    }
  }
  ```

---

## 3. Variable Types

| Type | Input UI | Value in Simple Mode | Value in JSON Mode |
|------|----------|----------------------|--------------------|
| `Text` | Text box | Trimmed string | String (omitted if empty) |
| `Comma list` | Text box (`a, b`) | Comma-joined string | Array of strings `["a","b"]` (omitted if empty) |
| `Dropdown` | `<select>` menu | Selected value | String (omitted if empty) |
| `Multi-select` | Checkboxes | Comma-joined values | Array of selected values (omitted if empty) |

---

## 4. Export, Import & Load from URL (Widget Library)

You can back up, share, or load custom search widgets from a file or a remote JSON URL:

- **Export all widgets**: Click **📥 Export** in **Settings → Custom Widgets** or **Settings → Export/Import → Custom Widgets**.
- **Export one widget**: Click **📥** next to a custom widget in **Saved Custom Widgets**.
- **Import from file**: Click **📤 Import** and select a `.json` file (supports full library exports, JSON arrays, or a single widget object). Widgets with a matching `id` update in place; new widgets are added automatically.
- **Load from URL**: Paste an `https://...` JSON URL in **Settings → Custom Widgets** and click **🌐 Load from URL**. The source URL is remembered on each loaded widget.
- **Manual Update & Revert**: Widgets loaded from a URL never auto-update. You can click **🔄** on a widget (or **🔄 Update from URL** in the library header) to manually fetch updates. Before applying an update, the previous configuration is saved so you can click **↩️** to revert if the new version is broken.

> **Security note:** Only import or load custom widgets from files and URLs you trust.

---

## 5. Grouping Search Engines & Prefix Auto-Routing

You can combine multiple search engines into a single compact search widget with a clickable engine switcher—and optionally auto-route queries by prefix:

1. In **Settings → Custom Widgets**, enter the same **Group (optional)** name (for example, `Web Search`) on two or more custom search widgets.
2. Check **Default in group** (or click **☆** in **Saved Custom Widgets**) on the engine you want selected initially and used as the group's placement entry in **Settings → Appearance → Widgets**.
3. On the new-tab page, click the search widget's icon button (`▾`) to switch between any engine in that group without leaving the bar.
4. **Prefix Auto-Routing (optional)**: Set `routePrefixes` (comma-separated, case-insensitive, longest prefix wins) on any member of a group—for example, `INC, CHG, RITM` on a ServiceNow widget. When you type a query starting with one of those prefixes (like `INC0012345`), the grouped bar automatically routes the submission to that matching engine.

---

## 6. Examples in This Folder

Import any `.json` file in this folder via **Settings → Custom Widgets → 📤 Import**:

- [`all-search-engines.json`](./all-search-engines.json) — Pre-grouped `Web Search` bundle (Google, Brave, DuckDuckGo, Bing, Ecosia)
- [`cve-review.json`](./cve-review.json) — Pre-grouped `CVE Review` bundle (NVD, CVE.org, GitHub Advisories, OSV.dev, CISA KEV, Snyk) with prefix auto-routing
- [`google.json`](./google.json) — Google Search
- [`brave.json`](./brave.json) — Brave Search
- [`duckduckgo.json`](./duckduckgo.json) — DuckDuckGo Search
- [`bing.json`](./bing.json) — Bing Search
- [`ecosia.json`](./ecosia.json) — Ecosia Search
- [`github-code.json`](./github-code.json) — GitHub Code Search
- [`mdn.json`](./mdn.json) — MDN Web Docs Search
- [`wikipedia.json`](./wikipedia.json) — Wikipedia Search
- [`youtube.json`](./youtube.json) — YouTube Search
- [`npm-packages.json`](./npm-packages.json) — npm Package Search
- [`servicenow.json`](./servicenow.json) — ServiceNow Search (with `routePrefixes` example)

Remember to click **Save** in Settings to persist changes.
