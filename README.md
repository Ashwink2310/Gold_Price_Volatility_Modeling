# Gold Price Volatility Modeling

## TLDR
Modeled daily gold price volatility using **three approaches — ARIMA (mean-only), GARCH (conditional variance), and POMP (latent-state volatility models)**. While GARCH with Student-t innovations provided the most efficient statistical fit, **POMP models such as Heston and Regime-Switching revealed hidden volatility regimes that traditional models could not capture**. This project demonstrates how **latent-state inference uncovers deeper market structure beyond surface-level variance modeling**. Full execution requires cloud/high-memory runtime.

---

## Objective
To compare classical and latent-state volatility models on gold returns (2022–2024) and determine:

- When **simple models (ARIMA, GARCH)** suffice for forecasting
- When **advanced state-space models (POMP)** uncover **hidden structural patterns**
- How volatility regimes **persist, switch, or decay over time**

---

## Data
| Source | Description | Period | Records |
|--------|-------------|--------|---------|
| Investing.com | Daily closing price of gold | Jan 2022 – Dec 2024 | 772 |

- Converted raw price series to **log returns** for stationarity
- Verified using **ADF test** → raw prices non-stationary (p = 0.68), log-returns stationary (p = 0.01)

---

## Models Compared

| Model Type | Model | Strength |
|------------|--------|----------|
| Mean-only | ARIMA(2,0,2) | Captures autocorrelation but no volatility dynamics |
| Conditional variance | GARCH(1,1) — Gaussian / Student-t | Captures clustering; Student-t absorbs heavy tails |
| Latent-state | Heston POMP | Models **continuous stochastic volatility path** |
| Latent-state | Regime-Switching POMP | Reveals **discrete high vs low volatility phases** |

---

## Key Result

| Model | Log-Likelihood | Insight |
|--------|----------------|---------|
| ARIMA | 2525.8 | Misses volatility entirely |
| GARCH(1,1) — t | **2543.4** | Best *statistical efficiency* |
| Heston POMP | 2536.8 | Smooth latent volatility curve |
| Regime-Switch POMP | 2539.7 | Clear **high vs low volatility states** |

**GARCH-t is best for raw accuracy**  
**POMP is best for *interpreting hidden behavior*** → Regime-Switching revealed **asymmetric persistence**, with high-volatility periods lasting longer than calm ones

---

## Takeaway
**GARCH-t wins on fit, but POMP wins on interpretability** — making it the preferred model when *understanding* volatility behavior matters more than *blind prediction*.

---

## Future Extensions
- Apply **asymmetric EGARCH or GJR-GARCH** to capture leverage effects
- Incorporate **macroeconomic covariates** (inflation, VIX, interest rates)
- Use **particle filtering forecasts for risk simulation**
