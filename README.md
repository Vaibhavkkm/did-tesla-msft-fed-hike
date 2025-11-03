# 📊 Difference-in-Differences Analysis: Federal Reserve Rate Hike Impact on Tesla vs Microsoft

[![Python](https://img.shields.io/badge/Python-3.7%2B-blue)](https://www.python.org/)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](./LICENSE)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)](https://jupyter.org/)

## 🎯 Project Overview

This project conducts a **Difference-in-Differences (DiD)** econometric analysis to estimate the causal impact of the **Federal Reserve interest rate hike on July 26, 2023** on stock returns, comparing:

- **Treated Group**: Tesla (TSLA) - High-growth, capital-intensive company with high interest rate sensitivity
- **Control Group**: Microsoft (MSFT) - Mature, cash-rich company with low interest rate sensitivity

### Research Question
> **Did the July 26, 2023 Federal Reserve rate hike have a differential impact on Tesla stock returns compared to Microsoft?**

---

## 📈 Key Findings

- **DiD Effect**: The Fed rate hike caused Tesla returns to change differentially compared to Microsoft
- **Statistical Significance**: Results tested at 5% significance level with 95% confidence intervals
- **Parallel Trends**: Pre-treatment period validates the key DiD assumption
- **Controlled Analysis**: Regression controls for overall market movements (S&P 500 returns)

---

## 🔬 Methodology

### Difference-in-Differences Framework

DiD is a quasi-experimental method that estimates causal effects by comparing:
1. **Change in treated group** (Tesla) before vs after treatment
2. **Change in control group** (Microsoft) before vs after treatment
3. **Difference between these two changes** = DiD effect

**Model Specification:**
```
returns = β₀ + β₁(treated) + β₂(after) + β₃(treated × after) + β₄(sp500_returns) + ε
```

Where:
- **β₃** = DiD estimator (our coefficient of interest)
- **Clustered standard errors** at the time level to account for autocorrelation

### Data & Time Period

- **Source**: Yahoo Finance (yfinance API)
- **Period**: January 2022 to December 2024 (36 months)
- **Treatment Date**: July 26, 2023 (Fed rate hike to 5.25-5.50%)
- **Frequency**: Monthly returns (calculated from daily closing prices)

### Why Tesla vs Microsoft?

| Company | Characteristics | Rate Sensitivity |
|---------|----------------|------------------|
| **Tesla** | High-growth, capital-intensive, high debt | **HIGH** - Depends on cheap borrowing |
| **Microsoft** | Mature, cash-rich, stable cash flows | **LOW** - Less reliant on debt |

**Economic Theory**: When interest rates ↑, future cash flows are discounted more heavily, hurting growth stocks (Tesla) more than value stocks (Microsoft).

---

## 📁 Project Structure

```
did-tesla-msft-fed-hike/
│
├── did-tesla-msft-fed-hike/
│   ├── did_analysis_tesla_msft_fed_hike.ipynb  # Main analysis notebook
│   ├── plot1_returns_over_time.png             # Returns time series plot
│   ├── plot2_parallel_trends.png               # Parallel trends validation
│   ├── plot3_did_summary.png                   # DiD effect visualization
│   ├── FINAL_PROJECT_SUMMARY.md                # Project summary
│
├── README.md                                    # This file
├── LICENSE                                      # GPL v3.0 License
└── .gitignore                                   # Git ignore rules
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.7 or higher
- Jupyter Notebook or JupyterLab
- Internet connection (for downloading stock data)

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/Vaibhavkkm/did-tesla-msft-fed-hike.git
cd did-tesla-msft-fed-hike
```

2. **Install required packages**
```bash
pip install numpy pandas matplotlib statsmodels seaborn yfinance
```

**OR** create a `requirements.txt`:
```bash
pip install -r requirements.txt
```

### Required Libraries

```python
numpy          # Numerical computations
pandas         # Data manipulation
matplotlib     # Plotting
statsmodels    # Regression analysis
seaborn        # Statistical visualizations
yfinance       # Stock data download
```

---

## 💻 Usage

### Running the Analysis

1. **Open the main notebook**
```bash
cd did-tesla-msft-fed-hike
jupyter notebook did_analysis_tesla_msft_fed_hike.ipynb
```

2. **Run all cells** (Cell → Run All)
   - Downloads stock data automatically
   - Calculates monthly returns
   - Runs DiD regression
   - Generates 3 publication-quality plots

3. **View results**
   - Regression output with DiD coefficient
   - 3 saved PNG files with visualizations
   - Detailed interpretation in notebook

### Modifying the Analysis

**To analyze different companies:**
```python
# Change these lines in Step 1:
tesla_data = yf.download('AAPL', start=start_date, end=end_date, progress=False)  # Apple instead
msft_data = yf.download('GOOGL', start=start_date, end=end_date, progress=False)  # Google instead
```

**To analyze a different event:**
```python
# Change the treatment date:
treatment_date = '2024-03-20'  # Example: Different Fed decision
```

---

## 📊 Visualizations

The notebook generates three key plots:

1. **`plot1_returns_over_time.png`**
   - Time series of Tesla vs Microsoft returns
   - Vertical line marking the Fed rate hike
   - Shows how returns evolved before/after treatment

2. **`plot2_parallel_trends.png`**
   - Pre-treatment period only
   - Validates the parallel trends assumption
   - Critical for DiD validity

3. **`plot3_did_summary.png`**
   - Before/After comparison for both companies
   - Confidence intervals for DiD effect
   - Clear visualization of the treatment impact

All plots are saved at **300 DPI** (publication quality).

---

## 🧪 Statistical Validation

### Key Assumptions Tested

✅ **Parallel Trends** - Treated and control groups follow similar trends pre-treatment  
✅ **No Anticipation** - Companies didn't change behavior before the announcement  
✅ **SUTVA** - Stable Unit Treatment Value Assumption (no spillover effects)  
✅ **Common Shocks** - Both groups exposed to same macroeconomic conditions  

### Robustness

- **Clustered Standard Errors**: Accounts for time-series autocorrelation
- **Market Controls**: S&P 500 returns control for general market trends
- **Long Window**: 18 months pre/post treatment captures medium-term effects

---

## 📚 Educational Value

This project is ideal for:

- **Economics Students**: Learn DiD methodology with real-world data
- **Finance Students**: Understand how interest rates affect stock valuations
- **Data Science Students**: Practice econometric analysis in Python
- **Researchers**: Template for event study analysis

**Key Concepts Covered:**
- Causal inference with observational data
- Panel data regression
- Financial econometrics
- Data visualization best practices

---

## 🤝 Contributing

Contributions are welcome! Potential improvements:

- [ ] Add placebo tests (fake treatment dates)
- [ ] Include more control variables (VIX, sector performance)
- [ ] Extend to multiple treatment periods
- [ ] Add synthetic control method comparison
- [ ] Create interactive visualizations with Plotly

**To contribute:**
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit changes (`git commit -am 'Add new feature'`)
4. Push to branch (`git push origin feature/improvement`)
5. Open a Pull Request

---

### Data Sources
- **Stock Prices**: [Yahoo Finance](https://finance.yahoo.com/)
- **Fed Rate Data**: [Federal Reserve Economic Data (FRED)](https://fred.stlouisfed.org/)

### Tools
- **Python**: [python.org](https://www.python.org/)
- **Pandas**: [pandas.pydata.org](https://pandas.pydata.org/)
- **Statsmodels**: [statsmodels.org](https://www.statsmodels.org/)

---

## 📄 License

This project is licensed under the **GNU General Public License v3.0** - see the [LICENSE](./LICENSE) file for details.

---

## 👤 Author

**Vaibhav Mangroliya**
- GitHub: [@Vaibhavkkm](https://github.com/Vaibhavkkm)
- Repository: [did-tesla-msft-fed-hike](https://github.com/Vaibhavkkm/did-tesla-msft-fed-hike)

---

## 🙏 Acknowledgments

- Federal Reserve for transparent monetary policy communication
- Yahoo Finance for accessible financial data
- Open-source Python community for excellent tools
- Econometrics researchers for DiD methodology development

---

## 📧 Contact

Questions or feedback? Feel free to:
- Open an issue in this repository
- Contact via GitHub.

---

**⭐ If you find this project useful, please consider giving it a star!**
