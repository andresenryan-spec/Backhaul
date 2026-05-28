# Clayton Connect — Backhaul Matcher

A browser-based tool that identifies backhaul opportunities and loop plans from outbound shipment data to reduce empty miles.

## Using the Tool

Visit the live tool at: `https://<your-org>.github.io/<repo-name>`

No installation required — runs entirely in your browser.

## How It Works

1. Download the Excel template from the tool's upload screen
2. Fill in your outbound shipments (Shipment #, Production Date, Ship Date, Origin, Destination, Equipment)
3. Upload the file to the tool
4. Set your matching parameters and click **Find Backhauls**

Results are grouped into three planning tiers:
- 🔁 **Loops** — truck ends within 150 miles of origin; schedule first
- ↩ **Backhauls** — truck moves closer to origin; schedule second  
- ⬡ **Traditional Moves** — no pairing found; deadhead home

## Updating the Tool

All updates are made in this repository. Users get the latest version automatically on their next page load — nothing to redistribute.

### Files

| File | Purpose |
|------|---------|
| `index.html` | The matching tool — all logic runs in the browser |
| `Backhaul_Template.xlsx` | Upload template — update this when columns change |

### Making Changes

1. Edit `index.html` or `Backhaul_Template.xlsx` locally (or directly in GitHub)
2. Commit and push to the `main` branch
3. GitHub Pages deploys automatically within ~60 seconds
4. All users see the update on next page refresh

## Deployment (GitHub Pages Setup)

1. Go to **Settings → Pages** in this repository
2. Set Source to **Deploy from a branch**
3. Select branch: `main`, folder: `/ (root)`
4. Click Save — your URL will appear at the top of the Pages settings

## Geocoding

The tool resolves city coordinates from a built-in database of 1,100+ US cities. Cities not in the database are looked up automatically via the OpenStreetMap Nominatim API (requires internet access). Any cities that still can't be resolved appear in the **Unresolved Cities** tab after running the matcher — export that list to expand the database.

## Parameters Quick Reference

| Parameter | Default | Purpose |
|-----------|---------|---------|
| Yard Hold Window | 2 days | Days home can sit on yard before shipping |
| Max Deadhead Miles | 150 | Max empty miles from delivery to backhaul pickup |
| Return-to-Origin Radius | 250 | Max miles from backhaul destination to outbound origin |
| Max Days Between Loads | 5 | Max calendar days between outbound delivery and backhaul ship date |
| Min Origin Separation | 50 | Backhaul pickup must be this far from origin plant (prevents same-plant loops) |
| Net Displacement | Yes | Backhaul must bring truck closer to origin than outbound leg did |
| Min Backhaul Length | 0 | Filter out short regional hops |
| Max Backhaul Length | 9,999 | Filter out very long hauls |
