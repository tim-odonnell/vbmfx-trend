# vbmfx-trend

Daily report: is **VBMFX** (Vanguard Total Bond Market Index Fund Investor Shares, the first bond index fund for
ordinary investors, started 1986-12-11) **above or below its trend** over 1 month, 3 and 6 months, 1, 5, 10, 20 and
30 years and over its whole history, and what NAV the **next trading day** would need to be exactly on each trend.

- Data: Yahoo Finance `VBMFX`, the full daily history from the fund's first day. Each run downloads all of it and saves
  it as `~/VBMFX-Reports/data/vbmfx-daily.csv` (`date,close,adjclose`), used by the report when a download fails (the
  report then says so). Today's bar is ignored until 18:00 New York time (NAV not out yet).
- Trend: least-squares line through the **log** of the dividend-adjusted closes in each window (= exponential trend,
  monthly interest dividends reinvested), shown in today's NAV dollars and extended to the next trading day. Most of a
  bond fund's return is that interest - the raw NAV has stayed near $10 since 1986 - so adjusted prices are essential.
  R² shows how well prices followed the line. Bond trends bend with interest rates (2022 was the worst year on record).
- Chart: under the dots and bars, the last 5 years of price with every trend line drawn faintly behind it
  (`bin/trend_overlay.py`, written by a local Gemma E2B in 9 guided steps, see ~/e2b-abilities task 6b), plus the
  amber all-history trend, refitted every night. On phones it opens at today; swipe for earlier years.
- Output: `~/VBMFX-Reports/<last close date>.html` + `.md`, `latest.html`; desktop pop-up with "Open report".
  Takes ~2 s; no AI model involved. Part of the combined page timodonnell.info/daily (daily-pages).

| Command / icon | What it does |
|---|---|
| `vbmfx-run-now` / **VBMFX Report - Run Now** | make the report now |
| `vbmfx-mode nightly` / **VBMFX Report - Nightly Auto** | run automatically Mon-Fri 02:14 (a missed run is made at next boot) |
| `vbmfx-mode manual` / **VBMFX Report - Manual Mode** | no automatic runs (the default after install) |
| `vbmfx-mode status` | mode, next run, last run, newest report |
| `vbmfx-trend --json FILE --now 2026-11-20T07:00 --out DIR` | offline test run |

Install: `./install.sh`. Trend lines are fitted to past prices; they are not a forecast and not financial advice.
Copied from vfinx-trend (2026-11-20).
