# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Kids height tracker — a French-language PWA ("Suivi de Taille") that plots children's growth curves against WHO percentile reference data (P3/P15/P50/P85/P97, ages 0–18). Data is persisted in `localStorage` and can be exported/imported as JSON or CSV.

## Architecture

The app is a single self-contained HTML file (`index.html`) with inline CSS and vanilla JS. Uses Chart.js 4.4.1 (loaded from CDN) for rendering growth charts. It's a PWA with a service worker (`sw.js`) and web app manifest (`manifest.json`).

UI has 4 tabs: Courbes (chart), Mesurer (add measurement), Enfants (manage children), Données (export/import).

## Data Model

Each child: `{ id, name, gender ("boy"|"girl"), birthDate (ISO string), color, measurements: [{ id, date, height }] }`.

The `data/` directory contains sample CSV exports and a JSON import file.

## Development

No build system, package manager, or test framework. To run locally, serve the directory with any static file server:

```
python3 -m http.server 8000
```

The service worker caches assets aggressively — bump the `CACHE` version string in `sw.js` when deploying changes to `index.html`.

## Key Constraints

- The app UI is entirely in French
- Maximum 4 children per tracker
- Height measurements must be between 30–220 cm
- WHO data covers ages 0–18 years with percentiles P3, P15, P50, P85, P97
