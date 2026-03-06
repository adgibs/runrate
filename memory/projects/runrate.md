# RunRate

**Live URL:** https://adgibs.github.io/runrate
**Repo:** github.com/adgibs/runrate
**Tech:** Single HTML file (~2500 lines), vanilla JS, Canvas charts, localStorage

## Car Data Model
```javascript
{
  name, make, fuel, body, price, efficiency, co2,
  annualService, depreciationPct, annualInsurance,
  salSac?: { yr1, yr2, yr3, netMonthly }
}
```
- `fuel`: "electric" | "petrol" | "diesel" | "phev"
- `body`: "saloon" | "suv" | "estate" | "hatchback" | "coupe"
- `efficiency`: mi/kWh for electric, MPG for others
- `salSac`: salary sacrifice cars have 3 yearly rental rates

## Cost Calculation (calcCarCosts)
- Depreciation: `price * depreciationPct / 100` over 3 years
- VED: UK 2025/26 bands based on CO2 (electric £0 yr1, then £195; ICE varies by CO2)
- Fuel: electric = `(miles / efficiency) * electricityPrice`; ICE = `(miles / efficiency) * 4.546 * fuelPrice`
- Tyres: mileage-based with price tier multiplier, electric +20% wear
- Insurance, service, breakdown, MOT, congestion: annual × 3
- Sal sac total: `yr1×12 + yr2×12 + yr3×12 + fuelCost`

## Persistence (localStorage key: 'carCostCalc')
Stores: userCars, editedBuiltins, deletedBuiltins, priceOverridesByName, starRatings, settings, sort, fuelFilter, minStarFilter

## Key Bugs Fixed
- Favourites stored by index shifted on car deletion → switched to name-based
- Auto-favourite used `cars.length - 1` index → switched to `car.name`
- Chart labels overlapping → collision detection + zone splitting

## Chart Details
1. **Stacked bars**: Horizontal bars, colour-coded cost segments, smart name truncation
2. **Scatter**: Split electric/ICE zones, "Best value zone" label, collision detection for labels
3. **Timeline**: Cumulative 36-month cost lines, per-year sal sac rates, label collision detection

## Evolution History
1. Basic table with sorting/filtering
2. Added modal details, PHEV support, extra cost categories
3. Salary sacrifice comparison with 3 yearly rates
4. localStorage persistence + export/import
5. Star ratings (1-3) replacing simple favourites
6. Card view + comparison mode
7. Colour-coded cost cells
8. Canvas charts (stacked, scatter, timeline)
9. Chart readability fixes (current)
