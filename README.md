# Portfolio RiskLab
### Portfolio Risk, Value at Risk (VaR), and Stress Testing Engine

A Python-based portfolio risk analytics project for studying historical equity performance, portfolio volatility, downside risk, hypothetical market shocks, and Value at Risk (VaR) model performance.

The project uses historical market data to analyze a selected basket of Indian equities against the NIFTY 50 benchmark. It includes configurable stock selection, portfolio weights, statistical analysis, multiple VaR approaches, scenario-based stress testing, and rolling historical VaR backtesting.

> **Project status:** Base version (v1.0) — Days 1–7  
> **Environment:** Google Colab / Jupyter Notebook  
> **Primary language:** Python

---

## Table of Contents

- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Data Source](#data-source)
- [Stock Selection and Portfolio Configuration](#stock-selection-and-portfolio-configuration)
- [Methodology](#methodology)
  - [Day 1 — Data Collection and Cleaning](#day-1--data-collection-and-cleaning)
  - [Day 2 — Returns and Statistical Analysis](#day-2--returns-and-statistical-analysis)
  - [Day 3 — Portfolio Construction and Performance](#day-3--portfolio-construction-and-performance)
  - [Day 4 — Historical and Parametric VaR](#day-4--historical-and-parametric-var)
  - [Day 5 — Monte Carlo VaR and CVaR](#day-5--monte-carlo-var-and-cvar)
  - [Day 6 — Stress Testing](#day-6--stress-testing)
  - [Day 7 — VaR Backtesting](#day-7--var-backtesting)
- [Key Financial and Statistical Measures](#key-financial-and-statistical-measures)
- [How to Run the Project](#how-to-run-the-project)
- [Outputs](#outputs)
- [Results and Observations](#results-and-observations)
- [Assumptions and Limitations](#assumptions-and-limitations)
- [Future Improvements](#future-improvements)
- [Disclaimer](#disclaimer)
- [Author](#author)

---

## Project Overview

Portfolio RiskLab is an educational quantitative finance project designed to explore portfolio performance and downside risk using Python.

The notebook downloads historical price data, calculates stock-level and portfolio-level statistics, estimates VaR using different approaches, evaluates hypothetical stress scenarios, and performs rolling historical VaR backtesting.

The project can be configured to analyze:

- A baseline basket of Indian equities
- A personal watchlist
- A hypothetical portfolio
- A custom portfolio with user-defined weights

The initial implementation uses an equal-weight portfolio by default. Custom weights can be supplied for alternative portfolio experiments.

The project is focused on **portfolio analytics and risk measurement**, rather than automated trading or stock-price prediction.

---

## Objectives

1. Collect and clean historical market-price data.
2. Calculate simple and logarithmic returns.
3. Measure volatility, covariance, and correlation.
4. Construct a portfolio using selected stocks and portfolio weights.
5. Compare portfolio performance with the NIFTY 50 benchmark.
6. Estimate portfolio downside risk using historical, parametric, and Monte Carlo VaR.
7. Calculate Conditional Value at Risk (CVaR), also known as Expected Shortfall.
8. Evaluate hypothetical market and sector shocks through stress testing.
9. Backtest rolling historical VaR estimates against subsequent realized losses.
10. Present the analysis through tables and visualizations.

---

## Features

### Market Data Analysis
- Historical adjusted closing prices
- Data cleaning and missing-value inspection
- Individual stock return calculations
- Daily and rolling volatility
- Correlation analysis

### Portfolio Analytics
- Equal-weight portfolio construction
- Custom portfolio weights
- Portfolio return calculation
- Cumulative performance comparison against NIFTY 50
- Annualized return and volatility
- Sharpe and Sortino ratios
- Maximum drawdown
- Covariance matrix
- Portfolio risk contribution

### Downside Risk Measurement
- Historical VaR
- Parametric VaR using a normal-distribution assumption
- Monte Carlo VaR
- Conditional Value at Risk (CVaR)

### Stress Testing
- Hypothetical broad-market shock
- Banking-sector shock
- IT-sector shock
- Combined market and sector shock
- Custom scenario shocks
- Estimated portfolio-level and stock-level loss contributions

### VaR Backtesting
- Rolling historical VaR estimation
- Trailing lookback window
- Actual loss versus estimated VaR comparison
- VaR breach identification
- Observed breach-rate summary

---

## Technology Stack

| Technology | Usage |
|---|---|
| Python | Main programming language |
| Pandas | Data manipulation and time-series analysis |
| NumPy | Numerical computation and simulation |
| SciPy | Statistical distribution functions |
| yfinance | Historical market-data retrieval |
| Matplotlib | Data visualization |
| Google Colab | Primary development environment |
| GitHub | Version control and project hosting |

---

## Project Structure

```text
portfolio-risklab/
│
├── Portfolio_RiskLab.ipynb
├── README.md
├── requirements.txt
├── .gitignore
│
└── images/
    ├── portfolio_performance.png
    ├── correlation_heatmap.png
    ├── volatility_analysis.png
    ├── var_comparison.png
    ├── stress_test_results.png
    └── var_backtesting.png
```

The `images/` folder is optional. Add screenshots or exported charts after generating and reviewing them.

The current base version is organized in a single notebook. The code can be refactored into reusable Python modules in a future version.

---

## Data Source

Historical market data is retrieved using the `yfinance` Python library.

Example instruments include:

| Instrument | Example ticker |
|---|---|
| Reliance Industries | `RELIANCE.NS` |
| Tata Consultancy Services | `TCS.NS` |
| Infosys | `INFY.NS` |
| HDFC Bank | `HDFCBANK.NS` |
| ICICI Bank | `ICICIBANK.NS` |
| State Bank of India | `SBIN.NS` |
| ITC | `ITC.NS` |
| Larsen & Toubro | `LT.NS` |
| Bharti Airtel | `BHARTIARTL.NS` |
| Sun Pharma | `SUNPHARMA.NS` |
| NIFTY 50 benchmark | `^NSEI` |

The stock list is configurable. Users can replace the baseline tickers with other supported symbols.

The notebook uses adjusted closing prices for return calculations. Historical data availability varies by instrument and data provider.

**Data-source note:** yfinance is an unofficial interface for accessing Yahoo Finance data. It is used here for educational and research practice, not as an official exchange feed or guaranteed real-time data source. Review the applicable Yahoo Finance terms and data-provider conditions before using the data for other purposes.

---

## Stock Selection and Portfolio Configuration

The notebook supports three stock-selection modes:

- `baseline` — original example basket
- `personal` — user-selected holdings or watchlist
- `custom` — an experimental basket of selected stocks

Users can modify the configuration cell in the notebook to change the selected tickers.

### Portfolio weights

The initial portfolio uses equal weights.

For a custom portfolio, weights can be entered as percentages and converted into decimal proportions. The weights should total 100%.

For example, a hypothetical portfolio with three assets could use weights of 40%, 35%, and 25%.

The notebook checks that the selected stocks have available price data and that the portfolio weights sum to 1.

### Stocks with shorter histories

Not all stocks have the same listing date or historical data availability.

The notebook reports the available observation count and date range for each selected instrument. Portfolio calculations use aligned observations for the selected holdings.

A shorter history results in a shorter common analysis period. Missing pre-listing observations should not be replaced with artificial zero prices or zero returns.

---

## Methodology

### Day 1 — Data Collection and Cleaning

- Configure stock tickers and benchmark.
- Download historical market data.
- Extract adjusted closing prices.
- Inspect missing values and duplicate dates.
- Clean the price dataset.
- Save the cleaned price data.

### Day 2 — Returns and Statistical Analysis

Calculate:

- Simple daily returns
- Logarithmic returns
- Mean daily return
- Standard deviation
- Annualized volatility
- Rolling 30-day volatility
- Correlation matrix
- Correlation with NIFTY 50

Visualizations include normalized price performance, return distributions, rolling volatility, and a correlation heatmap.

### Day 3 — Portfolio Construction and Performance

Construct the portfolio using selected stocks and weights.

Calculate:

- Portfolio daily returns
- Cumulative portfolio performance
- Benchmark performance
- Total return
- CAGR
- Annualized average return
- Annualized volatility
- Sharpe ratio
- Sortino ratio
- Maximum drawdown
- Covariance matrix
- Portfolio variance
- Stock-level risk contribution

### Day 4 — Historical and Parametric VaR

Estimate one-day VaR at selected confidence levels, including 95% and 99%.

**Historical VaR:** Uses the empirical distribution of observed portfolio returns.

**Parametric VaR:** Uses the portfolio's estimated mean and standard deviation under a normal-distribution assumption.

The estimates are presented as return-based thresholds and can also be converted into illustrative monetary amounts using a configurable portfolio value.

### Day 5 — Monte Carlo VaR and CVaR

Generate simulated portfolio returns using a normal distribution parameterized by the historical mean and standard deviation.

Use the simulated return distribution to estimate Monte Carlo VaR.

Calculate CVaR by estimating the average loss in the tail beyond the selected VaR threshold.

The current simulation is a simplified model. It does not capture all real-world market characteristics, such as changing volatility, fat tails, jumps, or changing correlations.

### Day 6 — Stress Testing

Apply hypothetical shocks to selected portfolio holdings.

Scenarios include:

- Broad-market decline
- Banking-sector decline
- IT-sector decline
- Combined market and sector decline
- User-defined custom shock

Calculate the resulting portfolio return and estimated monetary profit or loss.

The scenarios are illustrative assumptions, not forecasts or probability estimates.

### Day 7 — VaR Backtesting

Use a rolling historical VaR model with a trailing 252-observation window.

For each eligible date:

1. Estimate VaR using only prior observations.
2. Compare the forecast threshold with the subsequent realized loss.
3. Identify whether a VaR breach occurred.
4. Calculate the observed breach count and breach rate.

The backtest compares observed breach rates with the nominal tail probabilities associated with the selected confidence levels.

---

## Key Financial and Statistical Measures

| Measure | Description |
|---|---|
| Simple return | Percentage change in price between consecutive observations |
| Log return | Natural logarithm of the ratio of consecutive prices |
| Variance | Measure of dispersion of returns around their mean |
| Standard deviation | Square root of variance; commonly used as a volatility measure |
| Annualized volatility | Daily standard deviation scaled by the square root of 252 trading days |
| Covariance | Measure of joint variation between two return series |
| Correlation | Standardized measure of linear co-movement, ranging from -1 to +1 |
| CAGR | Compound annual growth rate over the selected period |
| Sharpe ratio | Excess return divided by volatility |
| Sortino ratio | Return relative to downside deviation |
| Maximum drawdown | Largest peak-to-trough decline in cumulative portfolio value |
| VaR | Estimated loss threshold at a specified confidence level |
| CVaR / Expected Shortfall | Average loss in the tail beyond the VaR threshold |
| VaR breach | An observed loss that exceeds the model's VaR threshold |

Annualization and ratio calculations depend on assumptions and conventions. The notebook documents the assumptions used in its calculations.

---

## How to Run the Project

### Option 1 — Google Colab (Recommended)

1. Open the notebook in the repository.
2. Select **Open in Colab**, or upload the `.ipynb` file to Google Colab.
3. Run the notebook cells in order, starting from Day 1.
4. Review the selected tickers and analysis dates in the configuration section.
5. Run Days 1–7 sequentially.
6. Review the tables, plots, and generated CSV files.

If you change the selected stock list or portfolio weights, rerun the relevant cells from the beginning so all downstream calculations use the updated configuration.

### Option 2 — Run Locally

Requires Python 3.10 or later.

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/portfolio-risklab.git
cd portfolio-risklab
```

Create and activate a virtual environment:

```bash
python -m venv .venv
```

On Windows:

```bash
.venv\Scripts\activate
```

On macOS/Linux:

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Start Jupyter:

```bash
jupyter notebook
```

Open `Portfolio_RiskLab.ipynb` and execute the cells sequentially.

---

## Outputs

The notebook generates analytical tables, visualizations, and CSV files.

Example outputs include:

- Cleaned adjusted closing prices
- Daily and logarithmic returns
- Rolling volatility
- Correlation matrix
- Portfolio weights
- Portfolio performance metrics
- Covariance matrix
- Risk contribution
- Historical and parametric VaR
- Monte Carlo VaR and CVaR
- Stress scenario returns and estimated losses
- Stock-level stress-loss contributions
- Rolling VaR backtesting results
- VaR breach summary

The CSV files are generated during notebook execution. They are not required to be committed to GitHub unless they are intentionally included as sample outputs.

---

## Results and Observations

Add your verified findings here after running the notebook.

Suggested items to document:

- Selected stocks and analysis period
- Number of valid observations
- Portfolio annualized volatility
- Portfolio maximum drawdown
- Portfolio performance compared with NIFTY 50
- Historical, parametric, and Monte Carlo VaR estimates
- CVaR estimates
- Stress scenario results
- 95% and 99% VaR breach counts and observed rates

Do not interpret historical results as guaranteed future performance.

---

## Assumptions and Limitations

1. **Historical data:** Results depend on the data provider, available history, adjusted-price methodology, and data quality.
2. **Shorter listing histories:** Newer stocks have fewer observations, which can make statistical estimates more sample-sensitive.
3. **Portfolio weights:** The baseline portfolio uses equal weights unless custom weights are supplied.
4. **Risk-free rate:** The current Sharpe ratio calculation assumes a 0% risk-free rate unless modified.
5. **Annualization:** The notebook uses 252 trading days as an annualization convention.
6. **Normality assumption:** Parametric and current Monte Carlo VaR use a normal-distribution assumption.
7. **Monte Carlo model:** Simulations use estimated historical mean and standard deviation and do not model all market dynamics.
8. **Stress scenarios:** Scenario shocks are user-defined hypothetical assumptions, not forecasts.
9. **Backtesting:** Historical VaR breach rates are sample-dependent and do not guarantee future model performance.
10. **Investment cash flows:** Historical market-price analysis is not a complete personal investment return calculation. Deposits, withdrawals, trades, dividends, fees, and taxes may affect actual investor outcomes.
11. **No transaction-cost modeling:** The base version does not comprehensively model brokerage fees, taxes, slippage, or market impact.
12. **No live brokerage integration:** The project does not connect to a brokerage account or automatically track live holdings.

---

## Future Improvements

Potential extensions include:

- Interactive Streamlit dashboard
- SQLite or DuckDB storage and SQL analytics
- Additional portfolio weighting methods
- Historical scenario analysis
- Alternative volatility and return-distribution models
- More detailed VaR backtesting diagnostics
- Transaction-cost and slippage modeling
- Automated data-quality checks
- Unit tests for portfolio and risk calculations
- Modular Python source files
- Exportable portfolio risk reports

These are planned extensions and are not part of the current base version unless explicitly implemented.

---

## Disclaimer

This project is intended for educational and analytical purposes only.

It is not investment advice, a trading recommendation, or a guarantee of future performance. Historical returns, risk measures, simulations, and hypothetical stress scenarios have limitations and should not be treated as predictions of future market behavior.

The project does not account for every factor that may affect actual investment outcomes, including transaction costs, taxes, liquidity constraints, corporate actions, and investor-specific circumstances.

---

## Author

**Chirag Agrawal**

- Location: Vadodara, Gujarat, India
- LinkedIn: [linkedin.com/in/chirag-agrawal-180614221](https://www.linkedin.com/in/chirag-agrawal-180614221/)
- GitHub: [github.com/chirag1503](https://github.com/chirag1503)

---

**Project:** Portfolio RiskLab — Portfolio Risk, VaR & Stress Testing Engine  
**Version:** 1.0 — Base implementation covering Days 1–7
