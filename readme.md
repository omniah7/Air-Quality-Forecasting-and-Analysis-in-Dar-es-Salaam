## ⚙️ Installation & Setup

To run this notebook locally, you need to have Python and Jupyter installed.

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/<your-username>/Air_Quality_in_Dar_es_Salaam_TZ.git
    cd Air_Quality_in_Dar_es_Salaam_TZ
    ```

2.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```
3. **Install the required dependencies:**
    ```bash
    pip install pandas numpy seaborn matplotlib statsmodels scikit-learn jupyter
    ```
4.  **Launch Jupyter Notebook:**
    ```bash
    jupyter notebook
    ```
    Navigate to and open `Air_Quality_in_Dar_es_Salaam_TZ.ipynb`.

## 🚀 Usage

1.  **Run the Notebook:** Execute the cells in `Air_Quality_in_Dar_es_Salaam_TZ.ipynb` sequentially.
2.  **Data Loading:** Ensure the raw data files are in the same directory as your notebook (`january_2018_sensor_data_archive.csv`, etc.).
3.  **Follow the Analysis:** The notebook guides you through data inspection, cleaning, visualization, and time series modeling.
4.  **Output:** The final output of the data wrangling process is a cleaned, resampled time series of hourly average PM2.5 values, stored in the variable `clean_data`.
5.  **Model Results:** The project builds a baseline ARIMA model. The results, including model performance metrics, are discussed in the final cells of the notebook.

## 📊 Data Sources

The analysis uses air quality sensor data collected in **Dar es Salaam, Tanzania, from January to March 2018** from [OpenAfrica](https://open.africa/) website. The data includes measurements from multiple sensors (`SDS011` for particulate matter, `DHT22` for humidity) and various value types (`P1`, `P2`, `humidity`).

## 🔍 Code Overview / Walkthrough

### 1. Overview
This project aims to predict the concentration of **PM2.5** (particulate matter with diameters less than or equal to 2.5 micrometers) in the air of Dar es Salaam using a Time Series Forecasting approach.

### 2. Data Loading
The project starts by loading three months of sensor data. Each file is read into a Pandas DataFrame with the `timestamp` column set as the index and parsed as datetime objects.
*   **Key Insight:** The initial dataset contains over 346,000 entries with 7 columns, including `sensor_type`, `value_type` (P1, P2, humidity), `location`, and `value`.

### 3. Data Wrangling
The core data preparation is done by the `wrangle()` function, which:
*   **Filters** for `P2` (PM2.5) readings.
*   **Converts** the timezone to 'Africa/Dar_es_Salaam'.
*   **Drops** all columns except `value`, renaming it to `P2`.
*   **Removes outliers** (values above 500 µg/m³).
*   **Resamples** the data to a **1-hour frequency** using the mean, forward-filling any missing gaps.
*   **Result:** A clean Pandas Series with 2160 hourly data points ready for analysis and modeling.

### 4. Exploratory Data Analysis (EDA)
A boxplot is generated to visualize the distribution of PM2.5 values and confirm the removal of extreme outliers after the cleaning process.

### 5. Modeling and Evaluation
*   **Model Choice:** An ARIMA model was implemented to forecast future PM2.5 values.
*   **Validation:** A robust **walk-forward validation** technique was used to simulate real-world forecasting and evaluate performance fairly.
*   **Results:** The baseline ARIMA model achieved a **Mean Absolute Error (MAE) of 3.15 µg/m³**. This result, which represents an error of ~36% relative to the mean value, establishes a performance baseline. It highlights the challenge of forecasting this specific dataset and the potential need for more complex models or additional features, as explored in the Future Work section.

## 🔮 Future Work / Potential Improvements

The ARIMA model serves as a solid baseline. To improve forecasting accuracy beyond the achieved MAE of 3.15 µg/m³, the following suggestions are considered:

*   **Model Sophistication:** Experiment with models better suited for complex seasonality:
    *   **SARIMA:** To explicitly capture daily and weekly seasonal patterns.
    *   **Machine Learning (XGBoost):** Using engineered features like hour of day, day of week, and lagged variables.
*   **Incorporate External Features:** Enhance forecasts by integrating weather data (e.g., temperature, humidity, wind speed, pressure), which significantly influences pollution dispersion.
*   **Comprehensive EDA:** Dive deeper into the data by analyzing autocorrelation (ACF/PACF plots) and cross-correlations between different pollutants (`P1` and `P2`) and humidity to inform feature engineering.

## 👤 Author

**Omniah Arafah**
*   GitHub: [@omniah7](https://github.com/omniah7)
*   LinkedIn: [OmniahArafah](www.linkedin.com/in/omniah-arafah)

---