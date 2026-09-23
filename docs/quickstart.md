# Quick Start

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

See the [API Reference](reference/core.md) for full details on every class and function used here.
