This project is licensed under the [GNU General Public License v3.0](./LICENSE).


Difference-in-Differences (DiD) analysis of the Federal Reserve rate hike impact (July 2023) on Tesla (treated) vs. Microsoft (control) stock retnumpy pandas matplotlib statsmodels seaborn scikit-learn causalml yfinancens a DiD analysis evaluating the causal impact of the Fed's rate hike on July 26, 2023, on Tesla's stock returns compared to Microsoft's.

- **Objective**: Assess how the Fed rate hike affected Tesla (a growth stock) more than Microsoft (a stable stock).
- **Data Period**: January 2022 to May 2025 (41 months).
- **Treatment Event**: Fed rate hike on July 26, 2023 (month 18).

## Methodology
- **DiD Model**: OLS regression with clustered standard errors to estimate the treatment effect, controlling for confounders.
- **Confounders**:
  - P/E ratio (simulated with realistic variation).
  - EBITDA (simulated: Tesla ~$1.5B/month, Microsoft ~$10B/month).
  - VIX (market volatility).
  - 10-year Treasury yield (interest rate expectations).
  - S&P 500 returns (market-wide trends).
- **Heterogeneous Effects**: Used CausalML's T-Learner to estimate conditional average treatment effects (CATE).

## Key Findings
- **DiD Effect**: The rate hike reduced Tesla's monthly stock returns by 0.82% more than Microsoft's (SE: 0.432, p-value: 0.056).
- **Significance**: Borderline significant at the 5% level (significant at the 10% level), indicating a negative impact on Tesla consistent with economic theory.
- **Visualizations**:
  - Stock returns over time for Tesla and Microsoft.
  - Parallel trends check to validate the DiD assumption.
  - DiD summary with confidence intervals.
  - Treatment effect heterogeneity (CATE) by P/E ratio, VIX, and Treasury yield.

## Contents
- `did_tesla_msft_fed_hike_2023.ipynb`: Jupyter Notebook with the full analysis, including code, visualizations, and explanations.
- **Future Additions**:
  - README with setup instructions.
  - Data files (if external data is added).
  - Additional analyses (e.g., synthetic control method).

## Usage
- **For Presentations**: Open the notebook in Jupyter Notebook or Google Colab to view the code, outputs, and plots inline.
- **For Reuse**: Modify the notebook for other stock pairs or events by adjusting the tickers and treatment date.

## Requirements
- Python 3.7+
- Libraries: `numpy`, `pandas`, `matplotlib`, `statsmodels`, `seaborn`, `scikit-learn`, `causalml`, `yfinance`
- Install via: `pip install numpy pandas matplotlib statsmodels seaborn scikit-learn causalml yfinance`
