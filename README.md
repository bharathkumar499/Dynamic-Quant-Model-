# Dynamic-Quant-Model-
This repository implements a Quantitative Trading System for Indian stock markets using sector-based dynamic portfolio rotation strategies. It integrates custom signal generation, optimization techniques, risk management, and backtesting across multiple market regimes (2018–2025).

📂 Project Structure
sector-rotator/
├── backtest/
│   └── run_backtest.py            # Simulates portfolio equity curve with stops
├── scripts/
│   ├── generate_flags.py          # Sector signal + macro overlay (index filter)
│   └── run_optimizer.py           # Dynamic portfolio optimizer (MVO)
│   └── analyze_backtests.py       # Final performance, regime & benchmark analysis
├── signals/
│   ├── tech_rubberband.py         # RSI Reversal for TECH
│   ├── fmcg_turnofmonth.py        # Breakout filter for FMCG
│   └── bank_momentum.py           # SMA crossover for BANK
├── optimizer/
│   └── rule_based.py              # Mean-Variance Optimization with long/short
├── metadata/
│   └── selected_current.yaml      # Sector-to-stock mapping
├── data/
│   ├── raw/                       # Historical OHLCV stock data
│   ├── indices/                   # Nifty sector index data (e.g., CNXIT)
│   ├── signals/                   # Buy/Short signal flags
│   ├── weights/                   # Allocation weights per day
│   └── backtest/                  # Portfolio value and rolling returns
└── report/
    ├── rolling_30d_return.png     # Visual return analysis
    └── benchmark_vs_portfolio.png # Cumulative return vs Nifty 50
Features
Sector-Specific Signals
Each sector has a custom strategy:

TECH → RSI Reversal (RSI(2) < 30)
FMCG → Breakout filter using ATR-based lower band
BANK → SMA(20) > SMA(63) momentum strategy
Long/Short Support
Signal values:

1 → Long
-1 → Short
0 → No position
Dynamic Portfolio Optimization
Implements Mean-Variance Optimization (MVO) per day:

Allocation across active signals
Bounds: -0.5 to +0.5 per sector
Ensures exposure across atleast 2 sectors where possible
Risk Management
Stop-loss via drawdown-based cash switching
Adaptive Drawdown Limit (based on rolling volatility)
Sector Cap: Max 50% per sector
Trailing Stop and breakeven logic
Supports both gross leverage control and capital scaling
Backtesting Engine
Realistic equity simulation using sector-wise allocations
Handles flat exposure days and capital preservation
Computes rolling returns, portfolio curve, risk overlays
Performance Evaluation
CAGR, Sharpe Ratio, Max Drawdown
VaR, CVaR, Win/Loss ratio
Alpha/Beta vs Nifty 50
Regime-wise CAGR for:
IL&FS Bear
Pre-COVID Bull
COVID Crash
Post-COVID Bull
Rate Hike Bear
Recent Bull
🛠️ How to Run
1. Download Stock + Index Data
Ensure data is placed in data/raw/ and index files in data/indices/.

2. Generate Sector Flags
python scripts/generate_flags.py
3. Run Optimizer
python scripts/run_optimizer.py
4. Simulate Backtest
python backtest/run_backtest.py
5. Analyze Results
python scripts/analyze_backtests.py
Capital Assumption
Initial Capital: ₹10,00,000
Final portfolio equity computed based on cumulative return
Plots saved under report/
Future Enhancements (Optional Ideas)
ML models (LSTM, news sentiment) for signal enhancement
Regime classification using unsupervised learning
Sector ETF overlay for execution simulation
Real-time deployment using broker API
