[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/TomMonks/swast-forecast-tool/master)

# SWAST Ensemble Forecast Tool

A forecasting tool for SWAST. Implemented in Python.

## Aims: 

The tool predicts the number of calls that result in one or more dispatches of ambulances. 

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

#return a 12-step forecast with 95% prediction interval
results = forecast(y_train, 
                   horizon=12)
```

## The three step approach

```python

from swast_forecast.utility import default_ensemble()

#create an ensemble with default parameters
model = default_ensemble()

#fit the model to the training data
model.fit(y_train)

#return a 12-step forecast with 95% prediction interval
model.predict(horizon=12)
```




