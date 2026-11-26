# Weather Report

**Is the climate really changing where we live?**

This project fetches and analyses decades of historical daily weather data for a set of cities with different climates, in order to uncover long-term temperature trends, anomalies and changes in extreme events.


## Research questions

1. **Warming trend:** how much has the average temperature of each city changed since 1940, and how fast is it changing per decade?
2. **Extreme heat:** have heatwaves become more frequent and longer over time?
3. **Precipitation:** have heavy-rainfall days become more frequent?
4. **Seasons and regions:** how do the seasonal cycles differ between cities in different climate zones?

## Cities

| City | Country | Climate | Latitude | Longitude |
|---|---|---|---|---|
| Milan | Italy | Humid subtropical | 45.46 | 9.19 |
| Cairo | Egypt | Hot desert | 30.04 | 31.24 |
| Singapore | Singapore | Tropical rainforest | 1.35 | 103.82 |
| Reykjavik | Iceland | Subpolar oceanic | 64.15 | -21.94 |
| Sydney | Australia | Humid subtropical (southern hemisphere) | -33.87 | 151.21 |

The period analysed is **1940 to 2025**.

## Data source

Historical daily weather data comes from the free
[Open-Meteo Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api). The variables used are:

- daily maximum, minimum and mean temperature (`temperature_2m_max`, `temperature_2m_min`, `temperature_2m_mean`)
- daily precipitation sum (`precipitation_sum`)

The first run downloads the data and caches it locally as CSV files in `data/`, so later runs do not call the API again. The `data/` folder is not tracked by Git.

## Methodology

- **Cleaning and aggregation** (`pandas`): parse dates, handle missing values, aggregate daily data to monthly, seasonal and annual values.
- **Temperature anomalies:** difference from the 1961-1990 climatological baseline of each city.
- **Trend estimation** (`scipy`): linear regression of annual mean temperature against year, reported in °C per decade with its p-value.
- **Heatwaves:** at least 3 consecutive days with maximum temperature above the 95th percentile of the baseline period for that calendar day. Counted per year.
- **Heavy rainfall:** days with precipitation above the 95th percentile of wet days in the baseline period. Counted per year.

## Visualisations

- Temperature anomaly time series with trend line
- Heatmap of monthly average temperatures
- Warming stripes per city
- Comparison of cities
- Heatwave and heavy-rain frequency per decade

All figures are saved in `figures/`.

## Project structure

```
89220A_weatherReport/
├── src/weather/
│   ├── __init__.py
│   ├── data.py          # API access, error handling, local caching
│   ├── processing.py    # cleaning and aggregation with pandas
│   ├── analysis.py      # anomalies, trends, extreme events
│   └── plots.py         # plotting functions
├── notebooks/
│   └── analysis.ipynb   # presentation notebook (uses the package code)
├── tests/               # unit tests
├── figures/             # generated plots
├── data/                # cached data (not tracked by Git)
├── app.py               # Streamlit web app
├── requirements.txt
└── README.md
```

## Requirements

- Python 3.10 or newer
- Libraries listed in `requirements.txt`: `requests`, `pandas`, `numpy`, `scipy`, `matplotlib`, `seaborn`, `streamlit`, `pytest`

## Setup

```bash
git clone https://github.com/Saifi99/89220A_weatherReport.git
cd 89220A_weatherReport
python -m venv .venv
```

Activate the virtual environment:

- Windows (PowerShell): `.venv\Scripts\Activate.ps1`
- macOS / Linux: `source .venv/bin/activate`

Install the dependencies:

```bash
pip install -r requirements.txt
```

## Usage

Run the notebook:

```bash
jupyter notebook notebooks/analysis.ipynb
```

Run the Streamlit app:

```bash
streamlit run app.py
```

Run the tests:

```bash
pytest
```

## Results

*To be completed at the end of the project: main findings, trend per decade for each city, and heatwave frequency changes.*
