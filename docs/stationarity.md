# Stationarity

> **Note:** We are using `complaints.csv` as an example here, with the following columns: `date`, `complaints`. The `date` column is used as the time index and `complaints` as the target variable.

The `Stationarity` class provides methods to test and visualize the stationarity of **univariate time series data**. Stationarity is a key assumption in many time series models, and these tools help you assess and transform your data accordingly.

## Features

- Performs the Augmented Dickey-Fuller (ADF) test for stationarity.
- Plots rolling mean and standard deviation for visual inspection.
- Supports both instance-based and standalone usage.
- Optionally logs results and plots to HTML reports.

## Class: `Stationarity`

### Initialization

```python
Stationarity(df: pd.DataFrame = None, target_col: str = None, window: int = 12, output_filepath: str = None)
```

- **df**: The time series DataFrame (indexed by the time column).
- **target_col**: The column name of the univariate time series to analyze.
- **window**: Window size for rolling statistics (default: 12).
- **output_filepath**: Path prefix for saving HTML reports and plots.

> **Note:** Your DataFrame should have a time-based index (e.g., "date", "timestamp").

### Methods

#### `adf_test(data: pd.Series = None, verbose: bool = True, save: bool = True, output_filepath: str = None)`

Performs the Augmented Dickey-Fuller test for stationarity on the specified time series.

- **data**: Optional. A pandas Series to test. If not provided, uses the instance's DataFrame and target column.
- **verbose**: Whether to print and log the test summary (default: True).
- **save**: Whether to save the results to an HTML report (default: True).
- **output_filepath**: Optional. Path for saving the report.

**Standalone Example:**
```python
from dynamicts.stationarity import Stationarity

# Instance-based usage
stat = Stationarity(df, target_col="complaints", window=12, output_filepath="report")
adf_result = stat.adf_test()

# Standalone usage
stat = Stationarity()
adf_result = stat.adf_test(data=df["complaints"], verbose=True, output_filepath="report")
```

#### `plot_rolling_stats(data: pd.Series = None, window: int = None, save: bool = True, output_filepath: str = None)`

Plots the rolling mean and standard deviation for the specified time series and window size.

- **data**: Optional. A pandas Series to plot. If not provided, uses the instance's DataFrame and target column.
- **window**: Optional. Window size for rolling statistics. Defaults to the instance's `window`.
- **save**: Whether to save the plot to an HTML report (default: True).
- **output_filepath**: Optional. Path for saving the report.

**Standalone Example:**
```python
from dynamicts.stationarity import Stationarity

# Instance-based usage
stat = Stationarity(df, target_col="complaints", window=12, output_filepath="report")
fig = stat.plot_rolling_stats()
fig.show()

# Standalone usage
stat = Stationarity()
fig = stat.plot_rolling_stats(data=df["complaints"], window=12, output_filepath="report")
fig.show()
```

### Notes

- The DataFrame should be indexed by the time column for proper time series analysis.
- Results and plots can be logged to HTML reports if `save=True` and `output_filepath` is provided.

---
