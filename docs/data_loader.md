# DataLoader

> **Note:** We are using `complaints.csv` as an example here, with the following columns: `date`, `complaints`. The `date` column is used as the time index and `complaints` as the target variable.

The `DataLoader` class provides a unified interface for loading and managing time series data from CSV files in your Python projects. It is designed as the first step in your time series analysis workflow, ensuring your time series data is loaded, validated, and ready for further analysis.

## Features

- Loads time series data from CSV files into pandas DataFrames.
- Standardizes column names to lowercase.
- Checks if the time series index is regular (uniform intervals).
- Saves metadata (columns, dtypes, shape, index name) to a JSON file.

## Class: `DataLoader`

### Initialization

```python
DataLoader(filepath: str, index_col: Optional[Union[str, int]] = None, parse_dates: Union[bool, list] = True)
```

- **filepath**: Path to the CSV file containing your time series data.
- **index_col**: Name or position of the column to use as the time index (e.g., a timestamp or date column).
- **parse_dates**: Whether to parse dates in the index column.

> **Note:** Your CSV must contain a column representing the time axis (e.g., "date"). Set `index_col` to this column's name.

### Methods

#### `load() -> pd.DataFrame`

Loads the time series data from the specified CSV file, standardizes column names, and sets the index name to lowercase.

**Standalone Example:**
```python
from dynamicts.data_loader import DataLoader

loader = DataLoader(filepath="data/complaints.csv", index_col="date")
df = loader.load()
print(df.head())
```

#### `is_regular() -> bool`

Checks if the time series index is regular (i.e., intervals between timestamps are uniform). Returns `True` if regular, `False` otherwise.

**Standalone Example:**
```python
from dynamicts.data_loader import DataLoader

loader = DataLoader(filepath="data/complaints.csv", index_col="date")
loader.load()  # Must load data first
is_reg = loader.is_regular()
print("Is regular:", is_reg)
```

#### `save_metadata() -> None`

Saves metadata (columns, dtypes, shape, index name) of the loaded DataFrame to a JSON file in the `metadata/` directory.

**Standalone Example:**
```python
from dynamicts.data_loader import DataLoader

loader = DataLoader(filepath="data/complaints.csv", index_col="date")
loader.load()  # Must load data first
loader.save_metadata()
print("Metadata saved.")
```

#### `run_pipeline() -> Optional[pd.DataFrame]`

Runs the time series data loading pipeline:
- Loads the data.
- Checks for regularity.
- Saves metadata if data is regular.
- Returns the loaded DataFrame.

**Standalone Example:**
```python
from dynamicts.data_loader import DataLoader

loader = DataLoader(filepath="data/complaints.csv", index_col="date")
data = loader.run_pipeline()
if data is not None:
    print("Time series data loaded successfully!")
```

### Notes

- The loader logs all actions and errors to a log file in the `logs/` directory.
- If the time index is not regular, a warning is logged and the data is still returned for inspection.
- Metadata is saved only if the time series data is regular.

---
