# Hunza Valley Climate Trend Analysis (2000–2025)

## Project Overview

This repository provides a longitudinal climate study of the Hunza region in the Karakoram Range. By analyzing 25 years of historical weather data, this research quantifies the rate of warming and identifies significant baseline shifts that impact glacial stability and regional water security.
## Core Quantitative Results

The analysis utilizes Ordinary Least Squares (OLS) regression and rolling window averages to identify the following climate signals:
  
Parameter               	     Observed Value

**Decadal Warming Rate**    	**+2.53°C per decade**
**Aggregate Baseline Shift**	**+4.54°C (Comparing 2000–2015 to 2016–2025)**
**Temporal Coverage**       	**Jan 1, 2000 – Dec 31, 2025**
**Data Granularity**        	**Daily Mean/Max/Min Temperatures**

## Methodology
### 1. Signal Processing and Smoothing

To mitigate seasonal volatility and high-frequency "noise" inherent in daily high-altitude weather data, a 365-day centered moving average was applied. This ensures that each data point represents a balanced annual cycle, allowing for the observation of the long-term climate trajectory.

### 2. Regression Analysis

Linear trends were calculated using the Scikit-Learn `LinearRegression` model. The trendline is defined by the following equation:

     $y = mx + b$

Where:

    y: Smoothed temperature (°C)

    x: Ordinal date representation

    m: Derived slope (converted to °C/decade for reporting)

### 3. Epoch Comparison

The dataset was bifurcated into two distinct periods—2000–2010 and 2016–2025—to analyze the acceleration of warming. This comparative approach reveals a significant increase in both the mean temperature and the slope of warming in the most recent decade.

## Installation
```Bash
git clone https://github.com/arkalibaig/hunza-climate-analysis.git
cd hunza-climate-analysis
pip install -r requirements.txt```

## Usage
Execute the Jupyter Notebook analysis.ipynb to regenerate the plots and statistical outputs.

## Directory Structure
```text
hunza-climate-analysis/
├── scraper/            # Python script to scrape data
├── analysis/           # Jupyter notebook for analysis and visualization
├── data/               # CSV dataset used for analysis
├── figures/            # Plots and charts generated from analysis
├── README.md           # Project overview
├──requirements.txt     #Python dependencies
├──.gitignore           #Files/folders to ignore in Github
```
## Data Source

Weather data provided by the Open-Meteo Historical Weather API, covering coordinates for the Hunza Valley region at multiple elevations.
