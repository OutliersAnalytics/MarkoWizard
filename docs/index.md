<p align="center">
  <img src="assets/banner.png" alt="MarkoWizard" width="640">
</p>

**A modern Python library for Markowitz portfolio optimization and analysis.**

[![PyPI](https://img.shields.io/pypi/v/markowizard)](https://pypi.org/project/markowizard/)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

!!! note "Previously known as _Diversificador_"
    The original portfolio-analysis web app built with [Dash](https://dash.plotly.com/)
    is no longer maintained, but it is preserved on the
    [`dash-deprecated`](https://github.com/OutliersAnalytics/MarkoWizard/tree/dash-deprecated)
    branch for reference.

## Features

- **Markowitz Mean-Variance Optimization** — Compute the efficient frontier using `scipy.optimize`
- **Capital Allocation Line** — Mix risky portfolios with risk-free assets
- **Visualization** — Plotly-based charts for efficient frontier, allocation pie, CAL, correlation heatmaps, and price timelines
- **Data Fetching** — Built-in helpers for downloading market data via yfinance
- **Web Application** — FastAPI backend with a dark-themed interactive frontend

## Where to go next

- [Installation](installation.md) — install the library or run the web app
- [Quick Start](quickstart.md) — optimize a portfolio in a few lines of Python
- [Web Application](web-app.md) — run the interactive dark-themed UI locally or via Docker
- [API Reference](reference/core.md) — full reference for every public function and class
- [Contributing](contributing.md) — set up a dev environment and submit changes

## Modules

| Module | Description |
|---|---|
| [`core`](reference/core.md) | `MarkowitzOptimizer` — efficient frontier optimization |
| [`allocation`](reference/allocation.md) | `CapitalAllocator` — risk-free asset allocation |
| [`visualization`](reference/visualization.md) | Plotly chart functions (efficient frontier, pie, CAL, correlation) |
| [`data`](reference/data.md) | Market-data fetching and monthly-return helpers (yfinance) |

The web application (`backend/`, `frontend/`) is kept in the repo but is not
part of the installable package — see [Web Application](web-app.md).
