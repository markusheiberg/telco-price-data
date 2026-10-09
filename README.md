# Nordic telecom price data

Daily-refreshed prices and campaigns for Nordic mobile and broadband plans
(Norway, Sweden, Denmark, Finland), scraped from the operators' public websites.
Maintained by [telco-price-monitor](https://github.com/markusheiberg/telco-price-monitor);
this repo only receives the generated files and is overwritten daily.

| File | What it is |
|---|---|
| `latest_prices.csv` | One row per plan in the most recent snapshot — the market as it stands |
| `price_changes.csv` | Change log: one row per changed field per run (base-price moves, campaigns, plan additions/removals) |
| `backfill_no_mobile.csv` | Norway consumer-mobile history Jan 2025 – May 2026, reconstructed from Internet Archive captures (`archive_url` links each row to its capture) |
| `manifest.json` | When this data was published |

## Reading the data

- **Currency**: every file has a `currency` column (NOK / SEK / DKK / EUR). Prices are as shown on
  the operator's site; never aggregate across currencies without converting.
- **`monthly_price`** is the regular list price. **`campaign_price`** (with `campaign_months`) is a
  time-limited offer price when one was visible; empty means no campaign.
- **`vat_included`**: consumer prices include VAT; business prices are ex-VAT.
- **`price_changes.csv`**: filter `is_campaign=no` for genuine base-price and lineup moves; `yes` is
  promo churn. `kind` is `added`, `removed`, `modified` or `replaced`.
- **`scraped_at`** older than the newest run in `latest_prices.csv` means that operator's scrape failed
  and the row was carried forward — the price may be stale.
- Coverage of the Norway backfill is uneven: Telia Jun 2025 →, Telenor list prices only (~8 captures),
  ice ~2/month, OneCall 2026 only, Talkmore none.

Prices are collected automatically from public pages and may lag or misread an operator's site.
Check the operator before relying on a figure.
