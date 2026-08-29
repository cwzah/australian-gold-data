# Australian gold data

Machine-readable Australian gold production, refining and export statistics,
quarterly from March 1990. Companion to
<https://www.miningcapitalfunds.com.au/australian-gold-statistics>.

Compiled from the **Resources and Energy Quarterly** historical data workbook,
published by the Office of the Chief Economist, Australian Government
Department of Industry, Science and Resources, and licensed
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

Nothing here is modelled or forecast. The REQ publishes projections; none of
them appear in these files.

## Files

| File | Rows | What it holds |
|---|---|---|
| `australian-gold-quarterly.csv` | ~3,600 | Production, refining, exports, value, prices and exploration, long format |
| `australian-gold.json` | — | The full series in one object |

### `australian-gold-quarterly.csv`

One fact per row: `quarter,series,category,subcategory,value,unit`

| series | category | subcategory | unit |
|---|---|---|---|
| `mine_production` | `state` / `national` | name | t |
| `refinery_output` | `by origin` | primary/secondary × Australian/overseas, or `Total` | t |
| `exports_quantity` | `Refined and unrefined bullion` | destination or `Total` | t |
| `exports_value` | `Refined` | — | A$m |
| `imports_value` | `Refined and unrefined bullion` | — | A$m |
| `price` | `LBMA PM` / `Australia` | — | US$/oz or A$/oz |
| `exploration` | `Gold` / all metals | — | A$m |

Quarters are calendar quarters, labelled `YYYY-Qn`. `2026-Q1` is January to
March 2026.

## Four things that will trip you up

**Refinery rows stop earlier than everything else.** Refinery output ends two
quarters before production, exports and prices. Summing a fixed slice across
series will silently understate refining. Restrict both sides to the same window
before comparing.

**Export volume and export value are not the same quantity.** Volume covers
refined *and unrefined* gold and, per the department's own note, includes ash,
waste and scrap gold. Value is reported for refined gold only. Dividing value by
volume will not give you a price — use the `price` rows.

**Two different currencies.** The `LBMA PM` price is US dollars an ounce, the
`Australia` price Australian dollars an ounce. Both are reproduced as published
rather than converted, so the distance between them is mostly the exchange rate.

**The refinery origin cuts overlap.** "Overseas origin" and "secondary" are two
different ways of slicing the same total, and secondary-overseas gold sits in
both. Do not add them.

## Coverage

Unlike the coal and copper datasets, the geography here is complete: all seven
producing states and territories are published separately, the Northern
Territory and Victoria included. They sum to the national total in all but 23 of
145 quarters, where state and national figures were revised out of step; the
largest such gap is 4.59 t.

There is no mine-level detail. The REQ reports to state level, and no Australian
state publishes gold production mine by mine as open data.

Destinations do not sum to the export total. The department names only the major
buyers and withholds some country detail as confidential.

Exploration is private expenditure only.

## Related

- Copper: <https://github.com/cwzah/australian-copper-data>
- Queensland coal, mine by mine: <https://github.com/cwzah/qld-coal-data>

## Updates

Rebuilt after each quarterly REQ edition, roughly March, June, September and
December. File names do not change, so the raw URLs are stable.

## Attribution

Compiled by Clint Zahmel, Mining Capital Funds. Source data © Commonwealth of
Australia, used under CC BY 4.0. Underlying sources named by the department:
ABS International Trade in Goods and Services (cat. no. 5368.0); London Bullion
Market Association; Perth Mint. Conclusions drawn from this data are not
attributable to the department.
