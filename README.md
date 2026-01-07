# Pandas Data Analysis Learning Repository

[![Python](https://img.shields.io/badge/Python-3.14.2-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Latest-green.svg)](https://pandas.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## Overview

A comprehensive, systematic approach to mastering data analysis with Pandas. This repository documents practical implementations, methodologies, and best practices for data manipulation and analysis using real-world datasets.

**Initiated:** December 28, 2025  
**Current Phase:** Advanced Series Operations & Data Manipulation

---

## Repository Structure

```
pandas-learning-journey/
│
├── notebooks/
│   ├── 1_Series_Fundamentals.ipynb
│   ├── 2_Series_Deep_Dive.ipynb
│   ├── 3_Operators.ipynb
│   ├── 4_Aggregate_Methods.ipynb
│   ├── 5_Conversion_Methods.ipynb
│   ├── 6_Manipulation_Methods.ipynb
│   ├── 7_Indexing_Operations.ipynb
│   └── ...
│
├── datasets/
│   └── vehicles.csv
│
├── src/
│   └── utils/
│
├── requirements.txt
└── README.md
```

---

## Learning Roadmap

### Phase 1: Foundation (Completed)

-   [x] Series Fundamentals
-   [x] Index Abstraction
-   [x] Data Loading from CSV
-   [x] Series Attributes and Methods
-   [x] Operators and Dunder Methods
-   [x] Index Alignment
-   [x] Broadcasting Operations
-   [x] Aggregate Methods
-   [x] Type Conversion and Memory Optimization
-   [x] Data Manipulation Techniques
-   [x] Advanced Indexing Operations

### Phase 2: DataFrames (In Progress)

-   [ ] DataFrame Basics
-   [ ] Multi-column Operations
-   [ ] Data Selection and Filtering
-   [ ] Merging and Joining
-   [ ] GroupBy Operations

### Phase 3: Advanced Topics

-   [ ] Time Series Analysis
-   [ ] Advanced Missing Data Strategies
-   [ ] Performance Optimization
-   [ ] Custom Functions and Vectorization

### Phase 4: Applied Projects

-   [ ] Exploratory Data Analysis
-   [ ] Data Cleaning Pipelines
-   [ ] Statistical Analysis
-   [ ] Real-world Case Studies

---

## Current Work

### Module 3: Type Conversion and Memory Optimization

**Notebook:** `5_Conversion_Methods.ipynb`

**Core Concepts:**

**Automatic Type Conversion**
Pandas provides intelligent type inference and conversion capabilities.

```python
# Convert to optimal nullable integer type
city_mpg.convert_dtypes()
# Result: int64 → Int64 (supports NA values)

# Explicit type conversion
city_mpg.astype('Int16')  # Reduce memory footprint
```

**Memory Optimization Strategies**

Understanding data type limits and memory usage:

```python
# Integer type ranges
np.iinfo('int64')   # -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807
np.iinfo('uint8')   # 0 to 255

# Float type ranges
np.finfo('float16')  # ±65,504 (resolution: 0.001)
np.finfo('float64')  # ±1.798e+308 (resolution: 1e-15)
```

**Memory Usage Analysis**

```python
# Numeric data memory comparison
city_mpg.nbytes                    # 396,640 bytes (int64)
city_mpg.astype('Int16').nbytes    # 148,740 bytes (62.5% reduction)

# String/Object memory considerations
make.nbytes                        # 396,640 bytes (pointer size)
make.memory_usage(deep=True)       # 2,744,141 bytes (actual strings)
make.astype('category').memory_usage(deep=True)  # 112,242 bytes (95.9% reduction)
```

**Categorical Data Optimization**

```python
# Convert to unordered category
city_mpg.astype('category')
# Categories: 142 unique values

# Create ordered categorical type
values = pd.Series(sorted(set(city_mpg)))
city_type = pd.CategoricalDtype(categories=values, ordered=True)
city_mpg.astype(city_type)
# Categories: [6 < 7 < 8 < ... < 153]
```

**Series to DataFrame Conversion**

```python
city_mpg.to_frame()  # Convert Series to single-column DataFrame
```

**Key Findings:**

-   **Int16 conversion:** 62.5% memory reduction for numeric data
-   **Category conversion:** 95.9% memory reduction for string data (from 2.7MB to 112KB)
-   Ordered categories enable comparison operations
-   Type selection critical for large datasets

---

### Module 4: Data Manipulation Methods

**Notebook:** `6_Manipulation_Methods.ipynb`

**Performance-Critical Operations**

**Apply vs Vectorized Operations**

```python
# Custom function with .apply() - SLOW
def get20(val):
    return val > 20

city_mpg.apply(get20)       # 4.08 ms
city_mpg.gt(20)            # 22.5 μs (181x faster)
```

**Efficient Data Generalization**

```python
# Group manufacturers into categories
top5 = make.value_counts().index[:5]

# Method 1: .apply() with custom function
make.apply(generalize_top5)                    # 24.5 ms

# Method 2: .where() - PREFERRED
make.where(make.isin(top5), other='Other')     # 2.08 ms (12x faster)

# Method 3: .mask() - Inverse logic
make.mask(~make.isin(top5), other='Others')    # Same performance
```

**Multi-Condition Logic**

```python
# Approach 1: Chained .where()
(make
 .where(make.isin(top5), 'Top10')
 .where(make.isin(top10), 'Other'))

# Approach 2: NumPy select (preferred for complex conditions)
np.select([make.isin(top5), make.isin(top10)],
          [make, 'Top10'],
          'Other')
```

**Missing Data Operations**

```python
# Count missing values
cyl.isna().sum()  # 1,371 missing cylinder values

# Locate missing data
missing = cyl.isna()
make.loc[missing]  # Electric/hybrid vehicles (Tesla, Toyota, Nissan, Ford)

# Fill missing values
cyl.fillna(0)                    # Fill with constant
cyl.fillna(cyl.mean())           # Fill with mean
cyl.ffill()                      # Forward fill
cyl.interpolate()                # Linear interpolation
```

**Interpolation Example**

```python
temp = pd.Series([32, 40, None, 42, 39, 32])
temp.interpolate()
# Result: [32.0, 40.0, 41.0, 42.0, 39.0, 32.0]
```

**Outlier Management with Clipping**

```python
# Clip values to 5th and 95th percentiles
city_mpg.clip(
    lower=city_mpg.quantile(.05),  # 12 MPG
    upper=city_mpg.quantile(.95)   # 31 MPG
)
```

**Sorting Operations**

```python
# Sort by values (index follows)
city_mpg.sort_values()

# Sort by index
city_mpg.sort_index()

# Combined operations maintain alignment
(city_mpg.sort_values() + highway_mpg) / 2
```

**Deduplication and Ranking**

```python
# Remove duplicate values
city_mpg.drop_duplicates()  # 142 unique MPG values from 49,580 records

# Ranking methods
city_mpg.rank()                      # Average rank for ties
city_mpg.rank(method='min')          # Minimum rank for ties
city_mpg.rank(method='dense')        # Dense ranking (no gaps)
```

**Value Replacement**

```python
# Simple replacement
make.replace('Subaru', '昴, スバル')

# Multiple replacements
make.replace({'Subaru': '昴', 'Toyota': 'トヨタ'})
```

**Data Binning**

```python
# Equal-width bins
pd.cut(city_mpg, 10)  # 10 bins of equal width

# Custom bin edges
pd.cut(city_mpg, [0, 10, 20, 40, 70, 150])

# Equal-frequency bins (quantile-based)
pd.qcut(city_mpg, 10)  # 10 bins with equal counts
```

**Performance Summary:**

-   **Vectorized operations:** 181x faster than .apply()
-   **.where() method:** 12x faster than .apply() for conditional logic
-   **Always prefer built-in methods over custom functions**

---

### Module 5: Indexing Operations

**Notebook:** `7_Indexing_Operations.ipynb`

**Index Manipulation**

**Renaming Index**

```python
# Method 1: Using dictionary mapping
city2 = city_mpg.rename(make.to_dict())

# Method 2: Using Series directly (preferred)
city2 = city_mpg.rename(make)

# Result: Index becomes manufacturer names
# Alfa Romeo    19
# Ferrari        9
# Dodge         23
```

**Resetting Index**

```python
# Reset to DataFrame with old index as column
city2.reset_index()

# Drop old index, return Series with default integer index
city2.reset_index(drop=True)
```

**Label-Based Indexing with .loc**

```python
# Single label (may return Series if multiple matches)
city2.loc['Subaru']  # All 1,036 Subaru entries

# List of labels (always returns Series)
city2.loc[['Fisker']]  # 4 Fisker entries

# Multiple labels
city2.loc[['Ferrari', 'Lamborghini']]  # 455 combined entries

# Slicing (INCLUSIVE of both endpoints)
city2.sort_index().loc['Ferrari':'Lamborghini']  # 13,502 entries
```

**Position-Based Indexing with .iloc**

```python
# Single position
city2.iloc[0]      # First element: 19
city2.iloc[-1]     # Last element: 16

# Multiple positions
city2.iloc[[0, 1, -1]]  # First, second, and last

# Slicing (EXCLUSIVE of endpoint)
city2.iloc[-8:]    # Last 8 elements
```

**Convenience Methods**

```python
# Head and tail
city2.head(3)  # First 3 entries
city2.tail(3)  # Last 3 entries

# Random sampling
city2.sample(6, random_state=42)
# Porsche    20
# Saab       17
# Plymouth   19
```

**Index Filtering**

```python
# Substring match
city2.filter(like='rd')  # Returns all 'Ford' entries (3,904 records)

# Regular expression
city2.filter(regex='(Ford)|(Subaru)')  # 4,939 combined entries
```

**Key Indexing Concepts:**

-   **.loc:** Label-based, inclusive slicing
-   **.iloc:** Position-based, exclusive slicing
-   **Index operations preserve data alignment**
-   **Filtering enables pattern-based selection**

---

## Technical Environment

### System Requirements

```
Python 3.14.2
Pandas (latest)
NumPy
Jupyter Notebook/Lab
```

### Setup Instructions

**1. Clone Repository**

```bash
git clone https://github.com/yourusername/pandas-learning-journey.git
cd pandas-learning-journey
```

**2. Environment Configuration**

```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

**3. Install Dependencies**

```bash
pip install -r requirements.txt
```

**4. Launch Jupyter**

```bash
jupyter notebook
```

---

## Key Concepts Reference

### Type Conversion Methods

| Method              | Purpose                           | Example                 |
| ------------------- | --------------------------------- | ----------------------- |
| `.convert_dtypes()` | Automatic optimal type conversion | int64 → Int64           |
| `.astype(dtype)`    | Explicit type conversion          | `astype('Int16')`       |
| `.to_frame()`       | Convert Series to DataFrame       | Single-column DataFrame |

### Memory Optimization Guidelines

| Data Type      | Use Case             | Memory Impact         |
| -------------- | -------------------- | --------------------- |
| `int8`/`int16` | Small integer ranges | 87.5% - 75% reduction |
| `uint8`        | Non-negative 0-255   | 87.5% reduction       |
| `float16`      | Low-precision floats | 75% reduction         |
| `category`     | Repetitive strings   | 90%+ reduction        |

### Data Manipulation Methods

| Method                | Purpose                       | Performance        |
| --------------------- | ----------------------------- | ------------------ |
| `.apply(func)`        | Apply function element-wise   | Slow (Python loop) |
| `.where(cond, other)` | Replace where condition False | Fast (vectorized)  |
| `.mask(cond, other)`  | Replace where condition True  | Fast (vectorized)  |
| `.fillna(value)`      | Fill missing values           | Fast               |
| `.interpolate()`      | Interpolate missing values    | Medium             |
| `.clip(lower, upper)` | Limit value ranges            | Fast               |
| `.sort_values()`      | Sort by values                | Medium             |
| `.drop_duplicates()`  | Remove duplicates             | Medium             |
| `.rank()`             | Calculate ranks               | Medium             |
| `.replace(old, new)`  | Replace specific values       | Fast               |

### Binning Functions

| Function             | Method               | Output                   |
| -------------------- | -------------------- | ------------------------ |
| `pd.cut(data, bins)` | Equal-width bins     | Categorical intervals    |
| `pd.qcut(data, q)`   | Equal-frequency bins | Quantile-based intervals |

### Indexing Attributes

| Attribute    | Type           | Slicing Behavior    |
| ------------ | -------------- | ------------------- |
| `.loc[]`     | Label-based    | Inclusive endpoints |
| `.iloc[]`    | Position-based | Exclusive endpoint  |
| `.head(n)`   | First n rows   | N/A                 |
| `.tail(n)`   | Last n rows    | N/A                 |
| `.sample(n)` | Random n rows  | N/A                 |

---

## Dataset Information

### EPA Vehicle Dataset

**Description:** Comprehensive fuel economy data from the U.S. Environmental Protection Agency covering multiple vehicle model years.

**Statistics:**

-   **Total Records:** 49,580 vehicles
-   **Total Features:** 83 columns
-   **Missing Data:** 1,371 cylinder values (electric/hybrid vehicles)
-   **Unique Manufacturers:** 146 brands
-   **Primary Analysis Columns:**
    -   `city08`: City MPG for regular gasoline
    -   `highway08`: Highway MPG for regular gasoline
    -   `make`: Vehicle manufacturer
    -   `cylinders`: Engine cylinders (1,371 missing)

**Key Findings:**

-   **Average City MPG:** 20.59
-   **City MPG Variance:** 207.39
-   **Unique MPG Values:** 142 distinct values
-   **Vehicles with MPG > 20:** 14,686 (29.62%)
-   **City MPG Quantiles:**
    -   5th percentile: 12.0 MPG
    -   10th percentile: 13.0 MPG
    -   50th percentile: 18.0 MPG
    -   90th percentile: 26.0 MPG
    -   95th percentile: 31.0 MPG

**Top 5 Manufacturers by Volume:**

1. Chevrolet: 4,569 models
2. Ford: 3,903 models
3. GMC: 2,882 models
4. Dodge: 2,718 models
5. BMW: 2,643 models

**Memory Optimization Results:**

-   **Numeric optimization:** 62.5% reduction (int64 → Int16)
-   **Categorical optimization:** 95.9% reduction (object → category)
-   **Total dataset savings:** Potential 70%+ memory reduction

---

## Progress Metrics

| Metric                  | Count |
| ----------------------- | ----- |
| Days Active             | 5     |
| Notebooks Completed     | 7     |
| Datasets Analyzed       | 1     |
| Code Cells Executed     | 120+  |
| Methods Explored        | 500+  |
| Concepts Mastered       | 35+   |
| Performance Comparisons | 8     |

---

## Performance Insights

### Operation Speed Comparisons

| Operation               | Slow Method           | Fast Method       | Speedup           |
| ----------------------- | --------------------- | ----------------- | ----------------- |
| Boolean comparison      | `.apply(func)` 4.08ms | `.gt()` 22.5μs    | **181x**          |
| Conditional replacement | `.apply()` 24.5ms     | `.where()` 2.08ms | **12x**           |
| String memory           | `object` 2.74MB       | `category` 112KB  | **24x** reduction |

### Best Practices Learned

1. **Always prefer vectorized operations over .apply()**
2. **Use categorical dtype for repetitive string data**
3. **Choose appropriate numeric types based on value ranges**
4. **Use .where()/.mask() instead of .apply() for conditionals**
5. **Leverage np.select() for complex multi-condition logic**
6. **Consider memory_usage(deep=True) for actual memory footprint**
7. **Use .loc for label-based indexing, .iloc for position-based**
8. **Remember .loc slicing is inclusive, .iloc is exclusive**

---

## Advanced Techniques Implemented

### Memory-Efficient Data Loading

```python
# Specify dtypes at load time
df = pd.read_csv('data.csv',
                 dtype={'make': 'category',
                        'cylinders': 'Int8'},
                 low_memory=False)

# Select specific columns
df = pd.read_csv('data.csv', usecols=['city08', 'highway08'])
```

### Chained Operations Pattern

```python
# Clean, readable data transformations
result = (city_mpg
          .fillna(city_mpg.median())
          .clip(lower=10, upper=40)
          .astype('Int8')
          .sort_values()
          .head(100))
```

### Multi-Condition Categorical Mapping

```python
# NumPy select for complex logic
conditions = [
    make.isin(top5),
    make.isin(top10),
    make.isin(top20)
]
choices = [make, 'Top10', 'Top20']
result = np.select(conditions, choices, default='Other')
```

### Index-Based Filtering

```python
# Create custom index for analysis
city_by_make = city_mpg.rename(make)

# Filter using index patterns
european = city_by_make.filter(regex='(BMW)|(Mercedes)|(Audi)')
japanese = city_by_make.filter(regex='(Toyota)|(Honda)|(Nissan)')

# Statistical comparison
comparison = pd.DataFrame({
    'European': european.describe(),
    'Japanese': japanese.describe()
})
```

---

## Resources & References

### Official Documentation

-   [Pandas API Reference](https://pandas.pydata.org/docs/reference/index.html)
-   [Pandas User Guide](https://pandas.pydata.org/docs/user_guide/index.html)
-   [NumPy Documentation](https://numpy.org/doc/)

### Dataset Sources

-   [EPA Fuel Economy Data](https://www.fueleconomy.gov/feg/download.shtml)

### Key Tutorials Referenced

-   Pandas dtype optimization strategies
-   Vectorization vs iteration performance
-   Missing data handling methodologies

---

### Performance Comparison

```python
import time

# Slow method
start = time.time()
result1 = city_mpg.apply(lambda x: x > 20)
time1 = time.time() - start

# Fast method
start = time.time()
result2 = city_mpg.gt(20)
time2 = time.time() - start

print(f"Speedup: {time1/time2:.0f}x")
```

### Advanced Manipulation

```python
# Complex multi-step transformation
processed = (city_mpg
             .fillna(city_mpg.median())           # Handle missing
             .clip(lower=5, upper=50)              # Remove outliers
             .astype('Int8')                       # Optimize memory
             .where(city_mpg.gt(15), 'Low')        # Categorize
             .sort_values()                        # Order
             .drop_duplicates())                   # Deduplicate

# Multi-condition categorization
efficiency = np.select(
    [city_mpg.lt(15), city_mpg.between(15, 25), city_mpg.gt(25)],
    ['Low', 'Medium', 'High'],
    default='Unknown'
)
```

---

## Contributing

This repository follows a structured learning approach. Contributions, suggestions, and improvements are welcome through issues and pull requests.

---

## License

MIT License - This project is open source and available for educational purposes.

---

## Contact & Collaboration

For questions, discussions, or collaboration opportunities, please open an issue or reach out through GitHub.

---

**Last Updated:** January 4, 2026  
**Repository Status:** Active Development  
**Current Focus:** Advanced Series Manipulation & Memory Optimization  
**Next Milestone:** DataFrame Operations
