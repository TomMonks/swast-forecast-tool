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

'| ds                  |    yhat |   yhat_lower_95 |   yhat_upper95 |\n|:--------------------|--------:|----------------:|---------------:|\n| 2020-01-01 00:00:00 | 389.034 |         352.986 |        426.056 |\n| 2020-01-02 00:00:00 | 328.488 |         291.369 |        365.122 |\n| 2020-01-03 00:00:00 | 332.563 |         296.344 |        369.358 |\n| 2020-01-04 00:00:00 | 348.734 |         312.404 |        386.402 |\n| 2020-01-05 00:00:00 | 348.858 |         312.056 |        386.331 |\n| 2020-01-06 00:00:00 | 335.639 |         298.304 |        374.322 |\n| 2020-01-07 00:00:00 | 326.683 |         288.587 |        363.517 |\n| 2020-01-08 00:00:00 | 324.272 |         286.408 |        361.524 |\n| 2020-01-09 00:00:00 | 324.575 |         286.336 |        361.742 |\n| 2020-01-10 00:00:00 | 328.924 |         290.05  |        365.805 |\n| 2020-01-11 00:00:00 | 345.399 |         308.329 |        382.77  |\n| 2020-01-12 00:00:00 | 345.872 |         306.701 |        382.754 |'

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




