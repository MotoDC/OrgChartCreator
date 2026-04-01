# OrgChartCreator

> Ever wish you had a quick way to map out a customer org before a big meeting? We built one. Takes 30 seconds, lives on a link, exports to slides.

**Live tool → [https://motodc.github.io/OrgChartCreator/](https://motodc.github.io/OrgChartCreator/)**

---

## What it does

OrgChartCreator turns a simple CSV file into a fully interactive org chart in your browser — no software to install, no account required, no data leaves your machine.

Built for account managers and sales engineers who need to map a customer's organization quickly and present it clearly in business reviews.

**Features:**
- Upload or drag-and-drop a CSV file
- Auto-generates a hierarchical org chart from name + manager relationships
- Collapse and expand individual branches at any level
- Collapse all / Expand all with a single click
- Search by name, role, or location — highlights matches, dims others
- Light and dark mode toggle
- Export to PNG — respects current collapsed state, ready to paste into slides
- Zoom (scroll to zoom, anchors to cursor), pan (drag), fit-to-screen
- Node cards show name, role, location, email (clickable), direct reports count
- Works in any modern browser — Chrome, Edge, Firefox, Safari

---

## How to use it

### 1. Prepare your CSV

Your CSV needs at minimum two columns: `name` and `manager`. All other columns are optional.

| Column | Required | Description |
|---|---|---|
| `name` | ✅ | Person's full name |
| `manager` | ✅ | Their manager's name (must match exactly). Leave blank for the top of the org. |
| `role` | Optional | Job title |
| `location` | Optional | City or office |
| `email` | Optional | Shown as a clickable mailto link |
| `phone` | Optional | Phone number |

**Column order doesn't matter** — the app detects columns by header name.

Download the [template CSV](orgchart_template.csv) to get started.

### 2. Example CSV

```csv
name,manager,role,location,email,phone
Jane Smith,,Chief Technology Officer,Toronto,jane.smith@company.com,
John Doe,Jane Smith,VP Engineering,Toronto,john.doe@company.com,
Sarah Lee,Jane Smith,VP Operations,Vancouver,sarah.lee@company.com,
Mike Chen,John Doe,Director Software Dev,Toronto,mike.chen@company.com,
```

### 3. Generate the chart

1. Open the tool at [https://motodc.github.io/OrgChartCreator/](https://motodc.github.io/OrgChartCreator/)
2. Upload your CSV or drag and drop it onto the upload area
3. Click **Generate Org Chart**

### 4. Navigate the chart

| Action | How |
|---|---|
| Collapse a branch | Click **▾ collapse** on any node |
| Expand a branch | Click **▸ N hidden** on any node |
| Collapse everything | Click **Collapse all** in the toolbar |
| Expand everything | Click **Expand all** in the toolbar |
| Zoom | Scroll wheel (anchors to cursor position) |
| Pan | Click and drag the canvas |
| Fit to screen | Click **Fit all** button |
| Search | Type in the search box — matches highlight, others dim |
| Export | Click **Export PNG** — exports current view including collapsed state |

---

## Hosting it yourself

This is a single-file HTML application. To host it:

1. Download `index.html` and `orgchart_template.csv`
2. Place both files in the same folder/directory
3. Open `index.html` in any browser

For SharePoint or other hosting, both files need to be in the same root location for the template download link to resolve correctly.

> **Note:** SharePoint's OneDrive personal storage (`-my.sharepoint.com`) wraps HTML files in a preview container that breaks JavaScript. Use a SharePoint **Team Site** document library, or host via GitHub Pages / Azure Static Web Apps instead.

---

## Contributing

Contributions are very welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

Some ideas for improvements:
- Search that also highlights the path up to root
- Click a node to highlight their full reporting chain
- Import from other formats (Excel direct, JSON)
- Print/PDF export
- Node color coding by department or level
- Editable nodes (rename, change manager) directly in the UI
- Undo/redo for collapse state

---

## License

MIT — see [LICENSE](LICENSE) for details.
