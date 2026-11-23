# Wicko gold strategy tests: open data

Results from testing 16 well-known trading strategies on gold (XAUUSD), with trading costs
included. Each strategy was tested in its textbook form and in 196 variations in total, where one
rule at a time was changed. These are the same numbers shown on https://wicko.ai/strategies/.

Tested period: 1 July 2021 to 18 November 2026. Numbers last updated 22 November 2026.

This package holds results only. It has no trade prices and no candle data.

## The strategies

| strategy_id | Name | Trades | Average result after costs |
|---|---|---|---|
| `200-ema-bounce` | 200 EMA bounce (textbook) | 2,376 | -0.567R |
| `asian-range-breakout` | Asian range breakout | 1,091 | +0.022R |
| `bollinger-band-bounce` | Bollinger band bounce (textbook) | 21,967 | -0.536R |
| `break-and-retest` | Break and retest (textbook) | 11,011 | -0.519R |
| `engulfing-candle` | Engulfing candle (textbook) | 33,316 | -0.215R |
| `fvg-textbook` | Fair value gap (textbook) | 66,676 | -0.215R |
| `fibonacci-retracement` | Fibonacci retracement 61.8% (textbook) | 16,478 | -0.170R |
| `ichimoku-cloud` | Ichimoku cloud breakout (textbook) | 9,601 | -0.250R |
| `ict-silver-bullet` | ICT silver bullet (textbook) | 274 | +0.067R |
| `inside-bar-breakout` | Inside bar breakout | 37,198 | -0.128R |
| `liquidity-sweep` | Liquidity sweep (textbook) | 552 | -0.440R |
| `london-breakout` | London breakout | 895 | -0.037R |
| `macd-crossover` | MACD crossover (textbook) | 30,414 | -0.109R |
| `order-block` | Order block (textbook) | 18,818 | -0.275R |
| `rsi-divergence` | RSI divergence (textbook) | 3,552 | -0.096R |
| `supertrend` | Supertrend flip (textbook) | 9,902 | -0.066R |

## Key words

- **R**: the result of a trade as a multiple of the amount risked. If you risk $100 and the trade
  hits its stop, that is -1R (you lose $100). If it hits a target set at 2 times the risk, that
  is +2R (you make $200). An average of -0.05R means you lose, on average, 5% of what you risk on
  each trade.
- **Before costs**: the result if trading were free. No real account trades like this, so treat it
  as the raw edge of the setup, not what you would keep.
- **After costs**: the result after commission, slippage and the spread. See "How costs were
  charged" below.
- **Hit rate**: the share of trades that reached their target (0.31 means 31%).
- **Session**: the part of the trading day when the entry order filled, by UTC clock time.

## Files and columns

All files are plain CSV (comma separated, first line is the header). Shares and rates are
fractions between 0 and 1. An empty cell means "no value" (for example, no trades in that
session). `strategy_id` links every file together.

### strategies.csv (16 rows, one per strategy, textbook rules)

| Column | Meaning |
|---|---|
| strategy_id | Short id for the strategy |
| slug | The last part of the strategy's web address |
| name | Strategy name |
| instrument | Always XAUUSD (spot gold priced in US dollars) |
| timeframe | Candle size the rules read, for example 5m = 5-minute candles |
| order | How the entry was placed: market, stop or limit (see "How trades were filled") |
| date_from, date_to | First and last moment of data tested (UTC) |
| numbers_updated | When these numbers were produced (UTC) |
| cost_profile | Which cost settings were used (see "How costs were charged") |
| trades | Number of trades |
| hit_rate | Share of trades that reached the target |
| avg_r_before_costs | Average result per trade in R, before costs |
| avg_r_after_costs | Average result per trade in R, after costs |
| median_stop_usd | The middle value of the distance from entry to stop, in US dollars per ounce. Tight stops make costs weigh more in R |
| timeout_share | Share of trades closed by the time limit, not by the stop or target |
| longs, shorts | Number of buy trades and sell trades |
| min_trades | Smallest number of trades a result needs before it is shown on the website |
| publishable | true if the result met that minimum |
| variations_tested | How many variations are in variations.csv for this strategy |
| sources | Public web pages the textbook rules came from, separated by " \| " |
| page_url | The strategy's page on wicko.ai |

### variations.csv (196 rows, one per variation)

| Column | Meaning |
|---|---|
| strategy_id | Which strategy this varies |
| variation_id | Short id for the variation |
| label | What changed, in plain words |
| changed | The setting that changed and its new value, as JSON text. Settings ending in `_atr` are fractions of the typical daily move; `timeframe_minutes` is the candle size; `target_r` is the target as a multiple of the risk |
| trades, hit_rate, avg_r_before_costs, avg_r_after_costs | Same meaning as in strategies.csv, for this variation over the full period |
| publishable | true if the variation met the minimum number of trades |

### months.csv (96 rows, the most recent months for each strategy)

| Column | Meaning |
|---|---|
| strategy_id | Which strategy |
| month | Calendar month, YYYY-MM (UTC) |
| partial_to | If the month was not over when the numbers were made, the last day included. Empty for a full month |
| trades, hit_rate, avg_r_before_costs, avg_r_after_costs | Results for trades in that month, textbook rules |

### sessions.csv (64 rows, four sessions per strategy)

| Column | Meaning |
|---|---|
| strategy_id | Which strategy |
| session | asia, london, new_york or off_hours |
| session_hours | The UTC hours that session covers |
| trades, hit_rate, avg_r_before_costs, avg_r_after_costs | Results for trades whose entry filled in that session. Empty when there were no trades (some strategies only trade in one session by design) |

### periods.csv (424 rows, the two-period check)

| Column | Meaning |
|---|---|
| strategy_id | Which strategy |
| variation_id | `base` for the textbook rules, otherwise the id from variations.csv |
| variation_label | "Textbook rules" or the variation's label |
| period | `tuned_2021_2024` or `check_2025_2026` |
| period_years | The same in plain words |
| trades, hit_rate, avg_r_before_costs, avg_r_after_costs | Results for that period only |

### rules.md

Each strategy's rules and the list of variations, in plain words, with the public sources.

## How trades were tested

- **Price data**: 1-minute gold candles from an institutional price feed. Weekends and gaps in the data never
  count as part of a setup.
- **Rules**: each strategy is a textbook version written from public definitions (listed in
  `sources` and in rules.md). No private or paid rules were used.
- **How trades were filled**:
  - `market`: the entry is a market order at the open of the next minute after the setup forms.
  - `stop`: the entry is a stop order that waits beyond a price level and counts as filled the
    first minute price touches it.
  - `limit`: the entry is a limit order that counts as filled the first minute price touches it.
- **Exits**: checked minute by minute. If one minute touches both the stop and the target, the
  trade counts as a loss at the stop, because 1-minute candles cannot show which came first. This
  makes results slightly worse, not better. Trades still open at the strategy's time limit are
  closed at market.
- **Checks**: 20 random trades were re-counted with separately written code and matched. Every
  number comes from one checked results file per strategy.

## How costs were charged

The cost profile `raw_gold_broker` models a raw-spread gold account, where the broker charges a
commission and the spread is close to zero:

- Commission of 0.004% of the trade's value on each side (entry and exit).
- Slippage of 0.002% of the trade's value on each side, which stands for crossing the spread and
  getting a slightly worse price than expected.
- The entry and exits by stop or time limit pay both. An exit at the target is a resting limit
  order, so it pays the commission only.

Costs are a percentage of the gold price, so they turn into a bigger share of R when the stop is
tight. That is why `median_stop_usd` is included: it shows how much the costs bite.

## The two-period check

To see whether a result could be luck, the data is split in two: 2021 to 2024
(`tuned_2021_2024`) and 2025 to 2026 (`check_2025_2026`). If both periods point the same way
(both positive or both negative after costs), the overall result is not driven by one unusual
stretch. If they disagree, treat the overall number with care. On the website, a strategy whose
overall result after costs is positive but where one period is negative is labelled "unproven".

Every variation tested is listed, not only the best one. When many variations are tested, the
best one is partly lucky. Look at whether
it holds in both periods before trusting it.

## Known limits

- Past results on historical data. They do not promise future results and are not advice.
- One instrument (gold) and one cost profile. Other brokers, other spreads, or a different market
  will give different numbers.
- Taxes and overnight funding (swap) costs are not included.
- The spread is not modelled minute by minute. It is covered by the fixed slippage figure, which
  can be too low in fast markets and around news.
- Fills assume a touch is enough: a limit or stop order counts as filled the first minute price
  reaches its level, regardless of how much size was available there.
- 1-minute candles hide the order of moves inside a minute. Ties go to the stop, which is
  cautious but still an assumption.
- Textbook versions are one reading of each strategy. A trader who applies the same idea with
  judgement may get different results.
- `months.csv` covers only the most recent months, and the latest month may be partial
  (`partial_to`).
- Numbers change slightly when the data is refreshed. Cite the `numbers_updated` date.

## How to cite

> Wicko strategy lab. "Wicko gold strategy tests: open data." Numbers updated 22 November 2026.
> https://wicko.ai/strategies/

When you quote one strategy, link its page (the `page_url` column) and give the date above.

## Licence

The data in this repository is licensed under Creative Commons Attribution 4.0 International
(CC BY 4.0), full text in [LICENSE](LICENSE). You may copy, share and adapt it, including for
commercial use, as long as you credit "Wicko strategy lab" and link https://wicko.ai/strategies/.

## Rebuilding

The files are generated from Wicko's strategy results by a build script that also re-reads every
CSV and checks each value against the source. Do not edit the CSVs by hand.
