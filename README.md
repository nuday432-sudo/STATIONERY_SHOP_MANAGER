# Stationery Shop Manager (Prototype)

Menu-driven Python app to manage **stationery stock, sales and reorder levels**.
Built for *Campus Catalyst - Project #88*. Pure standard library, Python 3.10+, no installs needed.

## Run it
```bash
cd stationery_shop_manager
python main.py          # use python3 on macOS/Linux
```
First launch offers to load a demo dataset (42 products + 2 weeks of sales).

## Run the tests
```bash
python -m unittest discover -s tests
```

## Features
| Brief requirement | Where |
|---|---|
| Interactive terminal menu | `main.py` (12 options, ANSI colours, paginated tables) |
| Defensive input validation | `stationery/validation.py` - SKU regex, price/qty ranges, category whitelist, loop-until-valid `ask()` |
| Core logic (stock, sales, reorder) | `stationery/inventory.py` - sell, restock, edit levels, OK/LOW/OUT status |
| JSON persistence | `stationery/storage.py` - atomic saves, missing/corrupt file recovery (corrupt file is backed up) |
| Search / filter | menu option 5 - keyword (name or SKU) + category |
| Executive summary | menu option 7 - totals, averages, category breakdown, top sellers, 7-day revenue trend |
| Multi-format export | option 8 - Markdown, plain text, CSV + audit log copy -> `exports/` |
| Threshold warnings | startup banner, option 6, and the dashboard alerts (CRITICAL / WARNING / NOTICE) |
| Bulk CSV import | option 9 - row-by-row validation, error log in `exports/` |
| Sample data (30-50 rows) | `data/sample_products.csv/.json` (42 products incl. out-of-stock, boundary and overstock cases) and `data/legacy_import_sample.csv` (deliberately bad rows) |

## 5-minute demo script
1. Launch -> branded banner, load demo data, see alert banner.
2. **Add product** -> type a bad SKU, a negative price, letters for stock; watch each get rejected, then enter valid values.
3. **Record a sale** -> try selling more than is in stock (blocked), then a valid sale.
4. **Summary dashboard** (7) -> metrics, top sellers, trend, alerts.
5. Exit (0), relaunch -> data is still there (persistence).
6. **Import CSV** (9) with the default messy file -> 3 rows imported, 7 rejected with reasons.
7. **Export reports** (8) -> open the generated files in `exports/`.

## Project layout
```
main.py                 menu + handlers
stationery/             validation, models, inventory (logic), storage, importer, reports, ui, seed
data/                   sample datasets (shop_data.json and audit.log are created at runtime)
exports/                generated reports and import error logs
tests/test_core.py      19 unit tests
```

## Ideas to extend
Tkinter/Textual front-end, Matplotlib sales charts, pandas-based analytics, discounts/GST, supplier list, barcode lookup.
