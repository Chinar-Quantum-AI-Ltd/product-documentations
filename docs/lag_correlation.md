# Correlation

> **Note:** We are using `complaints.csv` as an example here, with the following columns: `date`, `complaints`. The `date` column is used as the time index and `complaints` as the target variable.

The `Correlation` class provides methods for analyzing and visualizing autocorrelation (ACF) and partial autocorrelation (PACF) in univariate time series data. These tools are essential for understanding lag relationships and dependencies in time series analysis.
 
## Features

- Plots autocorrelation (ACF) for a given time series and number of lags.
- Plots partial autocorrelation (PACF) for a given time series and number of lags.
- Supports both instance-based and standalone usage.
- Optionally logs plots to HTML reports.

## Class: `Correlation`

### Initialization

```python
Correlation(df: pd.DataFrame = None, target_col: str = None, lags: int = 20, output_filepath: str = None)
```

- **df**: The time series DataFrame (indexed by the time column).
- **target_col**: The column name of the univariate time series to analyze.
- **lags**: Number of lags to use for correlation plots (default: 20).
- **output_filepath**: Path prefix for saving HTML reports and plots.

> **Note:** Your DataFrame should have a time-based index (e.g., "date", "timestamp").

### Methods

#### `acf_plot(data: pd.Series = None, lags: int = None, save: bool = True, output_filepath: str = None)`

Plots the autocorrelation function (ACF) for the specified time series and number of lags.

- **data**: Optional. A pandas Series to plot. If not provided, uses the instance's DataFrame and target column.
- **lags**: Optional. Number of lags to plot. Defaults to the instance's `lags`.
- **save**: Optional. Whether to save the plot to an HTML report.
- **output_filepath**: Optional. Path for saving the report.

**Standalone Example:**
```python
from dynamicts.lag_correlation import Correlation

# Instance-based usage
corr = Correlation(df, target_col="complaints", lags=30, output_filepath="report")
fig = corr.acf_plot()
fig.show()

# Standalone usage
corr = Correlation()
fig = corr.acf_plot(data=df["complaints"], lags=30, output_filepath="report")
fig.show()
```

#### `pacf_plot(data: pd.Series = None, lags: int = None, save: bool = True, output_filepath: str = None)`

Plots the partial autocorrelation function (PACF) for the specified time series and number of lags.

- **data**: Optional. A pandas Series to plot. If not provided, uses the instance's DataFrame and target column.
- **lags**: Optional. Number of lags to plot. Defaults to the instance's `lags`.
- **save**: Optional. Whether to save the plot to an HTML report.
- **output_filepath**: Optional. Path for saving the report.

**Standalone Example:**
```python
from dynamicts.lag_correlation import Correlation

# Instance-based usage
corr = Correlation(df, target_col="complaints", lags=30, output_filepath="report")
fig = corr.pacf_plot()
fig.show()

# Standalone usage
corr = Correlation()
fig = corr.pacf_plot(data=df["complaints"], lags=30, output_filepath="report")
fig.show()
```

### Notes

- The DataFrame should be indexed by the time column for proper time series analysis.
- Plots can be logged to HTML reports if `save=True` and `output_filepath` is provided.

---
