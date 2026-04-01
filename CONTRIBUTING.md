# Contributing to OrgChartCreator

Thanks for your interest in contributing! This is a single-file HTML tool — no build system, no dependencies, no npm. Just plain HTML, CSS, and vanilla JavaScript.

## Getting started

1. Fork the repo
2. Clone it locally
3. Open `index.html` directly in your browser — that's it

No build step, no dev server required.

## How it's structured

Everything lives in `index.html`:

| Section | What it does |
|---|---|
| `:root` / `:root.light` CSS vars | All theme colours — dark and light |
| `#upload-screen` | The initial CSV upload UI |
| `#topbar` | Toolbar with search, buttons, theme toggle |
| `#canvas-wrap` | The chart rendering area |
| `parseCSV()` | Parses uploaded CSV into row objects |
| `buildTree()` | Converts flat rows into a parent-child tree |
| `layoutTree()` | Calculates x/y positions for every node |
| `render()` | Draws nodes and edges into the DOM/SVG |
| `fitAll()` | Auto-scales and centres the view |
| Export PNG block | Canvas-based PNG snapshot of current state |
| Standalone theme script | Isolated from main script to avoid strict-mode issues |

## Ground rules

- Keep it a **single file** — no external dependencies, no build tools
- Must work offline (no CDN calls required for core functionality — Google Fonts is fine to keep as a nice-to-have)
- Test in Chrome and Edge before submitting
- Keep the CSV format backwards compatible — don't break existing files

## Submitting changes

1. Create a branch: `git checkout -b my-feature`
2. Make your changes
3. Test with a real CSV (the included `orgchart_template.csv` is a good start)
4. Open a pull request with a clear description of what you changed and why

## Reporting bugs

Open a GitHub Issue with:
- What you expected to happen
- What actually happened
- Browser and OS
- A minimal CSV that reproduces the issue (remove any sensitive names)

## Ideas and feature requests

Open an Issue tagged `enhancement`. Check the README for a list of ideas already on the radar.
