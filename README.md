# Fed Rate Hikes: Growth vs Value Analysis (2022-2023)

I built this project to dig deeper into the 2022-2023 Federal Reserve hiking cycle. Everyone knows "rates up, stocks down," but I wanted to quantify *how much* and *where* the pain was felt most. Specifically, I looked at the divergence between **Growth stocks** (like Tesla, Nvidia, ARKK) and **Value stocks** (like Microsoft, Berkshire Hathaway, Energy sector).

It's not just about price drops; it's about volatility regimes and structural breaks in the market.

## What's Inside

I moved beyond simple price comparisons and implemented a few rigorous financial models to get real answers:

### 1. Event Study Analysis
I used the standard **MacKinlay (1997)** event study methodology to isolate the impact of **11 major rate hikes** (March 2022 - July 2023).
*   **Window:** Analyzed returns in a short window (+/- 5 days) around each FOMC announcement.
*   **Result:** You can clearly see the "abnormal returns" drift significantly for Growth stocks compared to the broader market immediately following the announcements.

### 2. Volatility Modeling (GARCH)
Price tells one story, risk tells another. I implemented an **EGARCH(1,1)** model (Exponential GARCH) with a Student's t-distribution to model the time-varying volatility of high-beta assets like TSLA and NVDA.
*   **Why?** Standard volatility models assume normal distribution, but these stocks have "fat tails" (extreme moves). EGARCH captures the leverage effect (volatility spikes more when prices drop).
*   **Insight:** When the model's conditional volatility hits certain thresholds (e.g., >4.0), it serves as a quantitative signal to cut position sizing, regardless of the news cycle.

### 3. Price Forecasting (LSTM)
Just for fun (and science), I trained a **Long Short-Term Memory (LSTM)** neural network to see if it could pick up on the non-linear patterns in the Growth Index.
*   **Architecture:** Multi-layer LSTM with Dropout regularization to prevent overfitting.
*   **Input:** Scaled time-series data of the custom Growth Index.
*   **Output:** Next-day price predictions (plotted against actuals to visualize the lag/accuracy).

---

## The "So What?"

This analysis basically confirms the **Duration Risk** theory in finance:
*   **Growth Stocks** are "long duration" assets. Their value comes from cash flows far in the future. When rates rise, the discount factor crushes their present value disproportionately.
*   **Value Stocks** are "short duration." They have cash flows *now*, making them far more resilient (and in some cases, like Energy, correlated positively) to inflation and rate hikes.

## How to Run It

Everything is in the Jupyter notebook `fed_rate_hike_impact_analysis.ipynb`.

1.  Clone the repo.
2.  Install the dependencies:
    ```bash
    pip install -r requirements.txt
    ```
3.  Run the notebook. It triggers a fresh download of data from Yahoo Finance, so you're always analysing up-to-date price action.

## Tech Stack
*   **Python** (Pandas, NumPy) for the heavy lifting.
*   **Statsmodels** for the regression and t-tests.
*   **arch** library for the volatility modeling.
*   **TensorFlow/Keras** for the LSTM deep learning part.
*   **Matplotlib/Seaborn** for the charts.
