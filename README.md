# SEforAll — Energy Compacts Visualization Tools

Two self-contained, browser-based tools for exploring the UN Energy Compacts ecosystem: an **interactive network graph** and an **interactive metrics dashboard**. Both run entirely in the browser — no server, no installation, no upload of your data to any third party.

This repository contains the source HTML tools, sample data, written user guides, and PDF walkthroughs for both tools.

---

## Repository Structure

```
SEforAll/
├── Network Graph/
│   ├── Graph_Network_Interactive.html      ← open this in a browser
│   ├── Graph_Network_README.md             ← full tool documentation
│   ├── Graph_Network_User_Guide.pdf
│   ├── compact_actor_database.xlsx         ← sample input data
│   └── images/
│
└── Metrics Dashboard/
    ├── SE4All_Dashboard_Interactive.html   ← open this in a browser
    ├── SE4All_Dashboard_README.md          ← full tool documentation
    ├── SE4All_Dashboard_User_Guide.pdf
    ├── Metrics Dashboard Data.xlsx         ← sample input data
    └── images/
```

---

## 1. Energy Compacts Ecosystem Network Graph

📄 [Full documentation](Network%20Graph/Graph_Network_README.md)

An interactive force-directed network visualization of compacts and the actors (countries, organizations, companies, institutions) that participate in them. Built on D3.js, the graph reveals how compacts cluster, which actors serve as hubs, and how compacts connect through shared participants. The current sample dataset resolves to **169 compacts**, **1,204 actors**, and **2,067 relationships**.

### Demo

https://github.com/Parhamzn/SEforAll/raw/main/Network%20Graph/network_graph_demo.mp4

<video src="https://github.com/Parhamzn/SEforAll/raw/main/Network%20Graph/network_graph_demo.mp4" controls width="100%"></video>

![Default view: full ecosystem with Node Connections ≥ 5 — compacts (amber squares) and actors (blue circles)](Network%20Graph/images/p02_x0007_1320x725.jpeg)

### Adjust Density to Reveal Structure

Spread nodes apart with the Node Spacing slider to surface labels and topology.

![Node Spacing at 2.9× spreads the network and reveals labels and clusters](Network%20Graph/images/p04_x0011_1320x723.jpeg)

Or raise the Node Connections threshold to peel away long-tail nodes and isolate the most-connected hub compacts.

![Node Connections ≥ 29 leaves only the highest-degree hub compacts](Network%20Graph/images/p03_x0009_1320x723.jpeg)

### Filter Toggles

Switch between **All**, **Compacts only**, and **Actors only** to reduce the graph to one node type at a time.

![Compacts-only view — actor circles hidden, compact-to-compact links remain](Network%20Graph/images/p05_x0014_1320x723.jpeg)

![Compacts-only across the full ecosystem — only the cross-compact backbone is visible](Network%20Graph/images/p06_x0017_1320x725.jpeg)

![Actors-only view around an isolated compact — only the participating actors are shown](Network%20Graph/images/p05_x0015_1320x723.jpeg)

### Click-to-Isolate + Detail Sidebar

Click any node to isolate it and its direct neighborhood; the sidebar enumerates every linked compact and actor along with the actor's role in each compact. Sidebar items are clickable, allowing chain navigation through the network.

![Clicking SEforALL isolates it and opens the detail sidebar — 46 linked compacts and 64 actors with roles](Network%20Graph/images/p05_x0013_1320x723.jpeg)

### Configurable Export

The Export HTML panel lets you choose which UI elements (controls, stats, sidebar, legend) ship in the exported standalone file.

![Export panel — toggle which UI elements are included in the exported HTML](Network%20Graph/images/p07_x0019_1320x723.jpeg)

**Highlights**

- ID-based entity joining tolerates spelling variants across rows
- Auto-detects actors whose names match compacts and promotes them to compact-typed nodes — revealing cross-compact links
- Search, node-connections filter, node-spacing slider, and Compacts-only / Actors-only toggles
- Click any node to isolate it and view its full role-by-role connection list in the sidebar
- Two themes (UN Energy / SEforAll) and configurable HTML export (choose which UI elements ship in the exported file)
- D3.js and SheetJS loaded from CDN with **Subresource Integrity (SRI)** hashes; all user-supplied text is HTML-escaped before rendering

**Run it:** double-click `Network Graph/Graph_Network_Interactive.html`.

---

## 2. Energy Compacts Metrics Dashboard

📄 [Full documentation](Metrics%20Dashboard/SE4All_Dashboard_README.md)

A self-contained HTML tool that ingests energy compact data (CSV or Excel) and generates a fully interactive dashboard covering all SDG 7 metrics, finance, jobs, transport, GHG emissions, and net-zero pledges. The dashboard ships in two visual themes — UN Energy (light) and SEforAll (dark) — and either theme can be exported as a standalone HTML file ready to drop onto any web server.

![Four-step workflow: Upload File → Pick Date → Launch → Export](Metrics%20Dashboard/images/p01_x0017_900x220.png)

### Dual Theme

Two visual themes ship in the same file. Toggle between them instantly using the V1/V2 buttons in the bottom-right toolbar; whichever is active when you click **Export HTML** becomes the standalone deliverable.

**V1 — UN Energy Website Theme (light)**

![V1 light theme: dashboard with map, SDG 7 tiles, and Other Metrics grid](Metrics%20Dashboard/images/dashboard_v1_light.png)

**V2 — SEforAll Website Theme (dark)**

![V2 dark theme: identical layout in dark navy / amber palette](Metrics%20Dashboard/images/dashboard_v2_dark.png)

### Bottom Toolbar

![Bottom toolbar — New file, V1, V2, Export HTML](Metrics%20Dashboard/images/p01_x0049_1268x146.jpeg)

### Input Data Structure

The dashboard auto-detects columns by header keywords — exact column order does not matter, and extra columns are safely ignored.

![Excel / CSV column layout: A=Compact Name, B=Compact ID, C–L=Proponent Types, M–X=Metric Values, Y–AB=Coverage Regions, AC–AL=Target Years](Metrics%20Dashboard/images/p01_x0059_900x380.png)

One-hot columns (proponent types, coverage regions, net-zero) accept a wide range of yes-values:

![Accepted yes/no values for one-hot columns](Metrics%20Dashboard/images/p01_x0278_500x280.png)

### Per-Metric Target-Year Filtering

The Target Year filter operates at the metric level, not the compact level — each metric is summed only over compacts whose target year *for that specific metric* is at or below the selected threshold.

![Target Year dropdown: All, ≤ 2030, ≤ 2040, ≤ 2050, ≤ 2060](Metrics%20Dashboard/images/p01_x0266_700x160.png)

**Highlights**

- Drag-and-drop CSV / XLSX upload, parsed entirely in-browser
- Interactive world map with click-to-filter coverage regions
- 12 SDG-aligned metric tiles (SDG 7.1.1, 7.1.2, 7.2, 7.3, 8, 11, 13, 17, Net Zero)
- Filters: proponent type, coverage region, origin country, per-metric target year
- Two themes (UN Energy / SEforAll), toggled with one click
- Export to standalone HTML with your data baked in — ready for GitHub Pages, Netlify, or any static host

**Run it:** double-click `Metrics Dashboard/SE4All_Dashboard_Interactive.html`.

---

## How They Fit Together

Both tools consume related but distinct slices of the same underlying Energy Compacts data:

| | Network Graph | Metrics Dashboard |
|---|---|---|
| **Unit of analysis** | One row per actor-compact relationship | One row per compact |
| **Primary question** | *Who is working with whom?* | *How much progress are compacts delivering?* |
| **Key fields** | Compact ID, Actor ID, Role | SDG metrics, target years, regions, proponent types |
| **Output** | Force-directed network + clickable sidebar | Aggregated metric tiles + filterable map |
| **Export** | Standalone themed HTML (with selectable UI panels) | Standalone themed HTML |

Use the network graph to understand the partnerships behind the numbers; use the dashboard to track delivery against the SDG 7 targets.

---

## Technology

- **No backend.** Everything runs in the browser.
- **No data leaves your machine.** Parsing happens locally via PapaParse (CSV) and SheetJS (Excel).
- **Dependencies** (loaded from public CDNs on first open):
  - Network Graph: D3.js v7.9.0, SheetJS v0.18.5 (both pinned with SRI hashes)
  - Dashboard: React 18, Babel Standalone, PapaParse, SheetJS
- **Browser support:** any modern browser (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+).

---

## License & Attribution

Tools developed for visualizing data from the [UN Energy Compacts](https://www.un.org/en/energy-compacts) framework, aligned with the [Sustainable Energy for All (SEforAll)](https://www.seforall.org/) initiative.
