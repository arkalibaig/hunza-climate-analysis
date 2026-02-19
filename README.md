# Hunza Valley Climate Trend Analysis (2000–2025)

## Project Overview

This repository provides a longitudinal climate study of the Hunza region in the Karakoram Range. By analyzing 25 years of historical weather data, this project quantifies an apparent warming trend and — critically — investigates a structural anomaly in the data that raises important questions about the reliability of reanalysis datasets in high-altitude regions.

> **Note:** After initial publication, a significant data limitation was identified that affects the interpretation of results. See the [Data Limitations](#data-limitations-and-revised-interpretation) section before drawing conclusions from the quantitative outputs.

---

## Observed Quantitative Results

The analysis uses OLS regression and rolling window averages to identify the following signals:

| Parameter | Observed Value |
|---|---|
| **Decadal Warming Rate** | **+2.53°C per decade** |
| **Aggregate Baseline Shift** | **+4.54°C (2000–2015 vs. 2016–2025)** |
| **Temporal Coverage** | Jan 1, 2000 – Dec 31, 2025 |
| **Data Granularity** | Daily Mean/Max/Min Temperatures |

---

## Data Limitations and Revised Interpretation

### The Problem

The apparent warming rate of ~2.53°C per decade should be interpreted with significant caution. Open-Meteo historical data for the Hunza region is derived from reanalysis models such as ERA5 rather than a physical weather station, meaning it represents grid-based interpolated estimates rather than direct measurements. Hunza's extreme altitude variation — spanning valleys at ~1500m to peaks above 5000m — makes accurate single-grid-cell representation particularly challenging.

More critically, a structural break in the temperature trend is visible around 2015–2016. This coincides with known transitions between underlying datasets in reanalysis APIs, where older ERA5 data may be stitched with more recent model outputs using updated physics or changed spatial resolution. This kind of backend dataset discontinuity can introduce artificial baseline shifts that mimic real warming signals.

A genuine 4.5°C temperature increase over 25 years would imply catastrophic glacier collapse and ecological transformation at a scale that is not corroborated by existing literature on the Hindu Kush-Karakoram region. This physical implausibility strongly suggests the observed shift is at least partly a data artifact introduced by a model revision around 2016, rather than pure climate acceleration.

### Revised Conclusion

An apparent warming rate of ~2.53°C per decade was observed using Open-Meteo historical data. However, a structural break around 2016 suggests possible dataset discontinuity, highlighting the limitations of grid-based reanalysis data in high-altitude regions. The true warming signal for Hunza, while real and concerning, is likely masked by this artifact and cannot be reliably quantified from this dataset alone without cross-validation against physical station data or a consistent single reanalysis product.

### What This Project Demonstrates

Rather than invalidating the work, this finding reframes the project's value. Identifying, documenting, and explaining a data discontinuity is itself a meaningful analytical contribution — and a cautionary example of why reanalysis data in complex mountain terrain requires careful critical evaluation before being taken at face value.

---

## Methodology

### 1. Signal Processing and Smoothing

To mitigate seasonal volatility in daily high-altitude weather data, a 365-day centered moving average was applied. This ensures each data point represents a balanced annual cycle, enabling observation of the long-term climate trajectory.

### 2. Regression Analysis

Linear trends were calculated using Scikit-Learn's `LinearRegression`. The trendline follows:

```
y = mx + b
```

Where `y` is smoothed temperature (°C), `x` is the ordinal date, and `m` is the slope converted to °C/decade for reporting.

### 3. Epoch Comparison

The dataset was split into two periods — 2000–2015 and 2016–2025 — to analyze the apparent acceleration of warming. The breakpoint at 2016 was initially interpreted as climate acceleration but is now identified as a likely data discontinuity boundary.

---

## Installation

```bash
git clone https://github.com/arkalibaig/hunza-climate-analysis.git
cd hunza-climate-analysis
pip install -r requirements.txt
```

## Usage

Execute `analysis/analysis.ipynb` to regenerate plots and statistical outputs.

## Directory Structure

```
hunza-climate-analysis/
├── scraper/        # Python script to fetch data from Open-Meteo
├── analysis/       # Jupyter notebook for analysis and visualization
├── data/           # CSV dataset
├── figures/        # Generated plots and charts
├── README.md
├── requirements.txt
└── .gitignore
```

## Data Source

Weather data sourced from the [Open-Meteo Historical Weather API](https://open-meteo.com/), covering coordinates for the Hunza Valley region. Open-Meteo primarily uses ERA5 reanalysis data for historical periods, blended with more recent forecast model outputs — a stitching methodology that can introduce the structural discontinuities discussed above.

## License

MIT
