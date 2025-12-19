# Predicting a Server’s CPU Utilization Rate from Network Indicators

This project designs, explains, and evaluates a **regression model** that predicts a server’s **CPU load** using network indicators.  
The work is framed in a **Security Operations Center (SOC)** scenario to help **anticipate overloads** (e.g., DDoS-like traffic bursts) and detect **abnormal behavior** before it impacts service availability.

---

## Dataset (Network Logs)

Each observation corresponds to a **time interval** and includes:

- `tcp_connections`: number of active TCP connections  
- `data_volume_MB`: transmitted data volume (MB)  
- `packet_loss_rate`: packet loss rate (%)  
- `ids_alerts`: number of IDS alerts  
- `cpu_load`: CPU load, **target variable to predict**

> The dataset is realistically simulated with noise and CPU spikes to mimic real SOC monitoring conditions.

---

## Methodology (Advanced Linear Regression Pipeline)

1. **Understanding the context**
   - Clarify the SOC objective: predict server CPU load from network signals.
   - Distinguish explanatory variables from the target.

2. **Data simulation and import**
   - Load the simulated dataset (`cpu_load_data.csv`).
   - Inspect structure and first rows (`df.head()`).

3. **Exploration and preprocessing**
   - Global overview: descriptive statistics, data types, missing values.
   - Correlation analysis between predictors and `cpu_load`.
   - Feature standardization (mean 0, variance 1) to make variables comparable.

4. **Train/Test split**
   - Split data into training and testing sets (80% / 20%).
   - Verify final dataset shapes.

5. **Feature selection**
   - Apply **Sequential Feature Selection (forward)** using linear regression.
   - Keep the most relevant features for prediction.

6. **Modeling and evaluation**
   - Fit a baseline **Linear Regression** on selected features.
   - Evaluate via:
     - **R²** (goodness of fit),
     - **RMSE** (root mean squared error),
     - **MAE** (mean absolute error),
     - Visualization of predicted vs. actual values.

7. **Model improvement**
   - Add interaction/non-linear terms with **PolynomialFeatures (degree=2)**.
   - Retrain and compare performance (R², RMSE, MAE).
   - Residual diagnostics + Shapiro-Wilk normality test.

8. **Conclusion and recommendations**
   - Identify which network indicators most influence CPU load.
   - Discuss SOC interpretations and potential alerting use cases.

---

## Project Structure
```
Prediction_CPU_Load/
├── Data/
│ └── cpu_load_data.csv
├── Notebook/
│ └── cpu_load_prediction.ipynb
├── README.md
└── requirements.txt
```

## How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/AdamBelbaraka/Prediction_CPU_Load.git
   cd Prediction_CPU_Load

2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

2. **Run the notebook**
   ```bash
   jupyter notebook Notebook/cpu_load_prediction.ipynb
   ```
Make sure the dataset stays in Data/cpu_load_data.csv and the notebook is run from the Notebook/ folder.

3. **System Requirements**

- Python 3.x
- pandas, numpy
- matplotlib, seaborn
- scikit-learn
- scipy

## Author

Adam Belbaraka
Cybersecurity engineering student

## License

feel free to use, modify, and share.
