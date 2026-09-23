# Web Application

An interactive web UI (FastAPI + a dark-themed frontend) lives in `backend/` and
`frontend/`. It is **not part of the PyPI package** — run it from the container
image or a clone.

## Using Docker

```bash
docker run -p 8000:8000 ghcr.io/outliersanalytics/markowizard:latest
```

## From a clone

```bash
git clone https://github.com/OutliersAnalytics/MarkoWizard
cd MarkoWizard
uv run --with-requirements backend/requirements.txt uvicorn backend.main:app --port 8000
```

Open [http://localhost:8000](http://localhost:8000) — the app auto-submits with
default tickers on load.

## API

It exposes a single endpoint, `POST /api/analyze`:

```json
{
  "tickers": ["AAPL", "MSFT", "GOOGL", "SPY"],
  "period": "5y",
  "risk_free_rate": 0.005
}
```

which returns the efficient frontier, max-Sharpe portfolio, capital-allocation-line
points, and correlation matrix as JSON. The frontend renders the charts.
