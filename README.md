# Macro-Factor-Driven Investment Strategy

## Overview
Systematic quantitative investment strategy developed at **AQUA (Advanced Quantitative Analytics)** that links 50+ Indian macroeconomic indicators to sector and factor returns using Hidden Markov Model (HMM) regime detection and statistical regression analysis.

**Status**: ⏳ In Development (Regime detection complete, backtesting in progress)

## Strategy Framework

### Core Components

#### 1. Macroeconomic Data Pipeline
- **50+ Indicators**: GDP growth, inflation (CPI/WPI), repo rates, GSec yields, USD/INR exchange rate, crude oil prices, FPI flows, PMI, IIP, auto sales, cement consumption
- **Sources**: RBI, MOSPI, CEIC, NSE, BSE
- **Frequency**: Monthly/Weekly updates
- **Time Horizon**: Historical analysis Feb 2019 - Jan 2026

#### 2. Regime Detection (Hidden Markov Model)
**Objective**: Identify market regimes (bullish, neutral, bearish, high volatility)

**Methodology**:
- Train HMM on returns + volatility + macro indicators
- 3-state model: Risk-On, Risk-Off, Transition
- State probabilities guide allocation intensity

**Implementation**: `regime_detection.ipynb`

#### 3. Factor-Macro Correlation Analysis
**Key Findings** (from analysis):
- **Crude Oil ↔ INR**: Negative correlation (-0.65) - rupee depreciates when crude rises
- **FPI Flows ↔ Equity Returns**: Positive correlation (0.72) - strong predictor of market direction
- **Rate Changes ↔ Sector Rotation**: RBI hike cycles favor financials, rate cuts favor IT/consumption

#### 4. Portfolio Allocation Engine
**Strategy Logic**:
IF Regime = Risk-On:
- 70% Equities | 20% Debt | 10% Commodities
- Overweight: Cyclicals, Financials, Infrastructure
- Hedge: 30% crude oil exposure for inflation

IF Regime = Risk-Off:
- 40% Equities | 50% Debt | 10% Cash
- Overweight: Defensive (IT, Pharma, FMCG)
- Increase gilt duration

IF Regime = Transition:
- 50% Equities | 40% Debt | 10% Options
- Reduce position sizes, increase hedges


**Rebalancing**: Monthly or on regime shift (whichever earlier)

---

## Key Deliverables

### Completed 
-  Regime detection HMM framework (implemented)
-  50-indicator data pipeline (scraped & cleaned)
-  Correlation analysis: crude-FX-FII inter-relationships
-  Feature engineering for macro factors

### In Progress 
-  Backtesting framework on historical data (1 year minimum)
-  Risk metrics: Sharpe ratio, max drawdown, win rate
-  Paper trading validation
-  Live strategy deployment roadmap

---

## Data Sources

| Indicator Category | Source | Frequency |
| GDP, Inflation, IIP, MOSPI Data | Ministry of Statistics & Programme Implementation | Monthly |
| Repo Rate, GSec Yields, Monetary Policy | RBI (Reserve Bank of India) | Weekly/Monthly |
| USD/INR, Forex Reserves | RBI, CEIC Data | Daily |
| Crude Oil (Brent, WTI) | CEIC, Bloomberg Terminal | Daily |
| FPI Flows, Equity Indices | NSDL, NSE India | Daily |
| NIFTY 50, Sector Indices | NSE India | Daily |

---

