# Energy Compacts Metrics Dashboard — Interactive Tool

## Overview

This is a self-contained HTML file that lets you upload energy compact data (CSV or Excel), select a data-updated date, and instantly generate a fully interactive dashboard. The dashboard comes in two visual themes — light (V1) and dark (V2) — with identical layouts, and you can export either as a standalone HTML file ready to deploy on a website.

**No server, no installation, no internet required for the dashboard itself** — the file runs entirely in your browser. The only external resources it fetches are fonts (Google Fonts) and JavaScript libraries (React, Babel, PapaParse, SheetJS) from CDNs on first load.

---

## How to Use

### Step 1 — Open the File

Double-click `SE4All_Dashboard_Interactive.html` on your computer. It opens in your default browser.

### Step 2 — Upload Your Data

Drag and drop (or click to browse) a `.csv` or `.xlsx` file containing your energy compact data. The parser auto-detects columns based on header names. Once parsed, a green confirmation shows how many compacts and proponent types were found.

### Step 3 — Select the Data Date

Pick the date when the data was last updated using the calendar date picker. This date is displayed on the dashboard header (e.g., "Updated 15 May 2026"). This field is required before launching.

### Step 4 — Launch & Explore

Click "Launch Dashboard" to enter the interactive dashboard. The opening page is titled "Energy Compacts Metrics Dashboard". Use the bottom-right toolbar to:

- **V1 / V2** — switch between UN Energy Website Theme (light) and SEforAll Website Theme (dark)
- **⤓ Export HTML** — download the currently displayed theme as a standalone HTML file with your data baked in, ready for website deployment
- **↩ New file** — return to the upload screen to load different data

---

## Dashboard Layout

The dashboard is titled **Energy Compacts Metrics Dashboard** and organized into three main sections:

### SDG 7 Metrics (next to the map)
Displayed prominently alongside the interactive world map. Includes four key metrics: SDG 7.1.1 (Electricity Connections), SDG 7.1.2 (Clean Cooking Access), SDG 7.2 (Renewable Capacity), and SDG 7.3 (Energy Savings). These tiles stretch to match the height of the map.

### Geographic Distribution
An interactive world map showing coverage regions. Click any region on the map to toggle it as a filter. Active regions are highlighted in color.

### Other Metrics
A grid of remaining metrics including Finance (displayed first), GHG Emissions Averted, Green Jobs Created, Green Jobs Training, Clean Transport Vehicles, Charging Infrastructure, Partnerships for Goals, and Net Zero Pledges.

---

## Visual Themes

Both themes have identical layouts, filters, and functionality. The only difference is the color scheme:

- **V1: UN Energy Website Theme** — White background, dark text, orange (#e89923) accents
- **V2: SEforAll Website Theme** — Dark navy background (#0d1b2a) matching the SE4All branding, white text, bright amber (#f5a800) accents

Toggle between them instantly using the V1/V2 buttons in the bottom-right toolbar. Exported files are named according to the selected theme.

---

## Expected Data Format

The tool expects a specific column structure. Columns are identified by keywords in the header row — the exact column order does not matter, and extra columns are safely ignored.

### Column A — Compact Name

The name or registry identifier for each energy compact. Any header containing "compact", "registry", or "name" (but not "SDG") is recognized.

**Required.** Rows with empty compact names are skipped.

### Columns C–L — Proponent Types (One-Hot Encoded)

Each proponent type gets its own column. The header must start with **"Proponent Type"** followed by the type name.

Example headers: `Proponent Type Private Sector`, `Proponent Type Member State`, `Proponent Type NGO`

Cell values use one-hot encoding: `Y` means the compact belongs to that type, anything else means it does not. A single compact can belong to multiple proponent types.

**Dynamic.** Adding or removing proponent type columns automatically updates the dashboard filters.

### Columns M–X — Metric Values

These columns contain the numeric values for each SDG metric. They are matched by keywords in the header:

| Header keyword | Metric |
|---|---|
| `finance committed` | Finance Committed (USD) |
| `SDG7.1.1` or `electricity connection` | Electricity Connections (million people) |
| `SDG7.1.2` or `clean cooking` | Clean Cooking Access (million people) |
| `SDG7.2` or `renewable capacity` | Renewable Capacity (GW) |
| `SDG7.3` or `energy savings` | Energy Savings (GWh) |
| `green jobs created` | Green Jobs Created |
| `jobs training` or `people trained` | Green Jobs Training |
| `buses` or `vehicles or trains` | Clean Transport Vehicles |
| `charging` or `refueling` | Charging & Refueling Infrastructure |
| `GHG` or `SDG13` | GHG Emissions Averted (million tonnes) |
| `partnerships` or `SDG17` | Partnerships for Goals |
| `net zero` | Net Zero Pledge (Y/N → counted as 1 or 0) |

Numbers can be in standard notation (`1000000`), scientific notation (`1.5E+09`), or with commas (`1,000,000`). Empty cells, dashes, and "N/A" are treated as zero.

### Column AM — Origin Country

Contains the name of the country where the compact originates (e.g., "India", "Brazil", "Germany"). The header must contain "origin country". This column populates the Origin Country dropdown filter. When a country is selected, its corresponding map region is highlighted automatically.

**Dynamic.** The list of countries in the filter is discovered from your data.

### Column AN — Notes

An optional free-text column for additional information about each compact (e.g., "HQ in São Paulo", "Government entity"). This column is preserved in the data but is not currently displayed on the dashboard or used for filtering.

### Columns Y–AB — Coverage Regions (One-Hot Encoded)

Each coverage region gets its own column. The header must start with **"Coverage Region"** followed by the region name.

Expected headers: `Coverage Region Americas`, `Coverage Region Europe`, `Coverage Region Asia-Pacific`, `Coverage Region Africa`

Same one-hot encoding as proponent types (`Y` = covered). A compact can cover multiple regions.

**Note:** The four regions above are mapped to the interactive world map. Adding a new coverage region column will create a filter checkbox but won't highlight on the map.

### Columns AC–AL — Per-Metric Target Years

Each metric (or group of related metrics) has its own target year column. The header must start with **"Target Year"** followed by a keyword:

| Header keyword in "Target Year ..." | Applies to metric(s) |
|---|---|
| `finance` | Finance Committed |
| `SDG7.1.1` | Electricity Connections |
| `SDG7.1.2` | Clean Cooking Access |
| `SDG7.2` | Renewable Capacity |
| `SDG7.3` | Energy Savings |
| `SDG8` | Green Jobs Created **and** Green Jobs Training |
| `SDG11` | Clean Transport Vehicles **and** Charging Infrastructure |
| `SDG13` | GHG Emissions Averted |
| `SDG17` | Partnerships for Goals |
| `Net Zero` | Net Zero Pledges |

---

## Filters

### Proponent Type

Multi-select dropdown with checkboxes. When one or more types are selected, only compacts belonging to **at least one** of the selected types are shown. When none are selected, all compacts are shown.

### Coverage Region

Multi-select dropdown with checkboxes. Includes five options:

- **Global** — shows only compacts marked as "yes" (Y, y, Yes, 1, true, etc.) across all four regions (Americas, Europe, Asia-Pacific, Africa)
- **Americas**, **Europe**, **Asia-Pacific**, **Africa** — shows compacts covering that region

Selecting a region highlights it on the map. Clicking a region on the map toggles the same filter. Multiple regions can be selected using OR logic (e.g., selecting "Global" + "Africa" shows compacts that are either global or in Africa).

### Origin Country

A dropdown listing all unique origin countries found in the data. When a country is selected, only compacts from that country are shown. Additionally, the country's corresponding region (Americas, Europe, Asia-Pacific, or Africa) is automatically highlighted on the map.

The list of countries is dynamic — it is discovered from the "Origin Country" column in your data file.

### Target Year

A dropdown with the following options: **All**, **≤ 2030**, **≤ 2040**, **≤ 2050**, **≤ 2060**.

This filters at the **metric level**, not the compact level:

- The compact count reflects only the proponent type and region filters.
- For each metric total, only contributions from compacts whose target year **for that specific metric** is ≤ the selected value are summed.
- "All" includes everything regardless of target year.

---

## What Is Hardcoded vs Dynamic

### Dynamic (adapts to your data)

- **Proponent types** — discovered from column headers starting with "Proponent Type". Add or remove columns freely.
- **Coverage regions (filter)** — discovered from column headers starting with "Coverage Region".
- **Origin countries** — discovered from the "Origin Country" column.
- **Compact count** — derived from the number of non-empty rows.
- **Metric values** — parsed from the data, with automatic number format handling.
- **Target years** — parsed per-metric from the data.
- **Data date** — entered by the user via the calendar picker.

### Hardcoded

- **Metric definitions** — the 12 SDG metrics (finance, electricity, clean cooking, etc.) are fixed.
- **Map regions** — the world map highlights Americas, Europe, Asia-Pacific, and Africa. New regions appear in filters but not on the map.
- **Target year dropdown options** — fixed at All, ≤ 2030, ≤ 2040, ≤ 2050, ≤ 2060.
- **Country-to-region mapping** — a built-in lookup maps countries to the four map regions for highlighting.
- **Global filter** — requires all four base regions to be marked as "yes" (using any accepted yes value).
- **Dashboard styling** — fonts (Oswald, Open Sans), color schemes, and layout are fixed.
- **Column matching keywords** — the keywords used to match column headers are fixed.

---

## Input Robustness

### One-Hot Encoding (Proponent Types & Coverage Regions)

The parser is case-insensitive and flexible. All of the following are recognized as "yes":

| Input | Recognized? |
|---|---|
| `Y` | ✓ |
| `y` | ✓ |
| `Yes` | ✓ |
| `yes` | ✓ |
| `YES` | ✓ |
| `1` | ✓ |
| `true` | ✓ |
| `TRUE` | ✓ |
| `Yes, 2050` | ✓ (first token used; see Net Zero below) |

Everything else is treated as "no" — including `0`, empty cells, `N`, `No`, or any other text.

The same logic — including the compound-form handling described in the **Net Zero Pledge** section below — now applies to the Net Zero column as well.

### Numeric Values

| Input | Parsed as |
|---|---|
| `1000000` | 1,000,000 |
| `1,000,000` | 1,000,000 |
| `1.5E+09` | 1,500,000,000 |
| _(empty)_ | 0 |
| `-` or `–` | 0 |
| `N/A` | 0 |

### Net Zero Pledge

Uses the same yes/no logic as other one-hot columns — `Y`, `y`, `Yes`, `yes`, `YES`, `1`, `true` (and `TRUE`) are all counted as 1 pledge; anything else is 0.

In addition, the Net Zero parser handles compound entries such as `"Yes, 2050"`, `"Yes - 2030"`, or `"Y, 2040"` by reading only the first token (the part before the comma, dash, or whitespace) and applying the yes-check to it. So `"Yes, 2050"` → 1 pledge, `"No, 2050"` → 0.

Note: the year (if any) in the compound form is **not currently captured** — only the Yes/No portion is parsed. The target year for Net Zero is still read from the dedicated "Target Year Net Zero" column.

---

## Export

The green "⤓ Export HTML" button downloads a standalone HTML file of whichever theme (V1 or V2) you are currently viewing. The exported file:

- Contains your data embedded directly (no CSV upload needed)
- Displays the date you selected
- Loads fonts and React from CDN
- Is a single `.html` file — no other files needed
- Can be deployed directly to any web server, CMS, or static host
- Works when opened locally by double-clicking

---

## Hosting Options

Since the exported file is a single self-contained HTML file, you can host it on:

- **Any web server** — just upload the file
- **Netlify Drop** — drag and drop at app.netlify.com/drop for an instant live URL
- **GitHub Pages** — push to a repo with Pages enabled
- **CMS** — embed via iframe or upload as a static page
- **Locally** — double-click to open in any browser

---

## Technical Notes

- **File size**: the interactive tool is approximately 130 KB; exported dashboards are smaller since they include only one theme and its dependencies.
- **Browser support**: any modern browser (Chrome, Firefox, Safari, Edge). Internet Explorer is not supported.
- **Privacy**: all data parsing happens in-browser. No data is sent to any server.
- **Libraries used**: React 18, Babel Standalone (for JSX), PapaParse (CSV parsing), SheetJS (Excel parsing), all loaded from cdnjs.cloudflare.com.
