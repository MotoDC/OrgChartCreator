# OrgChartCreator

> Ever wish you had a quick way to map out a customer org before a big meeting? We built one. Takes 30 seconds, lives on a link, exports to slides.

**Live tool → [https://motodc.github.io/OrgChartCreator/](https://motodc.github.io/OrgChartCreator/)**

---

## New in v5.0 — Edit directly in the chart

You can now fix and update org data without ever touching the CSV manually.

**Hover any node** to reveal two action buttons in the top-right corner of the card:

| Button | What it does |
|---|---|
| ✏️ Pencil | Opens the edit modal for that person |
| ⊕ Crosshair | Focuses the chart on that person's subtree |

**The edit modal lets you update:**
- Name, role, location, email, phone
- Relationship health (🟢 🟡 🔴)
- Who they report to — type a name and autocomplete will suggest matches

The editor validates your changes before saving — it will catch circular reporting chains, self-assignment, and duplicate names.

> **Important — changes are in-browser only.** Edits do not write back to your original CSV file. When you make a change, a red banner appears at the top of the screen. Click **Download updated CSV** in that banner to save a new file with your changes applied. The downloaded file uses your original filename plus a timestamp — for example, `acme_2026-04-07_1430.csv` — so your source file is never overwritten. Re-upload that file next time to start from where you left off.

---

## What it does

OrgChartCreator turns a simple CSV file into a fully interactive org chart in your browser — no software to install, no account required, and **no data ever leaves your computer**. All processing happens locally in your browser.

Built for account managers and sales engineers who need to map a customer's organization quickly and present it clearly in business reviews.

**Features:**
- Upload or drag-and-drop a CSV file
- Auto-generates a hierarchical org chart from name + manager relationships
- **Hover any node** to edit contact details or focus the chart on that person's subtree
- Edit name, role, location, email, phone, manager, and relationship health inline
- Collapse and expand individual branches at any level
- Collapse all / Expand all with a single click
- Search by name, role, or location — auto pan and zoom to matched nodes
- Relationship indicator — colour-coded dot (🟢 🟡 🔴) on each node card
- Light and dark mode toggle — remembers your preference
- Export PNG — captures exactly what's on screen at 2x resolution, ready to paste into slides
- Download updated CSV — exports your edited data with a timestamped filename
- Zoom (scroll to zoom, anchors to cursor), pan (drag), fit-to-screen
- Node cards show name, role, location, email (clickable), direct reports count
- Handles bad data gracefully — unresolvable managers surface as an **Uncategorized** node
- Works in any modern browser — Chrome, Edge, Firefox, Safari

---

## How to use it

### 1. Prepare your CSV

Your CSV needs at minimum two columns: `name` and `manager`. All other columns are optional.

| Column | Required | Accepted header names | Description |
|---|---|---|---|
| `name` | ✅ | `name` | Person's full name |
| `manager` | ✅ | `manager`, `managername`, `reportsto` | Their manager's name — must match a `name` in the file exactly. **Leave blank for the root of the org** (e.g. the CTO). |
| `role` | Optional | `role`, `title`, `jobtitle`, `position` | Job title |
| `location` | Optional | `location`, `loc`, `city`, `office` | City or office |
| `email` | Optional | `email`, `emailaddress`, `mail` | Shown as a clickable mailto link |
| `phone` | Optional | `phone`, `mobile`, `tel` | Phone number |
| `relationship` | Optional | `relationship`, `rel`, `status`, `health` | Relationship health — see below |

**Column order doesn't matter** — the app detects columns by header name.

Download the [template CSV](orgchart_template.csv) to get started.

---

### 2. Relationship indicator

Add a `relationship` column to show a colour-coded dot on each node card — useful for tracking account health at a glance during business reviews.

| Value | Accepted inputs | Indicator |
|---|---|---|
| Green | `green`, `g` | 🟢 |
| Yellow | `yellow`, `y`, `amber` | 🟡 |
| Red | `red`, `r` | 🔴 |
| None | *(blank)* | No dot shown |

Values are case-insensitive. Existing CSVs without this column work exactly as before.

---

### 3. Handling unknown or vacant managers

The app handles imperfect data gracefully:

| Manager value | How it's treated |
|---|---|
| **Blank** | Intentional root node (e.g. CTO/CEO) — placed at the top of the chart |
| **`VACANT`, `UNKNOWN`, `N/A`, `TBD`** | Bad data — person is placed under an **Uncategorized** node |
| **A name that doesn't match anyone** | Bad data — person is placed under **Uncategorized** |

The **Uncategorized** node appears as a distinctly styled amber card alongside the real org root. It starts collapsed so it doesn't dominate the view — it's a signal to go fix your data.

> **Tip:** If someone reports to a position that's currently unfilled, assign them directly to the skip-level manager rather than leaving the manager as `VACANT`. This keeps the chart clean until the role is filled.

---

### 4. Example CSV

```csv
name,manager,role,location,email,phone,relationship
Jane Smith,,Chief Technology Officer,Toronto ON,jane.smith@company.com,,green
John Doe,Jane Smith,VP Engineering,Toronto ON,john.doe@company.com,,green
Sarah Lee,Jane Smith,VP Operations,Vancouver BC,sarah.lee@company.com,,yellow
Mike Chen,John Doe,Director Software Dev,Toronto ON,mike.chen@company.com,,red
Priya Patel,John Doe,Director QA,Toronto ON,priya.patel@company.com,,
```

---

### 5. Generate the chart

1. Open the tool at [https://motodc.github.io/OrgChartCreator/](https://motodc.github.io/OrgChartCreator/)
2. Upload your CSV or drag and drop it onto the upload area
3. Click **Generate Org Chart**

---

### 6. Navigate the chart

| Action | How |
|---|---|
| Collapse a branch | Click **▾ collapse** on any node |
| Expand a branch | Click **▸ N hidden** on any node |
| Collapse everything | Click **Collapse all** in the toolbar |
| Expand everything | Click **Expand all** in the toolbar |
| Edit a person | Hover any node → click the **✏️ pencil** button |
| Focus on a person | Hover any node → click the **⊕ crosshair** button |
| Reset focus | Click **✕ Reset focus** in the blue banner |
| Zoom | Scroll wheel — anchors to cursor position |
| Pan | Click and drag the canvas |
| Fit to screen | Click **Fit all** |
| Search | Type in the search box — view auto-pans and zooms to matches |
| Export | Click **Export PNG** — captures what's currently on screen at 2x |
| Toggle theme | Click **Light mode / Dark mode** toggle (top right) |

**Export tip:** The PNG export captures exactly what's visible on screen. Pan and zoom to frame the section you want, collapse what you don't need, then export. This gives you a clean, presentation-ready image every time.

---

## Hosting it yourself

This is a single-file HTML application with no dependencies. To host it:

1. Download `index.html` and `orgchart_template.csv`
2. Place both files in the same folder/directory
3. Open `index.html` in any browser — works offline

For SharePoint or other hosting, both files need to be in the same root location for the template download link to resolve correctly.

> **Note:** SharePoint's OneDrive personal storage (`-my.sharepoint.com`) wraps HTML files in a preview container that blocks JavaScript. Use a SharePoint **Team Site** document library, or host via GitHub Pages / Azure Static Web Apps instead.

---

## Contributing

Contributions are very welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

Some ideas for improvements:
- Search that highlights the full path up to root
- Click a node to highlight their full reporting chain
- Import directly from Excel (.xlsx) without needing to export as CSV
- Print / PDF export
- Node colour coding by department or level
- Editable nodes (rename, change manager) directly in the UI
- Undo/redo for collapse state
- Multiple CSV files merged into one chart

---

## Changelog

| Version | Changes |
|---|---|
| **v5.2** | Add direct report button on hover tray (opens add modal pre-filled with manager); Delete button on hover tray with two-state confirm — simple for leaf nodes, choice of Reassign/Uncategorized when the person has direct reports |
| **v5.1** | Add person: new "+ Add person" button in topbar opens a create modal; placement control (Reports to / Root node / Uncategorized) replaces plain manager text field in both add and edit modes |
| **v5.0** | In-chart editing: hover any node to reveal pencil (edit) and crosshair (focus) buttons; edit modal covers name, role, location, email, phone, manager (autocomplete with cycle/self-assignment/duplicate-name validation), and relationship health; right-click context menu replaced by hover tray; internal ID system so tree structure is ID-driven and renaming cascades safely; red dirty-state banner when unsaved edits exist; CSV download uses source filename + timestamp (e.g. `acme_2026-04-07_1430.csv`) |
| **v3.7** | PNG export now captures current viewport at 2x — exports exactly what you see on screen, respecting zoom/pan/collapse state |
| **v3.6** | PNG export: guard against empty canvas (incomplete fix); relationship dot included in export |
| **v3.5** | Relationship column: red/yellow/green dot on node cards |
| **v3.4** | PNG export fully excludes Uncategorized node and its children; connections redrawn from data not DOM to avoid stray lines |
| **v3.3** | PNG export now excludes Uncategorized node (incomplete fix) |
| **v3.2** | Added privacy notice on upload screen |
| **v3.1** | Fixed: blank manager = intentional root, not orphan; VACANT/UNKNOWN/unresolvable = bad data → Uncategorized |
| **v3.0** | fitAll now correctly frames all root nodes when collapsed; Uncategorized node starts collapsed so real tree is dominant |
| **v2.9** | Uncategorized node: bad/missing manager data now surfaces as a visible amber-styled root node instead of silent orphans |
| **v2.8** | buildTree now treats blank/VACANT/UNKNOWN managers as a hidden synthetic root, collapsing orphan nodes into a single clean tree |
| **v2.7** | Fixed context menu bug: click event firing before menu item handlers nulled ctxTargetName so Focus always received null; fixed render() using allRoots instead of activeRoots for visible node collection in focus mode |
| **v2.6** | Search auto pan/zoom to matched nodes; focus clears search state; focus mode opens one level deep with subtrees collapsed |
| **v2.5** | Right-click focus mode: focus on any person and their subtree |
| **v2.4** | Fixed collapse-all to mark all descendants, not just root nodes |
| **v2.3** | Added "Map your customer's org" heading, description, template download link |
| **v2.2** | Light/dark theme toggle, fixed truncated file, removed Cloudflare artifacts |
| **v2.1** | Light mode as default |
| **v2.0** | Merged best-of-both: rich node cards + collapse/expand + PNG export |

---

## License

MIT — see [LICENSE](LICENSE) for details.
