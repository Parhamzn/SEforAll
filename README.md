# SEforAll — Energy Compacts Visualization Tools

Two self-contained, browser-based tools for exploring the UN Energy Compacts ecosystem: an **interactive metrics dashboard** and an **interactive network graph**. Both run entirely in the browser — no server, no installation, no upload of your data to any third party.

This repository contains the source HTML tools, sample data, written user guides, and PDF walkthroughs for both tools.

---

## Repository Structure

```
SEforAll/
├── Metrics Dashboard/
│   ├── SE4All_Dashboard_Interactive.html   ← open this in a browser
│   ├── SE4All_Dashboard_README.md          ← full tool documentation
│   ├── SE4All_Dashboard_User_Guide.pdf
│   ├── Metrics Dashboard Data.xlsx         ← sample input data
│   └── images/
│
└── Network Graph/
    ├── Graph_Network_Interactive.html      ← open this in a browser
    ├── Graph_Network_README.md             ← full tool documentation
    ├── Graph_Network_User_Guide.pdf
    ├── compact_actor_database.xlsx         ← sample input data
    └── images/
```

---

## 1. Energy Compacts Metrics Dashboard

📄 [Full documentation](Metrics%20Dashboard/SE4All_Dashboard_README.md)

A self-contained HTML tool that ingests energy compact data (CSV or Excel) and generates a fully interactive dashboard covering all SDG 7 metrics, finance, jobs, transport, GHG emissions, and net-zero pledges. The dashboard ships in two visual themes — UN Energy (light) and SEforAll (dark) — and either theme can be exported as a standalone HTML file ready to drop onto any web server.

**Highlights**

- Drag-and-drop CSV / XLSX upload, parsed entirely in-browser
- Interactive world map with click-to-filter coverage regions
- 12 SDG-aligned metric tiles (SDG 7.1.1, 7.1.2, 7.2, 7.3, 8, 11, 13, 17, Net Zero)
- Filters: proponent type, coverage region, origin country, per-metric target year
- Two themes (UN Energy / SEforAll), toggled with one click
- Export to standalone HTML with your data baked in — ready for GitHub Pages, Netlify, or any static host

**Run it:** double-click `Metrics Dashboard/SE4All_Dashboard_Interactive.html`.

---

## 2. Energy Compacts Ecosystem Network Graph

📄 [Full documentation](Network%20Graph/Graph_Network_README.md)

An interactive force-directed network visualization of compacts and the actors (countries, organizations, companies, institutions) that participate in them. Built on D3.js, the graph reveals how compacts cluster, which actors serve as hubs, and how compacts connect through shared participants. The current sample dataset resolves to **169 compacts**, **1,204 actors**, and **2,067 relationships**.

**Highlights**

- ID-based entity joining tolerates spelling variants across rows
- Auto-detects actors whose names match compacts and promotes them to compact-typed nodes — revealing cross-compact links
- Search, node-connections filter, node-spacing slider, and Compacts-only / Actors-only toggles
- Click any node to isolate it and view its full role-by-role connection list in the sidebar
- Two themes (UN Energy / SEforAll) and configurable HTML export (choose which UI elements ship in the exported file)
- D3.js and SheetJS loaded from CDN with **Subresource Integrity (SRI)** hashes; all user-supplied text is HTML-escaped before rendering

**Run it:** double-click `Network Graph/Graph_Network_Interactive.html`.

---

## How They Fit Together

Both tools consume related but distinct slices of the same underlying Energy Compacts data:

| | Metrics Dashboard | Network Graph |
|---|---|---|
| **Unit of analysis** | One row per compact | One row per actor-compact relationship |
| **Primary question** | *How much progress are compacts delivering?* | *Who is working with whom?* |
| **Key fields** | SDG metrics, target years, regions, proponent types | Compact ID, Actor ID, Role |
| **Output** | Aggregated metric tiles + filterable map | Force-directed network + clickable sidebar |
| **Export** | Standalone themed HTML | Standalone themed HTML (with selectable UI panels) |

Use the dashboard to track delivery against the SDG 7 targets; use the network graph to understand the partnerships behind those numbers.

---

## Technology

- **No backend.** Everything runs in the browser.
- **No data leaves your machine.** Parsing happens locally via PapaParse (CSV) and SheetJS (Excel).
- **Dependencies** (loaded from public CDNs on first open):
  - Dashboard: React 18, Babel Standalone, PapaParse, SheetJS
  - Network Graph: D3.js v7.9.0, SheetJS v0.18.5 (both pinned with SRI hashes)
- **Browser support:** any modern browser (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+).

---

## License & Attribution

Tools developed for visualizing data from the [UN Energy Compacts](https://www.un.org/en/energy-compacts) framework, aligned with the [Sustainable Energy for All (SEforAll)](https://www.seforall.org/) initiative.
