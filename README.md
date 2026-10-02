# Tadawul Firm Ranking Dashboard — Quality & Resilience Screen

**Live dashboard:** https://salemsharyah.github.io/tadawul-firm-ranking/

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/salemsharyah/tadawul-firm-ranking/blob/main/Capstone_Group13.ipynb)

Financial Analytics capstone · Group 13

Every Tadawul-listed firm is scored and ranked **within every fiscal year (2006–2025)** on a weighted set of financial ratios, with each firm compared against **its own sector**. The website lets anyone change the ratio weights, the comparison group and the quality gates, and the whole ranking recomputes in the browser.

## What the screen looks for

A good firm earns well **and** can keep earning through a downturn:

| Question | Ratio | Default weight |
|---|---|---|
| Does it make money? | ROA (net income / total assets) | 20 % |
| | Net margin (net income / revenue) | 20 % |
| Is it growing? | Revenue growth, year over year per firm | 25 % |
| Can it survive a bad year? | Debt / assets (lower is better) | 20 % |
| | Operating cash flow / assets | 15 % |

Two **quality gates** screen out firms with negative equity, and firms whose net profit came with an operating loss (a profit from one-off items).

## How the score works

1. Each ratio is winsorized at the 1st/99th percentile within each year.
2. z-score = (x − mean) / std among firms in the **same sector and year** (small sectors use the whole market). Debt is sign-flipped so higher is always better; z is capped at ±3.
3. Quality score = weighted sum of z-scores. A missing ratio counts as sector average; a firm needs ratios worth at least 50 % of the weight to be ranked.
4. Firms are ranked 1…N inside every fiscal year, with a percentile.

## Files

| File | What it is |
|---|---|
| `index.html` | The web dashboard. Never needs editing. |
| `dashboard_data.json` | Ratios and z-scores for every firm-year, exported from the notebook. |
| `Capstone_Group13.ipynb` | The full analysis in Google Colab: settings, ranking engine, checks, dashboard, insights, export. |
| `tadawul_merged.csv` | Source data (Tadawul-listed company financials, FY2006–FY2026). |

## Updating the dashboard

1. Open the notebook in Colab, upload `tadawul_merged.csv`, and change `WEIGHTS` (or add a ratio to `RATIO_MENU`) in the Settings cell.
2. **Runtime → Run all.** The last section downloads a new `dashboard_data.json`.
3. In this repository: **Add file → Upload files**, drop in the new `dashboard_data.json`, **Commit changes**. The website updates within about a minute.

A new ratio added in the notebook appears on the website as its own slider automatically.
