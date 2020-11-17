[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/TomMonks/swast-forecast-tool/master) [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.4277723.svg)](https://doi.org/10.5281/zenodo.4277723) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) [![Python 3.6+](https://img.shields.io/badge/python-3.6+-blue.svg)](https://www.python.org/downloads/release/python-360+/)

# SWAST Ensemble Forecast Tool

A forecasting tool for SWAST. Implemented in Python.

## Aims: 

The tool predicts the number of calls that result in the dispatch of one or more ambulances. 

## Methods:

Forecasting is an ensemble of Regression with ARIMA Errors and FBProphet.  The regression model and prophet explicitly model new year's day as a holiday.

## Dependencies and running the tutorial

All dependencies are contained in the binder/environment.yml.  It is recommended that the user first install conda (via Anaconda).  Once installed open a terminal (or Anaconda Prompt on windows), navigate to the swast-forecast-tool directory and run the following command to create the `swast_forecast` virtual environment.

* `conda env create -f binder/environment.yml`

To activate the virtual environment run the following command:

* `conda activate swast_forecast`

The virtual environment includes Jupyter-Lab.  To load it run the following command (or open from Anaconda Navigator):

* `jupyter-lab`

The repository contains a notebook `tutorial.ipynb`.  This contains detailed instructions for training a model and forecasting.

# Quick start

## The `all in one approach`

In the example below assume that `y_train` is a `pandas.Series` with a `DateTimeIndex` and time series of historical observations.

```python
from swast_forecast.utility import forecast

#return a 7-step forecast with 95% prediction interval
results = forecast(y_train, horizon=7)

```


## The three step approach

```python

from swast_forecast.utility import default_ensemble()

#create an ensemble with default parameters
model = default_ensemble()

#fit the model to the training data
model.fit(y_train)

#return a 7-step forecast with 95% prediction interval
model.predict(horizon=7)
```

**Output:**

By default three columns of data are returned in a `pandas.DataFrame`: 

* **yhat**: the mean of the forecast distribution (the point forecast)
* **yhat_lower_95**: the lower bound of the 95\% prediction interval
* **yhat_upper_95**: the upper bound of the 95\% prediction interval

The index of the dataframe is a `pandas.DataTimeIndex` 


| ds                  |    yhat | yhat_lower_95 | yhat_upper_95 |
| :------------------ | ------: | ------------: | -----------: |
| 2020-01-01 00:00:00 | 389.034 |       353.899 |      424.194 |
| 2020-01-02 00:00:00 | 328.488 |       291.634 |      365.817 |
| 2020-01-03 00:00:00 | 332.563 |       295.256 |      369.517 |
| 2020-01-04 00:00:00 | 348.734 |       311.209 |      384.396 |
| 2020-01-05 00:00:00 | 348.858 |       310.358 |      386.455 |
| 2020-01-06 00:00:00 | 335.639 |       297.341 |      372.774 |
| 2020-01-07 00:00:00 | 326.683 |       290.259 |      363.039 |


