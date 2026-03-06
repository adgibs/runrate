# Memory

## Me
Andrew (adgibs14@gmail.com). Building RunRate, a 3-year car cost of ownership comparison tool for the UK market.

## Project
| Name | What |
|------|------|
| **RunRate** | Single-file HTML car cost calculator. ~2500 lines. Hosted at adgibs.github.io/runrate |

## Key Files
| File | Purpose |
|------|---------|
| `outputs/car-cost-calculator.html` | Main working file — all CSS, HTML, JS in one file |
| `outputs/index.html` | GitHub Pages copy — always sync after changes with `cp` |

## GitHub
- Repo: `adgibs/runrate` on GitHub
- Live: https://adgibs.github.io/runrate
- Claude can't push — Andrew runs git commands locally
- Push command: `cd "/Users/andrew/0. Swift Coding/carpicker" && git add -A && git commit -m "message" && git push`

## Architecture
- Single HTML file, no build step, no frameworks
- Embedded `<style>` and `<script>` blocks
- ~56 pre-loaded UK cars in a `cars` array
- localStorage persistence via `saveState()`/`loadState()` with key `carCostCalc`
- Canvas-based charts (stacked bars, scatter, timeline)
- Name-based storage for star ratings, price overrides (not index-based — indices shift on delete)

## Key Features Built
- Sortable/filterable table + card view + comparison mode (max 4)
- 1-3 star rating system with per-level filters
- Salary sacrifice support with 3 yearly rental rates (yr1/yr2/yr3)
- PHEV as distinct fuel type, UK VED 2025/26 bands
- Additional costs: tyres, breakdown, congestion, MOT
- Price override per car, inline editing
- Export/import JSON backup, reset button
- Colour-coded cost cells (green→red gradient)
- Three canvas charts with high-DPI support

## Technical Patterns
- `_origIdx` on car objects for stable index references through sort/filter
- `effectiveCost()` / `effectiveMonthly()` for unified sal sac vs standard comparison
- `costColor(value, min, max)` returns CSS class; `totalColorStyle()` returns inline RGB
- Scatter chart splits electric (mi/kWh) vs ICE (MPG) into two zones
- Label collision detection via `canPlace()` in scatter and timeline charts
- `DEFAULT_CARS` deep clone for detecting user edits to built-in cars

## Preferences
- Andrew sends screenshots for visual feedback — this works well
- Iterate quickly, validate JS syntax after each edit, sync index.html
- Keep everything in one file unless it gets unmanageable
→ Details: memory/projects/runrate.md
