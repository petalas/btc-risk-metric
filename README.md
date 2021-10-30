
# BTC risk indicator
<!-- tags: bitcoin BTC risk metric indicator oscillator TradingView -->

## Disclaimer
This is a work in progress. It is also untested and not in any way financial advice.

## Main idea
Combine multiple metrics in an attempt to predict local tops and bottoms.

Can be used as a buy / sell signal or as a way to dynamically DCA based on how 'risky' current price level is.

## What's in this repo?

There are 2 pine scripts in here, both are indicators designed to work with TradingView.

It's the same logic in both, one of them in an overlay and the other one is an oscillator scaled to the 0..1 range.

## Preview
![BTC Risk Indicator Preview](preview.png?raw=true "BTC Risk Indicator Preview")

## Metrics involved so far, **open to suggestions** for more.

- [x] 5 DAY EMA / 50 WEEK EMA
- [x] [Mayer Multiple](https://stats.buybitcoinworldwide.com/mayermultiple/)
- [x] [Sharpe Ratio](https://www.investopedia.com/terms/s/sharperatio.asp)
- [x] Price / 400 DAY EMA
- [x] [RSI](https://www.investopedia.com/terms/r/rsi.asp) 20
- [x] [Puell Multiple](https://www.lookintobitcoin.com/charts/puell-multiple/)
- [ ] [Power Law](https://stats.buybitcoinworldwide.com/long-term-power-law/)
- [ ] [Sortino Ratio](https://www.investopedia.com/terms/s/sortinoratio.asp#:~:text=The%20Sortino%20ratio%20takes%20an,Sortino.)
- [ ] Bitcoin google trend numbers
- [ ] [RUPL/NUPL](https://www.lookintobitcoin.com/charts/relative-unrealized-profit--loss/)

## Current logic

Average the above metrics and then try to adjust / correct the average (explained below).

## Main problem

Because of the logarithmic nature of BTC growth and diminishing returns the peaks of our oscillator get lower and lower and the bottoms get higher and higher. We are also dealing with data (prices) that span multiple orders of magnitute which is not ideal when mapping to the 0..1 range.

## Current logic to adjust / correct the average

Multiplying by the log of the linear regression and by the log of average true range.

`multi = math.log(lr) * math.log(ta.atr(5)) // feels too arbitrary, open to suggestions`

### Effect of the adjustment (light blue is the 'before')
![Adjustment](adjustment.png?raw=true "Effect of the adjustment")

The peaks look okay after the adjustment but the bottoms don't go below 0.25 after 2013 or so, open to suggestions on how to adjust it better.

## TODO list / current ideas:
 - Optimize rolling window length of various oscillators
 - Figure out what other metrics we can use, maybe MACD etc
 - Figure out a better way to adjust for diminishing returns and the logarithmic nature of BTC growth
 - Weighted average + optimization of the weights by
     - neural networks
     - simulated annealing
     - monte carlo simmulations
     - genetic algorithms
- Run backtests and calculate net profit
- Use net profit as a fitness function to 'evolve' a better indicator automagically (a combination of the above 2)

## Contributing
If you have any suggestions or ideas for improvement please get in touch.

Feel free to [email me](mailto:webmasternikos@gmail.com). You can also just open a PR.

I am just now getting familiar with pine script and I am also not an expert in this field so there's likely plenty of room for improvement.

### Credits
Inspired by [Benjamin Cowen](https://www.youtube.com/channel/UCRvqjQPSeaWn-uEx-w0XOIg)'s BTC risk idea.

Special thanks to [Bitcoin Raven](https://www.youtube.com/channel/UCrlkqSLmHL8ZPVpOxj7La4Q) for working most of the oscillators involved and [Jay](https://www.youtube.com/channel/UC_bG7yHgT_xOUKvI2Hvo6Vg) for suggestions.


## If you find this useful please consider supporting this project.
|    | Address |
-----|-----
BTC  | 3B1gtQhVQj1x5c1jzVHHzq2eGKyEqf7rQb
ETH  | 0x18Df0b2C16d3E3927Ef74e02268fE36949bb6b2c
ADA  | addr1vyqvaqs56d90ha55duh04eh59y7fcps8duplgm987nyhv9qp3n05f
USDT | 0x96A37296B30Bf19A917c34810b3f040192Be2e67
