# Statistical-Arbitrage---Cointegration-Based-Pairs-Trading-Strategy  
"Develop a mean-reversion pairs trading model using Engle–Granger Cointegration Test on AMZN–GOOG to detect equilibrium relationships and generate Z-score driven entry/exit signals for profitable opportunities."

# Dataset  
 path = kagglehub.dataset_download("borismarjanovic/price-volume-data-for-all-us-stocks-etfs") 

# **Statistical Arbitrage**  
**Statistical Arbitrage** is a quantitative trading strategy that identifies mispricings between related assets based on statistical relationships rather than fundamental analysis.  
This project implements a **cointegration-based mean reversion model** using **Amazon (AMZN)** and **Google (GOOG)** stock data to capture temporary deviations from equilibrium and profit when prices revert to their long-term relationship.  

The strategy combines econometric modeling and backtesting techniques to analyze cointegration and test the reliability of the trading signals.

---

### 1. **Cointegration Analysis**
Cointegration determines whether two or more non-stationary time series share a stable, long-term equilibrium relationship.  
In this project, the **Engle–Granger Two-Step Method** is used:

- **Step 1:** Regress AMZN on GOOG using Ordinary Least Squares (OLS) to estimate the **hedge ratio (β)**.  
- **Step 2:** Apply the **Augmented Dickey-Fuller (ADF)** test on the regression residuals to confirm stationarity.  

If the residuals are stationary (p-value < 0.05), the series are considered cointegrated.  

**Result:** p-value = **0.0297** → Reject null hypothesis → AMZN and GOOG are cointegrated.  

This confirms that deviations between the two stocks are temporary and tend to revert, enabling a mean-reversion-based trading approach.

---

### 2. **Hedge Ratio and Spread Calculation**
The **hedge ratio (β)** defines how much of one asset to hold relative to another to maintain neutrality in the portfolio.  

- The spread is computed as:  
  \[
  \text{Spread}_t = \text{AMZN}_t - β \times \text{GOOG}_t
  \]

- Once the spread is calculated, rolling statistics such as **mean (μ)** and **standard deviation (σ)** are used to measure deviations from equilibrium.  

---

### 3. **Signal Generation**  
Trading signals are derived using the **Z-score** of the spread:  
\[
Z_t = \frac{\text{Spread}_t - μ_t}{σ_t}
\]

The Z-score identifies how far the current spread is from its historical mean in standard deviation units.  

**Entry/Exit Rules:**
- **Long Position:** Enter when Z < -1 (expect spread to increase)  
- **Short Position:** Enter when Z > +1 (expect spread to decrease)  
- **Exit:** Close position when |Z| < 0.25 (spread reverts to equilibrium)  

This method ensures trades are taken only when deviations are statistically significant, reducing noise and false signals.

---

### 4. **Backtesting**
Backtesting was performed using a **rolling-window approach** to simulate real trading conditions.  
Performance metrics such as **Cumulative Returns**, **Sharpe Ratio**, and **Win Rate** were used to evaluate profitability and robustness.  

Additionally, **regime stability analysis** was conducted to ensure the strategy performs consistently under different market conditions (e.g., bullish, bearish, or volatile regimes).  

---

### 5. **Results**
- Cointegration confirmed between **AMZN** and **GOOG** with p-value = **0.0297**.  
- Estimated hedge ratio: **β = 1.6161**.  
- Strategy demonstrated stable and mean-reverting behavior during backtesting.  
- The spread consistently reverted to equilibrium, validating the model’s robustness.  

---

### 6. **Key Concepts**
- **Cointegration:** Statistical property of two time series that share a long-term equilibrium relationship.  
- **Hedge Ratio (β):** Determines the proportion of one asset to another for neutral exposure.  
- **Z-Score:** Measures deviation of spread from its historical mean in standard deviation units.  
- **Mean Reversion:** The assumption that asset prices tend to revert to their equilibrium over time.  
- **Backtesting:** Simulating strategy performance on historical data to test effectiveness.  

---

### 7. **Tech Stack**
- **Programming Language:** Python  
- **Libraries Used:** `pandas`, `numpy`, `statsmodels`, `matplotlib`, `yfinance`, `scipy`  
- **Development Environment:** Jupyter Notebook / VS Code  

---

### 8. **Applications**
- **Pairs Trading:** Exploit relative price movements between two cointegrated assets.  
- **Market-Neutral Strategies:** Generate profits independent of market direction.  
- **Quantitative Research:** Validate statistical relationships for risk-managed trading systems.  

---

### 9. **Future Work**
- Extend strategy to multiple pairs for **portfolio-level optimization**.  
- Integrate **transaction cost modeling** for realistic profit estimation.  
- Explore **Kalman Filter** and **Machine Learning-based** adaptive hedge ratios.  

---

 
 
