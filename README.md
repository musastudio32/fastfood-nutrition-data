# Fast Food Nutrition Data

Machine-readable nutrition data for **7 major US restaurant chains** — 181 menu items and build-your-own ingredients, with calories, protein, carbs and fat.

Every value is transcribed from the chain's **own officially published nutrition information** and verified item-by-item. Last verified: **July 2026**.

| Chain | Items |
|---|---|
| Chipotle Mexican Grill | 24 |
| Panda Express | 34 |
| Starbucks | 19 |
| Subway | 28 |
| Taco Bell | 22 |
| Chick-fil-A | 29 |
| Wendy's | 25 |

## Files

| File | Format |
|---|---|
| [`nutrition.csv`](nutrition.csv) | Flat CSV — one row per item |
| [`nutrition.json`](nutrition.json) | Grouped by chain |

## Schema

```
chain      — restaurant name
category   — Proteins, Sides, Sauces, Drinks, etc.
item       — menu item or ingredient name
calories   — kcal per standard serving
protein_g  — grams
carbs_g    — grams
fat_g      — grams
```

## Quick start

```python
import pandas as pd
df = pd.read_csv("nutrition.csv")

# highest protein per calorie
df["protein_per_100cal"] = df.protein_g / df.calories * 100
print(df.nlargest(10, "protein_per_100cal")[["chain", "item", "calories", "protein_g"]])
```

```javascript
const data = require("./nutrition.json");
const chipotle = data.chains["Chipotle Mexican Grill"];
```

## Why this exists

Restaurant nutrition data is published as **PDFs and interactive widgets**, not as anything a program can read. Anyone building a meal tracker, a diet app, or a research project ends up re-transcribing the same numbers by hand — and transcription errors are common. Several nutrition datasets floating around contain items that were discontinued years ago, or that never existed on the US menu at all.

This repo is the cleaned, verified version of the data behind [ChainCalories](https://chaincalories.com), a set of free restaurant nutrition calculators.

## Notes and caveats

- **Standard portions only.** Real in-store portions vary; scooped items (rice, beans, salsas) vary the most.
- **Per-serving values.** For build-your-own chains (Chipotle, Subway) each row is a single ingredient portion, so a full order is the sum of its rows.
- **Subway values are per 6-inch.** A footlong is exactly double, per Subway's published methodology.
- **Starbucks values are for a Grande** with the drink's standard milk.
- **Limited-time items** are included when currently on the menu and may be removed later.
- **US menus only.** Regional and international menus differ significantly.
- Data is provided as-is for informational purposes. Not medical or dietary advice.

## Contributing

Found a wrong number? Please open an issue with the chain, item, and a link to the official source. Data corrections are the most valuable contribution here.

## License

Data: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — free to use with attribution to [ChainCalories](https://chaincalories.com).

Nutrition values are factual data published by the respective restaurant chains. All trademarks belong to their respective owners. This project is independent and not affiliated with, endorsed by, or sponsored by any restaurant brand.
