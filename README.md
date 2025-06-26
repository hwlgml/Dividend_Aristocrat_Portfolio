# Optimization of Dividend Aristocrat Portfolio Utilizing Fundamental Data and Backtesting

## Overview
This project was conducted as part of the Y-FoRM 24-1 long-term project initiative. Please refer to the full report for a comprehensive analysis and detailed results.

This project is dedicated to the optimization of a Dividend Aristocrat portfolio by leveraging fundamental financial data. The portfolio optimization primarily focuses on maximizing the Sharpe Ratio while ensuring stable and consistent dividend income, even during periods of market volatility. The study involves the use of key financial metrics, such as the Price-to-Earnings Ratio (PER) and Price-to-Free Cash Flow (P/FCF), to enhance the predictive capability of dividend payments and portfolio stability.

## Background
### Motivation
The increasing pace of population aging and the relatively low levels of pension income have heightened the need for investment portfolios that can generate stable income, particularly in uncertain economic environments. Dividend Aristocrats, which are companies that have increased their dividends for at least 25 consecutive years, offer a potential solution due to their consistent and reliable dividend payouts.

### Project Objective
The goal of this project is to create a mathematically optimized portfolio that focuses on Dividend Aristocrats, integrating constraints derived from fundamental data to better predict future dividends and optimize asset positioning. The project uses the Sharpe Ratio as the primary measure of portfolio performance, reflecting the trade-off between risk and return.

## Methodology
### Data Preprocessing

- **Dividend Data Adjustment**: The dataset was adjusted for special dividends, outliers in dividend payouts, and ensured consistent dividend distributions across selected stocks.
- **Investment Universe Expansion**: The universe of investable stocks was expanded from 30 to 63 Dividend Aristocrats to enhance diversification and improve portfolio robustness.
- **Backtesting Period**: The backtesting was conducted over the period from 2016 to 2023, with a sliding window of 3 years of data used to predict and rebalance the portfolio annually.

### Theoretical Framework
- **Gordon Growth Model**: The Gordon Growth Model (GGM) was employed to justify the assumption that a company’s stock price growth rate can be approximated by its dividend growth rate. The GGM is expressed as:

$$
R_i = \frac{D_i}{P_i} + g_i
$$

where:

- $R_i$ is the expected return for stock *i*
- $D_i$ is the dividend at time *i*
- $P_i$ is the price of the stock at time *i*
- $g_i$ is the expected growth rate of dividends for stock *i*

This model assumes that the dividends grow at a constant rate *g_i* which was validated through historical data analysis.

### Portfolio Optimization
- **Sharpe Ratio Maximization**: The optimization problem was formulated to maximize the Sharpe Ratio, defined as:

$$
S = \frac{E[R_p] - R_f}{\sigma_p}
$$

where:

- $E[R_p]$ is the expected portfolio return  
- $R_f$ is the risk-free rate (e.g., U.S. Treasury yield)  
- $\sigma_p$ is the standard deviation of portfolio returns  

The objective function was thus:

$$
\max \quad S = \frac{\sum_{i=1}^{n} w_i \left( \frac{D_i}{P_i} + g_i \right) - R_f}
{\sqrt{\sum_{i=1}^{n} w_i^2 \sigma_i^2}}
$$

subject to:

- $\sum_{i=1}^{n} w_i = 1$ (Portfolio weights sum to 1)  
- $w_i \leq 0.20$ for individual stock weights  
- Constraints based on PER and P/FCF (e.g., if $PER_i < 0$ or $PER_i > 50$, then $w_i \leq 0.01$)

### Rebalancing Strategy
- **Annual Rebalancing**: The portfolio was rebalanced annually, using a sliding window approach. Data from the previous 3 years was used to set the weights for the next year’s portfolio, adjusting for changes in stock prices and dividends.

## Results and Analysis
- **Sharpe Ratio**: The optimized portfolio demonstrated a superior Sharpe Ratio compared to a simple equally-weighted portfolio of Dividend Aristocrats, indicating better risk-adjusted returns.
- **Dividend Stability**: The portfolio provided stable monthly dividends, with an emphasis on maintaining a minimum of $100 in monthly dividend income, even during the market downturns in 2020 and 2021.
- **Gordon Growth Model Validation**: The assumptions of the Gordon Growth Model were largely validated, although some deviations were observed, particularly in periods of extreme market volatility.

### Limitations
- **Assumptions**: The model assumes that stocks can be purchased at their closing prices, which may not always be feasible in real-world trading scenarios.
- **Fixed Rebalancing Date**: Rebalancing was fixed at the start of each year (January 1st), which may not capture optimal rebalancing opportunities throughout the year.

## Future Work
- **Dynamic Rebalancing**: Implement real-time data integration to enable dynamic rebalancing based on market conditions and updated financial metrics.
- **Exploration of Alternative Models**: Investigate alternative models for predicting dividend growth and stock price appreciation to further refine the portfolio optimization process.

## Conclusion
This project successfully developed an optimized Dividend Aristocrat portfolio that leverages fundamental financial data to maximize risk-adjusted returns while maintaining stable dividend income. The findings demonstrate the potential for fundamental data-driven portfolio optimization in enhancing investment outcomes, particularly for income-focused investors.

## Appendix
### Key Parameters

- $w_i$: Weight of stock *i* in the portfolio  
- $g_i$: Dividend growth rate for stock *i*  
- $d_i$: Dividend yield for stock *i*  

### Objective Function
The objective function for maximizing the Sharpe Ratio incorporating the Gordon Growth Model was implemented as follows:

$$
\max \quad \frac{\sum_{i=1}^{n} w_i \left( \frac{D_i}{P_i} + g_i \right) - R_f}
{\sqrt{\sum_{i=1}^{n} w_i^2 \sigma_i^2}}
$$

### Optimization Techniques
- **Simple Sharpe Ratio Maximization**: Focused purely on historical returns and volatility.
- **Gordon Growth Model-Based Sharpe Ratio Maximization**: Incorporated expected dividend growth and yield into the optimization process.
