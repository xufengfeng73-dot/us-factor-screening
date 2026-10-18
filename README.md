# US Large-Cap Factor Screening

**One-liner:** A reproducible quant screen that scores 25 US large-cap stocks on momentum and quality factors using free public market data, and ranks them by a composite z-score.

## What's inside

- `factor_screening.ipynb` — the full analysis notebook. Loads the cached price
  data, computes both factors, z-scores them, and outputs the ranking.
  Re-running it top-to-bottom reproduces `results.md` exactly.
- `results.md` — the ranked results page (25 stocks, composite score +
  factor breakdown).
- `data/raw_prices.csv` — cached daily closes (Yahoo Finance, 2025-10-01 →
  2026-10-16) so the notebook is fully reproducible without re-downloading.
- `data/ranking.csv` — machine-readable ranking produced by the notebook.

## Data source

Yahoo Finance daily closing prices (free, public, no key required), accessed
via the public chart API. Ticker universe: 25 generic US large caps
(AAPL, MSFT, NVDA, AMZN, META, GOOGL, TSLA, BRK-B, JPM, V, MA, XOM, UNH, JNJ,
WMT, PG, ORCL, COST, NFLX, AMD, CRM, ABBV, LLY, AVGO, DIS).

## Method

1. **Momentum:** 6-month trailing return
   (`Close_t / Close_{t−126} − 1`).
2. **Quality (proxy):** inverse of 60-day annualized realized volatility.
   True quality factors need fundamental data; this is a documented,
   price-only stand-in.
3. **Composite:** z-score each factor across the universe, average 50/50,
   rank descending.

## Re-run it

```bash
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute factor_screening.ipynb --inplace
```

The ranking in `results.md` will match `data/ranking.csv` exactly.

## Disclaimer

Educational data-analysis project. Not investment advice; no brokerage
account, holdings, or trading activity are involved.
