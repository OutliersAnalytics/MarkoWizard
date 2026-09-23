<p align="center">
  <img src="https://raw.githubusercontent.com/OutliersAnalytics/MarkoWizard/main/assets/banner.png" alt="MarkoWizard" width="640">
</p>

<p align="center">
  <b>A modern Python library for Markowitz portfolio optimization and analysis.</b>
</p>

<p align="center">
  <a href="https://pypi.org/project/markowizard/"><img src="https://img.shields.io/pypi/v/markowizard" alt="PyPI"></a>
  <a href="https://www.python.org/downloads/"><img src="https://img.shields.io/badge/python-3.10+-blue.svg" alt="Python 3.10+"></a>
  <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT"></a>
</p>

<p align="center">
  📖 <b><a href="https://outliersanalytics.github.io/MarkoWizard/">Full documentation</a></b>
</p>

> **Previously known as _Diversificador_.** The original portfolio-analysis web app
> built with [Dash](https://dash.plotly.com/) is no longer maintained, but it is
> preserved on the [`dash-deprecated`](../../tree/dash-deprecated) branch for reference.

## Features

- **Markowitz Mean-Variance Optimization** — Compute the efficient frontier using `scipy.optimize`
- **Capital Allocation Line** — Mix risky portfolios with risk-free assets
- **Visualization** — Plotly-based charts for efficient frontier, allocation pie, CAL, correlation heatmaps, and price timelines
- **Data Fetching** — Built-in helpers for downloading market data via yfinance
- **Web Application** — FastAPI backend with a dark-themed interactive frontend

## Installation

```bash
pip install markowizard
```

That's everything the library needs: optimization (`scipy`), market-data
fetching (`yfinance`), and visualization (`plotly`). No optional extras.

## Quick Start (Library)

```python
from markowizard import MarkowitzOptimizer, CapitalAllocator
from markowizard.data import fetch_prices, compute_monthly_returns
from markowizard.visualization import efficiency_frontier_plot

# Fetch prices and compute monthly returns (decimal form, e.g. 0.01 = 1%)...
prices = fetch_prices(["AAPL", "MSFT", "GOOGL", "SPY"], period="5y")
returns = compute_monthly_returns(prices)
# ...or bring your own returns DataFrame (assets as columns).

# Optimize
optimizer = MarkowitzOptimizer(returns)
portfolios = optimizer.optimize()

# Compute Sharpe ratios (provide monthly risk-free rate)
risk_free_rate = 0.005  # 0.5% per month
portfolios = optimizer.compute_sharpe(risk_free_rate)

# Plot the efficient frontier
fig = efficiency_frontier_plot(portfolios, highlight_portfolio=50)
fig.show()

# Best portfolio (maximum Sharpe ratio)
best = optimizer.max_sharpe_portfolio()
print(best)

# Capital allocation line
allocator = CapitalAllocator(best, risk_free_rate)
cal_points = allocator.capital_allocation_line(steps=21)
```

## Web Application

An interactive web UI (FastAPI + a dark-themed frontend) lives in `backend/` and
`frontend/`. It is **not part of the PyPI package** — run it from the container
image or a clone.

### Using Docker

```bash
docker run -p 8000:8000 ghcr.io/outliersanalytics/markowizard:latest
```

### From a clone

```bash
git clone https://github.com/OutliersAnalytics/MarkoWizard
cd MarkoWizard
uv run --with-requirements backend/requirements.txt uvicorn backend.main:app --port 8000
```

Open [http://localhost:8000](http://localhost:8000) — the app auto-submits with
default tickers on load.

It exposes a single endpoint, `POST /api/analyze`; see the
[Web Application docs](https://outliersanalytics.github.io/MarkoWizard/web-app/)
for the request/response shape.

## API Reference

Full reference for every public class and function — `MarkowitzOptimizer`,
`CapitalAllocator`, the `visualization` chart functions, and the `data`
fetch helpers — lives in the
**[documentation site](https://outliersanalytics.github.io/MarkoWizard/reference/core/)**.

## Development

See [CONTRIBUTING.md](CONTRIBUTING.md) for setup instructions and contribution guidelines.

## License

MIT