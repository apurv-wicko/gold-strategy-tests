# The rules we tested

Each strategy is a textbook version written from public sources. Below are its rules, then every variation tested. A variation changes one rule and keeps everything else the same. Numbers for each one are in `strategies.csv` and `variations.csv`.

## 200 EMA bounce (textbook)

Strategy id: `200-ema-bounce`. Gold (XAUUSD), 5m candles. Entry: market order at the open of the next minute after the setup forms. Full page: https://wicko.ai/strategies/200-ema-bounce/

On 5-minute candles, the 200 EMA is rising and the last 10 candles stayed above it. A candle dips to the line and closes back above it: buy at the next open. Stop at that candle's low, target 2x the risk, closed after 4 hours if neither is hit. Shorts are the mirror image.

Public sources for the rules:

- https://therighttrader.com/learn/indicator-strategies/200-ema
- https://beatmarket.com/blog/?p=2082

Variations tested:

- `target-1r`: Target 1x risk
- `target-3r`: Target 3x risk
- `min-stop-5atr`: Skip touches with a stop under 5% of the typical daily move
- `min-stop-10atr`: Skip touches with a stop under 10% of the typical daily move
- `trend-1h-200ema`: Only trade with the 1-hour 200 EMA trend
- `tf-1m`: 1-minute candles
- `tf-15m`: 15-minute candles
- `tf-1h`: 1-hour candles
- `ema-50`: 50 EMA instead of 200
- `confirm-candle`: Touch candle must close in the trade's direction
- `stop-buffer-10atr`: Stop 10% of the typical daily move beyond the touch candle
- `trend-20`: 20 candles clear of the line before the touch, not 10

## Asian range breakout

Strategy id: `asian-range-breakout`. Gold (XAUUSD), 5m candles. Entry: stop order that waits beyond a price level and fills the first minute price touches it. Full page: https://wicko.ai/strategies/asian-range-breakout/

Mark the high and low from 00:00 to 08:00 UTC (the Asian range). At 08:00 UTC place a buy stop $0.50 above the high and a sell stop $0.50 below the low. The first one price touches is the trade and the other is cancelled; if neither is touched by 13:00 UTC, both are cancelled. One trade a day. Stop at the other side of the range. Target 2x the risk. Closed after 4 hours if neither is hit.

Public sources for the rules:

- https://fxnx.com/en/blog/master-asian-session-breakout-ultimate-set-forget-strategy
- https://newyorkcityservers.com/blog/asian-session-forex-strategy
- https://www.mql5.com/en/articles/17239
- https://fxnx.com/en/blog/asian-range-breakout-set-forget-strategy

Variations tested:

- `target-1r`: Target 1x risk (about one range width)
- `target-3r`: Target 3x risk
- `min-stop-5atr`: Skip setups with a stop under 5% of the typical daily move
- `min-stop-10atr`: Skip setups with a stop under 10% of the typical daily move
- `trend-1h-200ema`: Only place the order on the side of the 1-hour 200 EMA trend
- `stop-mid`: Stop at the middle of the Asian range
- `buffer-0`: Orders exactly at the range high and low (no buffer)
- `buffer-10pips`: Orders $1 (10 pips) beyond the range
- `range-00-07`: Asian range 00:00 to 07:00 UTC
- `range-23-03`: Asian range 23:00 to 03:00 UTC
- `tf-1m`: 1-minute candles (48-minute time limit)
- `tf-15m`: 15-minute candles (12-hour time limit)

## Bollinger band bounce (textbook)

Strategy id: `bollinger-band-bounce`. Gold (XAUUSD), 5m candles. Entry: market order at the open of the next minute after the setup forms. Full page: https://wicko.ai/strategies/bollinger-band-bounce/

On 5-minute candles with 20-period, 2 standard deviation Bollinger bands, a candle closes below the lower band and the next candle closes back inside it, still below the middle band: buy at the next open. Stop at the outside candle's low, target 2x the risk, closed after 4 hours if neither is hit. Shorts are the mirror image at the upper band.

Public sources for the rules:

- https://therighttrader.com/learn/indicator-strategies/bollinger-band-bounce
- https://therighttrader.com/learn/trading-strategies/bollinger-band-reversion
- https://crosstrade.io/learn/trading-strategies/bollinger-mean-reversion

Variations tested:

- `target-1r`: Target 1x risk
- `target-3r`: Target 3x risk
- `min-stop-5atr`: Skip bounces with a stop under 5% of the typical daily move
- `min-stop-10atr`: Skip bounces with a stop under 10% of the typical daily move
- `trend-1h-200ema`: Only trade with the 1-hour 200 EMA trend
- `tf-1m`: 1-minute candles
- `tf-15m`: 15-minute candles
- `tf-1h`: 1-hour candles
- `touch-entry`: Trade a wick through the band that closes back inside (one candle)
- `std-2.5`: Bands at 2.5 standard deviations instead of 2
- `confirm-candle`: Back-inside candle must close in the trade's direction
- `stop-buffer-10atr`: Stop 10% of the typical daily move beyond the outside candle
- `time-limit-8`: Close after 8 candles (40 minutes) instead of 48

## Break and retest (textbook)

Strategy id: `break-and-retest`. Gold (XAUUSD), 5m candles. Entry: market order at the open of the next minute after the setup forms. Full page: https://wicko.ai/strategies/break-and-retest/

A 5-minute candle closes beyond the latest swing high or low (3 candles each side). Within the next hour price comes back, touches the level and the candle closes back on the breakout side. Enter at the next open, stop past that candle's wick, target 2x the risk. Closed after 4 hours if neither is hit.

Public sources for the rules:

- https://www.luxalgo.com/library/concept/breakout-pullback-continuation/
- https://fxopen.com/blog/en/how-can-you-use-a-break-and-retest-strategy-in-trading/
- https://www.thepatternsite.com/ThrowPull.html

Variations tested:

- `target-1r`: Target 1x risk
- `target-3r`: Target 3x risk
- `min-stop-5atr`: Skip stops under 5% of the typical daily move
- `min-stop-10atr`: Skip stops under 10% of the typical daily move
- `trend-1h-200ema`: Only trade with the 1-hour 200 EMA trend
- `min-break-half-candle`: Break must close half an average candle past the level
- `retest-24`: Wait up to 24 candles for the retest
- `swing-5`: Swings need 5 candles each side
- `entry-limit`: Limit order at the level, no wait for the retest to hold
- `tf-1m`: 1-minute candles
- `tf-15m`: 15-minute candles
- `tf-1h`: 1-hour candles

## Engulfing candle (textbook)

Strategy id: `engulfing-candle`. Gold (XAUUSD), 5m candles. Entry: market order at the open of the next minute after the setup forms. Full page: https://wicko.ai/strategies/engulfing-candle/

On 5-minute candles: buy at the next open when an up candle's body covers the body of the down candle before it (opens at or below its close, closes at or above its open, taller body), and that down candle closed below its 20-period EMA, so there was a decline to reverse. Sell short on the mirror pattern above the EMA. Stop beyond the low (high for shorts) of the two candles, target 2x the risk, closed after 4 hours if neither is hit.

Public sources for the rules:

- https://chartschool.stockcharts.com/table-of-contents/chart-analysis/candlestick-charts/candlestick-bullish-reversal-patterns
- https://thepatternsite.com/BullEngulfing.html
- https://thepatternsite.com/BearEngulfing.html
- https://www.investopedia.com/terms/b/bullishengulfingpattern.asp

Variations tested:

- `target-1r`: Target 1x risk
- `target-3r`: Target 3x risk
- `min-stop-5atr`: Skip setups with a stop under 5% of the typical daily move
- `min-stop-10atr`: Skip setups with a stop under 10% of the typical daily move
- `trend-1h-200ema`: Only trade with the 1-hour 200 EMA trend
- `no-prior-trend`: No prior trend needed (any engulfing pair)
- `prior-trend-ema10`: Shorter prior trend: first candle beyond its 10 EMA
- `engulf-wicks`: Engulfing candle must also cover the first candle's wicks
- `confirm-next`: Wait for the next candle to close beyond the engulfing close
- `tf-1m`: 1-minute candles
- `tf-15m`: 15-minute candles
- `tf-1h`: 1-hour candles

## Fair value gap (textbook)

Strategy id: `fvg-textbook`. Gold (XAUUSD), 5m candles. Entry: limit order that fills the first minute price touches it. Full page: https://wicko.ai/strategies/fair-value-gap/

Three back-to-back 5-minute candles leave a gap. Limit entry at the gap's middle, valid 2 hours. Stop beyond the first candle. Target 2x the risk. Closed after 4 hours if neither is hit.

Public sources for the rules:

- https://www.luxalgo.com/library/concept/fair-value-gap/

Variations tested:

- `target-1r`: Target 1x risk
- `target-1.5r`: Target 1.5x risk
- `target-3r`: Target 3x risk
- `entry-near`: Enter at the gap's near edge
- `entry-far`: Enter at the gap's far edge
- `min-stop-5atr`: Skip gaps with a stop under 5% of the typical daily move
- `min-stop-10atr`: Skip gaps with a stop under 10% of the typical daily move
- `trend-1h-200ema`: Only trade with the 1-hour 200 EMA trend
- `fill-1h`: Order live for 1 hour
- `fill-4h`: Order live for 4 hours
- `tf-1m`: 1-minute candles
- `tf-15m`: 15-minute candles
- `tf-1h`: 1-hour candles

## Fibonacci retracement 61.8% (textbook)

Strategy id: `fibonacci-retracement`. Gold (XAUUSD), 5m candles. Entry: limit order that fills the first minute price touches it. Full page: https://wicko.ai/strategies/fibonacci-retracement/

On 5-minute candles, draw Fibonacci levels over each new leg from a swing low to a swing high (3 candles each side). Place a limit buy at the 61.8% retracement once the swing high is confirmed, valid 2 hours. Stop at the swing low, target 2x the risk. Down legs are traded short the same way. Closed after 4 hours if neither is hit.

Public sources for the rules:

- https://chartschool.stockcharts.com/table-of-contents/chart-analysis/chart-annotation-tools/fibonacci-retracements
- https://www.investing.com/academy/analysis/how-to-use-fibonacci-retracements
- https://en.wikipedia.org/wiki/Fibonacci_retracement

Variations tested:

- `target-1r`: Target 1x risk (back to the swing high)
- `target-3r`: Target 3x risk (the 152.8% extension)
- `min-stop-5atr`: Skip legs with a stop under 5% of the typical daily move
- `min-stop-10atr`: Skip legs with a stop under 10% of the typical daily move
- `trend-1h-200ema`: Only trade with the 1-hour 200 EMA trend
- `entry-50`: Enter at the 50% level
- `entry-382`: Enter at the 38.2% level
- `entry-786`: Enter at the 78.6% level
- `stop-786`: Stop at the 78.6% level instead of the swing
- `swing-5`: Swings need 5 candles each side
- `tf-1m`: 1-minute candles
- `tf-15m`: 15-minute candles
- `tf-1h`: 1-hour candles

## Ichimoku cloud breakout (textbook)

Strategy id: `ichimoku-cloud`. Gold (XAUUSD), 5m candles. Entry: market order at the open of the next minute after the setup forms. Full page: https://wicko.ai/strategies/ichimoku-cloud/

On 5-minute candles with Ichimoku 9, 26, 52: buy at the next open when a candle closes above the top of the cloud after closing at or below it, with the Tenkan above the Kijun and the Chikou confirming (the close above the close 26 candles earlier). Sell short on the mirror break below the cloud. The cloud on each candle is the one drawn 26 candles earlier, so only closed candles are used. Stop at the Kijun, target 2x the risk, closed after 4 hours if neither is hit.

Public sources for the rules:

- https://chartschool.stockcharts.com/table-of-contents/technical-indicators-and-overlays/technical-overlays/ichimoku-cloud
- https://www.oanda.com/us-en/skills-and-insights/education/technical-analysis/indicators-and-oscillators/ichimoku-cloud-trading-guide-key-strategies/
- https://articles.stockcharts.com/article/stockcharts-insider-the-missing-step-in-ichimoku-cloud-breakout-strategies
- https://www.binance.com/en/academy/articles/ichimoku-clouds-explained

Variations tested:

- `target-1r`: Target 1x risk
- `target-3r`: Target 3x risk
- `min-stop-5atr`: Skip setups with a stop under 5% of the typical daily move
- `min-stop-10atr`: Skip setups with a stop under 10% of the typical daily move
- `trend-1h-200ema`: Only trade with the 1-hour 200 EMA trend
- `no-chikou`: No Chikou confirmation
- `future-cloud`: Cloud ahead must agree (green for longs, red for shorts)
- `stop-cloud`: Stop at the far side of the cloud instead of the Kijun
- `settings-20-60-120-30`: Slower settings 20, 60, 120, 30
- `tf-1m`: 1-minute candles
- `tf-15m`: 15-minute candles
- `tf-1h`: 1-hour candles

## ICT silver bullet (textbook)

Strategy id: `ict-silver-bullet`. Gold (XAUUSD), 5m candles. Entry: limit order that fills the first minute price touches it. Full page: https://wicko.ai/strategies/ict-silver-bullet/

Between 10:00 and 11:00 New York time, a 5-minute candle trades past the high or low made since New York midnight. After it, the first fair value gap in the opposite direction inside the window sets the trade: a limit order at the gap's middle, live until 11:00, stop beyond the swing that made the sweep, target 2x the risk. One setup a day. Closed after 4 hours if neither is hit.

Public sources for the rules:

- https://www.luxalgo.com/blog/ict-silver-bullet-setup-trading-methods/
- https://fxopen.com/blog/en/what-is-the-ict-silver-bullet-strategy-and-how-does-it-work/
- https://tradingfinder.com/education/forex/ict-silver-bullet

Variations tested:

- `target-1r`: Target 1x risk
- `target-3r`: Target 3x risk
- `min-stop-5atr`: Skip setups with a stop under 5% of the typical daily move
- `min-stop-10atr`: Skip setups with a stop under 10% of the typical daily move
- `trend-1h-200ema`: Only trade with the 1-hour 200 EMA trend
- `tf-1m`: 1-minute candles
- `entry-near`: Enter at the gap's near edge
- `stop-candle1`: Stop beyond the gap's first candle, not the swing
- `no-sweep`: No sweep needed: any gap in the window
- `window-london`: London window: 03:00 to 04:00 New York time
- `window-pm`: Afternoon window: 14:00 to 15:00 New York time
- `fill-1h`: Order live 1 hour, even past 11:00

## Inside bar breakout

Strategy id: `inside-bar-breakout`. Gold (XAUUSD), 5m candles. Entry: market order at the open of the next minute after the setup forms. Full page: https://wicko.ai/strategies/inside-bar-breakout/

On 5-minute candles, an inside bar is a candle whose high is lower and whose low is higher than the candle before it (the mother bar). Buy at the next open when a later candle closes above the mother bar's high, sell short when one closes below its low. Stop at the other side of the mother bar. Target 2x the risk. Closed after 4 hours if neither is hit.

Public sources for the rules:

- https://fxopen.com/blog/en/inside-bar-trading-strategy/
- https://capital.com/en-gb/learn/trading-strategies/inside-bar-trading-strategy
- https://trendspider.com/learning-center/the-inside-and-outside-bars-a-traders-guide/

Variations tested:

- `target-1r`: Target 1x risk
- `target-3r`: Target 3x risk
- `min-stop-5atr`: Skip setups with a stop under 5% of the typical daily move
- `min-stop-10atr`: Skip setups with a stop under 10% of the typical daily move
- `trend-1h-200ema`: Only trade with the 1-hour 200 EMA trend
- `stop-mother-mid`: Stop at the middle of the mother bar
- `stop-inside`: Stop at the other side of the inside bar
- `break-inside`: Enter on a close beyond the inside bar, not the mother bar
- `tf-1m`: 1-minute candles
- `tf-15m`: 15-minute candles
- `tf-1h`: 1-hour candles
- `tf-4h`: 4-hour candles

## Liquidity sweep (textbook)

Strategy id: `liquidity-sweep`. Gold (XAUUSD), 5m candles. Entry: market order at the open of the next minute after the setup forms. Full page: https://wicko.ai/strategies/liquidity-sweep/

A 5-minute candle trades past the previous day's high or low and closes back inside. Only the first push past each level each day counts. Enter at the next open in the reversal direction, stop beyond the sweep candle, target 2x the risk. Closed after 4 hours if neither is hit.

Public sources for the rules:

- https://www.luxalgo.com/library/concept/liquidity-sweep/
- https://www.tmgm.com/en/academy/trading-academy/liquidity-sweep
- https://crosstrade.io/learn/price-action/liquidity-sweeps

Variations tested:

- `target-1r`: Target 1x risk
- `target-1.5r`: Target 1.5x risk
- `target-3r`: Target 3x risk
- `min-stop-5atr`: Skip sweeps with a stop under 5% of the typical daily move
- `min-stop-10atr`: Skip sweeps with a stop under 10% of the typical daily move
- `trend-1h-200ema`: Only trade with the 1-hour 200 EMA trend
- `tf-1m`: 1-minute candles
- `tf-15m`: 15-minute candles
- `level-session`: Previous session's high and low instead of previous day's
- `every-sweep`: Every sweep of the level, not only the first push
- `entry-level`: Limit order back at the swept level, live 2 hours
- `london-ny`: Only setups during London and New York hours

## London breakout

Strategy id: `london-breakout`. Gold (XAUUSD), 5m candles. Entry: market order at the open of the next minute after the setup forms. Full page: https://wicko.ai/strategies/london-breakout/

Mark the high and low of the 5-minute candles from 00:00 to 07:00 UTC (the Asian range). Between 07:00 and 10:00 UTC, the first 5-minute candle that closes above the range is a buy and the first that closes below it is a sell, entered at the next candle's open. One trade a day. Stop at the other side of the range. Target 2x the risk. Closed after 4 hours if neither is hit.

Public sources for the rules:

- https://www.dailyforex.com/forex-articles/london-breakout-strategy/210474
- https://therighttrader.com/learn/trading-strategies/london-breakout-strategy

Variations tested:

- `target-1r`: Target 1x risk
- `target-3r`: Target 3x risk
- `stop-mid`: Stop at the middle of the Asian range
- `range-size-filter`: Skip days whose Asian range is under 25% or over 80% of the typical daily move
- `trend-1h-200ema`: Only trade with the 1-hour 200 EMA trend
- `london-clock`: Follow London's clock (one hour earlier in UTC in British summer time)
- `window-1h`: Breakouts count only in London's first hour
- `window-5h`: Breakouts count for London's first 5 hours
- `tf-1m`: 1-minute candles
- `tf-15m`: 15-minute candles

## MACD crossover (textbook)

Strategy id: `macd-crossover`. Gold (XAUUSD), 5m candles. Entry: market order at the open of the next minute after the setup forms. Full page: https://wicko.ai/strategies/macd-crossover/

On 5-minute candles with MACD 12, 26, 9: buy at the next open when the MACD line closes above the signal line after being at or below it, sell short on the mirror cross. The textbook signal has no stop, so the stop is the most common public one: the lowest low (highest high for shorts) of the leg since the previous opposite cross. Target 2x the risk. Closed after 4 hours if neither is hit.

Public sources for the rules:

- https://chartschool.stockcharts.com/table-of-contents/technical-indicators-and-overlays/technical-indicators/macd-moving-average-convergence-divergence-oscillator
- https://www.macroption.com/macd-crossover/
- https://therighttrader.com/learn/indicator-strategies/macd-trading-strategy
- https://therighttrader.com/learn/indicator-strategies/macd-zero-line-crossover

Variations tested:

- `target-1r`: Target 1x risk
- `target-3r`: Target 3x risk
- `min-stop-5atr`: Skip setups with a stop under 5% of the typical daily move
- `min-stop-10atr`: Skip setups with a stop under 10% of the typical daily move
- `trend-1h-200ema`: Only trade with the 1-hour 200 EMA trend
- `zero-trend`: Longs only above the zero line, shorts only below
- `zero-reversal`: Longs only below the zero line, shorts only above
- `stop-last10`: Stop at the low (high) of the last 10 candles
- `settings-5-35-5`: Faster MACD settings 5, 35, 5
- `tf-1m`: 1-minute candles
- `tf-15m`: 15-minute candles
- `tf-1h`: 1-hour candles

## Order block (textbook)

Strategy id: `order-block`. Gold (XAUUSD), 5m candles. Entry: limit order that fills the first minute price touches it. Full page: https://wicko.ai/strategies/order-block/

A 5-minute candle closes beyond the latest swing high or low (3 candles each side). The last opposite candle in the 10 before it is the order block. Limit entry at the block's near edge, valid 2 hours. Stop past the block's far edge, target 2x the risk. Closed after 4 hours if neither is hit.

Public sources for the rules:

- https://www.luxalgo.com/library/concept/order-block/
- https://www.cmcmarkets.com/en-gb/trading-strategies/order-block-trading-explained
- https://crosstrade.io/learn/price-action/order-blocks

Variations tested:

- `target-1r`: Target 1x risk
- `target-3r`: Target 3x risk
- `min-stop-5atr`: Skip blocks with a stop under 5% of the typical daily move
- `min-stop-10atr`: Skip blocks with a stop under 10% of the typical daily move
- `trend-1h-200ema`: Only trade with the 1-hour 200 EMA trend
- `entry-mid`: Enter at the block's middle (the 50% level)
- `entry-body`: Enter at the block's body edge (its open)
- `with-fvg`: The move must leave a fair value gap
- `swing-5`: Swings need 5 candles each side
- `fill-4h`: Order live for 4 hours
- `tf-1m`: 1-minute candles
- `tf-15m`: 15-minute candles
- `tf-1h`: 1-hour candles

## RSI divergence (textbook)

Strategy id: `rsi-divergence`. Gold (XAUUSD), 5m candles. Entry: market order at the open of the next minute after the setup forms. Full page: https://wicko.ai/strategies/rsi-divergence/

On 5-minute candles, price makes a lower swing low while the 14-period RSI makes a higher low (bullish), or a higher swing high while RSI makes a lower high (bearish), with the two swings 5 to 60 candles apart. A swing needs 3 candles on each side. Enter at the next open once a candle closes beyond the highest high (lowest low) between the two swings, within 2 hours. Stop at the second swing. Target 2x the risk. Closed after 4 hours if neither is hit.

Public sources for the rules:

- https://www.tradingview.com/support/solutions/43000502338-relative-strength-index-rsi/
- https://chartschool.stockcharts.com/table-of-contents/technical-indicators-and-overlays/technical-indicators/relative-strength-index-rsi
- https://www.luxalgo.com/library/indicator/5fFcLNgg-divergence-rsi/
- https://thepatternsite.com/DivergenceTest.html

Variations tested:

- `target-1r`: Target 1x risk
- `target-3r`: Target 3x risk
- `min-stop-5atr`: Skip setups with a stop under 5% of the typical daily move
- `min-stop-10atr`: Skip setups with a stop under 10% of the typical daily move
- `trend-1h-200ema`: Only trade with the 1-hour 200 EMA trend
- `no-confirm`: Enter as soon as the divergence shows, no waiting for a close
- `rsi-zone`: First swing's RSI under 30 (over 70 for bearish)
- `min-rsi-diff-3`: RSI must differ by at least 3 points
- `swing-5`: Swings need 5 candles on each side
- `longs-only`: Bullish divergence only (longs)
- `tf-1m`: 1-minute candles
- `tf-15m`: 15-minute candles
- `tf-1h`: 1-hour candles

## Supertrend flip (textbook)

Strategy id: `supertrend`. Gold (XAUUSD), 5m candles. Entry: market order at the open of the next minute after the setup forms. Full page: https://wicko.ai/strategies/supertrend/

On 5-minute candles with the default Supertrend (ATR 10, multiplier 3), the line flips from above price to below it: buy at the next open. Stop at the Supertrend line, target 2x the risk, closed after 4 hours if neither is hit. Sells are the mirror image.

Public sources for the rules:

- https://www.luxalgo.com/library/concept/supertrend/
- https://therighttrader.com/learn/indicators/supertrend

Variations tested:

- `target-1r`: Target 1x risk
- `target-3r`: Target 3x risk
- `exit-flip`: No target: hold until the line flips back (stop stays at the entry line)
- `min-stop-5atr`: Skip flips with a stop under 5% of the typical daily move
- `min-stop-10atr`: Skip flips with a stop under 10% of the typical daily move
- `trend-1h-200ema`: Only trade with the 1-hour 200 EMA trend
- `tf-1m`: 1-minute candles
- `tf-15m`: 15-minute candles
- `tf-1h`: 1-hour candles
- `mult-2`: Multiplier 2 instead of 3 (tighter line, more flips)
- `mult-4`: Multiplier 4 instead of 3 (wider line, fewer flips)
- `atr-7`: ATR length 7 instead of 10
- `confirm-candle`: Wait one candle after the flip and enter only if it holds
