# UnivariateAnalysis

> **Note:** The following examples assume a time series DataFrame similar to `complaints.csv`, with columns: `date`and `complaints`.

The `UnivariateAnalysis` class provides a suite of methods for exploratory and statistical analysis of univariate time series data. It helps you understand the distribution, missing values, and outliers in your time series before further modeling or forecasting.

## Features

- Visualizes the distribution and boxplot of the target time series.
- Computes skewness and kurtosis with interpretation.
- Checks for missing values and provides recommendations.
- Detects outliers using IQR and Z-score methods.
- Logs plots and messages to HTML reports.

## Class: `UnivariateAnalysis`

### Initialization

```python
UnivariateAnalysis(df: pd.DataFrame, target_col: str, index_col: str = "date", output_filepath: str = "output_filepath")
```

- **df**: The time series DataFrame (indexed by the time column).
- **target_col**: The column name of the univariate time series to analyze.
- **index_col**: The name of the time index column (default: "date").
- **output_filepath**: Path prefix for saving HTML reports and plots.

> **Note:** Your DataFrame should have a time-based index (e.g., "date", "timestamp").

### Methods

#### `plot_distribution()`

Plots the histogram and boxplot of the target time series column and logs the plot to the HTML report.

**Standalone Example:**
```python
from dynamicts.analysis import UnivariateAnalysis

analysis = UnivariateAnalysis(df, target_col="complaints", index_col="date", output_filepath="report")
fig = analysis.plot_distribution()
fig.show()
```

#### `check_distribution_stats()`

Computes skewness and kurtosis for the target column, interprets the results, and logs the summary to the HTML report.

**Standalone Example:**
```python
from dynamicts.analysis import UnivariateAnalysis

analysis = UnivariateAnalysis(df, target_col="complaints", index_col="date", output_filepath="report")
stats = analysis.check_distribution_stats()
print(stats["full_message"])
```

#### `check_missing_values()`

Checks for missing values in the target column, reports the count and percentage, and logs recommendations to the HTML report.

**Standalone Example:**
```python
from dynamicts.analysis import UnivariateAnalysis

analysis = UnivariateAnalysis(df, target_col="complaints", index_col="date", output_filepath="report")
missing = analysis.check_missing_values()
print(missing["message"])
```

#### `detect_outliers(method="both", plot=True)`

Detects outliers in the target column using IQR, Z-score, or both. Optionally plots and logs the results.

- **method**: "iqr", "zscore", or "both" (default: "both").
- **plot**: Whether to plot the outliers (default: True).

**Standalone Example:**
```python
from dynamicts.analysis import UnivariateAnalysis

analysis = UnivariateAnalysis(df, target_col="complaints", index_col="date", output_filepath="report")
outliers = analysis.detect_outliers(method="both", plot=True)
print(f"Outliers detected: {outliers['outliers_detected']}")
```

#### `run_univariate_analysis(df, output_filepath, target_col, index_col="date")` (static method)

Runs the full univariate analysis pipeline: distribution plot, stats, missing values, and outlier detection. Displays results in a notebook environment.

**Standalone Example:**
```python
from dynamicts.analysis import UnivariateAnalysis

results = UnivariateAnalysis.run_univariate_analysis(
    df=df,
    output_filepath="report",
    target_col="complaints",
    index_col="date"
)
```

### Notes

- All plots and messages are logged to HTML reports using the provided `output_filepath`.
- The DataFrame should be indexed by the time column for proper time series analysis.

---
