## Momentum Factor Research: Replicating Jegadeesh & Titman (1993)
Overview: This repository contains a quantitative research project exploring the 12-1 Momentum Factor.

Goal: To build a rigorous backtesting pipeline in Python, moving from raw market data to statistical validation and out-of-sample testing.

## Methodology
1. Data & Universe
- Universe: 50 large-cap stocks from the S&P 500.
- Source: yfinance (Adjusted closing prices from 2021 to 2024).
- Frequency: Monthly resampled data.
2. Signal Engineering (12-1 Momentum)
  
The signal follows the academic standard of 12-1 momentum:
- Formation Period: 12 months.
- Mean Reversion Buffer: The most recent month (t-1) is excluded from the cumulative return calculation to account for short-term mean reversion, which can otherwise decay the momentum signal.
3. Backtesting Logic
- Lagged Execution: To prevent lookahead bias, positions are decided at the end of month $t$ and "traded" at the end of month $t+1$.
- Portfolio Construction: Every month, the universe is ranked by signal strength. The top 20% (Winners) are held long, and the bottom 20% (Losers) are held short.
- Weighting: Equal-weighted across all positions.

## Performance & Statistical Validation
The model was evaluated on both its raw returns and its statistical significance:

Metric	Result:
- Annualized Return	-0.33%
- Annualized Volatility	4.37%
- Sharpe: -0.99
- Max Drawdown	-6.24%
- Win Rate	52.17%

## Key Findings
- Statistical Significance: The T-statistic of -0.1051 and P-value of 0.9172 indicate that for this specific 50-stock universe and time period, the results were not statistically significant at the 5% level.
- Out-of-Sample Decay: A split-sample analysis (in-sample 2022 vs. out-of-sample 2023-2024) showed in-sample returns of +3.16% deteriorating to -3.53% out-of-sample, suggesting the momentum signal did not generalize beyond the training period in a concentrated large-cap universe.
