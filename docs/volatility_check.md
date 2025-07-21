# VolatilityChecker

> **Note:** We are using `complaints.csv` as an example here, with the following columns: `date`, `complaints`. The `date` column is used as the time index and `complaints` as the target variable.

The `VolatilityChecker` class provides methods for analyzing and visualizing volatility in univariate time series data using ARCH and GARCH models. These tools help you assess the presence and dynamics of volatility clustering in your time series.

## Features

- Computes and plots volatility using ARCH(1) and GARCH(1,1) models.
- Supports both instance-based and standalone usage.
- Optionally logs plots and summary statistics to HTML reports.

## Class: `VolatilityChecker`

### Initialization

```python
VolatilityChecker(df: pd.DataFrame = None, target_col: str = None, output_filepath: str = "Output")
```

- **df**: The time series DataFrame (indexed by the time column).
- **target_col**: The column name of the univariate time series to analyze.
- **output_filepath**: Path prefix for saving HTML reports and plots.

> **Note:** Your DataFrame should have a time-based index (e.g., "date", "timestamp").

### Methods

#### `arch_volatility(data: pd.Series = None, save: bool = True, output_filepath: str = None)`

Computes and plots volatility using an ARCH(1) model.

- **data**: Optional. A pandas Series to analyze. If not provided, uses the instance's DataFrame and target column.
- **save**: Whether to save the plot and summary to an HTML report (default: True).
- **output_filepath**: Optional. Path for saving the report.

**Standalone Example:**
```python
from dynamicts.data_loader import DataLoader
from dynamicts.volatility_check import VolatilityChecker

loader = DataLoader(filepath="data/complaints.csv", index_col="date")
df = loader.run_pipeline()

# Instance-based usage
vc = VolatilityChecker(df, target_col="complaints", output_filepath="report")
fig = vc.arch_volatility()
fig.show()

# Standalone usage
vc2 = VolatilityChecker()
fig2 = vc2.arch_volatility(data=df["complaints"], output_filepath="report")
fig2.show()
```

#### `garch_volatility(data: pd.Series = None, save: bool = True, output_filepath: str = None)`

Computes and plots volatility using a GARCH(1,1) model.

- **data**: Optional. A pandas Series to analyze. If not provided, uses the instance's DataFrame and target column.
- **save**: Whether to save the plot and summary to an HTML report (default: True).
- **output_filepath**: Optional. Path for saving the report.

**Standalone Example:**
```python
from dynamicts.data_loader import DataLoader
from dynamicts.volatility_check import VolatilityChecker

loader = DataLoader(filepath="data/complaints.csv", index_col="date")
df = loader.run_pipeline()

# Instance-based usage
vc = VolatilityChecker(df, target_col="complaints", output_filepath="report")
fig = vc.garch_volatility()
fig.show()

# Standalone usage
vc2 = VolatilityChecker()
fig2 = vc2.garch_volatility(data=df["complaints"], output_filepath="report")
fig2.show()
```

### Notes

- The DataFrame should be indexed by the time column for proper time series analysis.
- Plots and summary statistics can be logged to HTML reports if `save=True` and `output_filepath` is provided.

---
