# Next‑day directional signal across

## Objective
Transform daily ratings/indicators into **next-day directional signals** for 8 assets (30 trading days each).  
Build and validate a simple predictive model, report precision/recall, and evaluate a **practical decision metric** — the average next-day return of predicted buy signals.

---

## Approach
1. **Data:** 8 assets × 30 days from [Stooq.com](https://stooq.com).  
2. **Feature Engineering:**
   - 1-day and 3-day returns (`ret_1`, `ret_3`)
   - 3-day and 5-day moving averages and their difference (`ma_diff`)
   - 3-day momentum (`momentum_3 = Close / MA₃ − 1`)
   - Relative volume (`rv_3 = Volume / MA₃(Volume) − 1`)
   - 5-day rolling volatility (`vol_5`)
3. **Label:** `y_dir = 1` if next-day close > current close, else 0.
4. **Models:** Logistic Regression and Random Forest (300 trees).
5. **Validation:** Rolling (walk-forward) split across 6 test dates.
6. **Metrics:**
   - Precision, Recall, F1
   - Average next-day return per predicted long signal (economic metric)
7. **Visualization:** Precision/Recall trends, Confusion Matrix, PR Curve, Feature Importance, and Cumulative P&L.

---

## Key Results
| Metric | Logistic Regression | Random Forest |
|:-------:|:-------------------:|:--------------:|
| **Precision** | ~0.38 | **0.41** |
| **Recall** | 0.46 | **0.49** |
| **F1 Score** | 0.39 | **0.41** |
| **Avg Return per Signal** | 0.0028 | **0.0033** |
| **Avg Signals per Test Day** | 3.5 | **3.8** |

The **Random Forest** model provided the best overall trade-off between accuracy and signal profitability.

---

## Insights
- Simple, interpretable features can still yield predictive power in short time windows.
- Nonlinear methods (Random Forest) slightly outperform linear baselines (Logistic Regression).
- A ~0.3% mean next-day return per signal is directionally promising but not sufficient without cost modeling.
- Expanding the dataset and tuning thresholds could improve robustness.

---

## Limitations
- 30-day window → small sample, noisy metrics.
- Transaction costs and slippage ignored.
- Signals evaluated independently (no portfolio optimization).
- Only long signals considered (no shorts).

---

## Next Steps
1. Extend dataset (3–6 months of daily data).
2. Include cost model and Sharpe/Drawdown metrics.
3. Calibrate thresholds for target precision or expected return.
4. Experiment with boosting and temporal models (XGBoost, LSTM, TCN).
5. Add sector or market index features for contextual awareness.

---

**Author:** Maung Thu Ra 
**Date:** November 8th, 2025 
**Contact:** https://www.linkedin.com/in/maung-thu-ra/  