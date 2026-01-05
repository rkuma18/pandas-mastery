# Pandas Data Analysis Learning Repository

[![Python](https://img.shields.io/badge/Python-3.14.2-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Latest-green.svg)](https://pandas.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## Overview

A comprehensive, systematic approach to mastering data analysis with Pandas. This repository documents practical implementations, methodologies, and best practices for data manipulation and analysis using real-world datasets.

**Initiated:** December 28, 2025
**Current Phase:** Series Operations & Aggregation Methods

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

### Phase 1: Foundation

-   [x] Series Fundamentals
-   [x] Index Abstraction
-   [x] Data Loading from CSV
-   [x] Series Attributes and Methods
-   [x] Operators and Dunder Methods
-   [x] Index Alignment
-   [x] Broadcasting Operations
-   [x] Aggregate Methods
-   [ ] Boolean Indexing
-   [ ] Method Chaining Patterns

### Phase 2: DataFrames

-   [ ] DataFrame Basics
-   [ ] Data Selection and Filtering
-   [ ] Merging and Joining
-   [ ] GroupBy Operations

### Phase 3: Advanced Topics

-   [ ] Time Series Analysis
-   [ ] Missing Data Handling
-   [ ] Performance Optimization
-   [ ] Custom Functions

### Phase 4: Applied Projects

-   [ ] Exploratory Data Analysis
-   [ ] Data Cleaning Pipelines
-   [ ] Statistical Analysis
-   [ ] Real-world Case Studies

---

## Current Work

### Module 1: Series Operations

**Notebook:** `3_Operators.ipynb`

**Core Concepts:**

**Dunder Methods (Magic Methods)**
Understanding the underlying mechanics of Python operators through double underscore methods.

```python
# Operator translation
(2).__add__(4)  # Equivalent to: 2 + 4
# Result: 6
```

**Index Alignment**
Pandas automatically aligns Series by index during operations, creating Cartesian products for duplicate indices.

```python
s1 = pd.Series([10, 20, 30], index=[1, 2, 2])
s2 = pd.Series([35, 44, 53], index=[2, 2, 4])

s1 + s2
# Result:
# 1     NaN    # No match in s2
# 2    55.0    # 20 + 35
# 2    64.0    # 20 + 44
# 2    65.0    # 30 + 35
# 2    74.0    # 30 + 44
# 4     NaN    # No match in s1
```

**Broadcasting**
Scalar operations are automatically broadcast across all Series values.

```python
# Calculate average MPG
(city_mpg + highway_mpg) / 2
```

**Operator Methods with Fill Values**
Handle missing indices gracefully using the `fill_value` parameter.

```python
# Use 0 for missing indices instead of NaN
s1.add(s2, fill_value=0)
# Result:
# 1    10.0    # Only in s1, uses 0 for s2
# 2    55.0    # 20 + 35
# 2    64.0    # 20 + 44
# 2    65.0    # 30 + 35
# 2    74.0    # 30 + 44
# 4    53.0    # Only in s2, uses 0 for s1
```

**Method Chaining**
Compose complex operations through sequential method calls for improved readability.

```python
(city_mpg
 .add(highway_mpg)
 .div(2))
```

---

### Module 2: Aggregate Methods

**Notebook:** `4_Aggregate_Methods.ipynb`

**Statistical Aggregations**

Core statistical methods for data summarization:

```python
city_mpg.mean()          # 20.59 MPG average
city_mpg.is_unique       # False (duplicate values exist)
city_mpg.is_monotonic_increasing  # False
```

**Quantile Analysis**

```python
# Default: 50th percentile (median)
city_mpg.quantile()      # 18.0

# Multiple quantiles
city_mpg.quantile([.1, .5, .9])
# 0.1    13.0
# 0.5    18.0
# 0.9    26.0
```

**Boolean Aggregations**

Combining boolean masks with aggregation methods for analytical insights.

```python
# Count of vehicles with MPG > 20
city_mpg.gt(20).sum()    # 14,686 vehicles

# Percentage of vehicles with MPG > 20
city_mpg.gt(20).mul(100).mean()  # 29.62%
```

**Custom Aggregation with `.agg()`**

Apply multiple aggregation functions simultaneously, including custom functions.

```python
# Custom aggregation function
def second_to_last(s):
    return s.iloc[-2]

# Multiple aggregations
city_mpg.agg(['mean', 'var', 'max', second_to_last])
# mean               20.59
# var               207.39
# max               153.00
# second_to_last     18.00
```

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

## Key Concepts Covered

### Series Data Structure

**Definition:** One-dimensional labeled array capable of holding any data type.

**Core Components:**

-   **Index:** Axis labels for data access
-   **Values:** The actual data array
-   **Name:** Optional identifier
-   **dtype:** Data type of elements

### Operators and Operations

**Arithmetic Operators:**

| Operator | Method   | Description    |
| -------- | -------- | -------------- |
| `+`      | `.add()` | Addition       |
| `-`      | `.sub()` | Subtraction    |
| `*`      | `.mul()` | Multiplication |
| `/`      | `.div()` | Division       |
| `**`     | `.pow()` | Exponentiation |
| `%`      | `.mod()` | Modulo         |

**Comparison Operators:**

| Operator | Method  | Description           |
| -------- | ------- | --------------------- |
| `==`     | `.eq()` | Equal to              |
| `!=`     | `.ne()` | Not equal to          |
| `>`      | `.gt()` | Greater than          |
| `>=`     | `.ge()` | Greater than or equal |
| `<`      | `.lt()` | Less than             |
| `<=`     | `.le()` | Less than or equal    |

### Aggregation Methods

**Statistical Methods:**

| Method        | Purpose             | Returns |
| ------------- | ------------------- | ------- |
| `.mean()`     | Arithmetic average  | float   |
| `.median()`   | Middle value        | float   |
| `.std()`      | Standard deviation  | float   |
| `.var()`      | Variance            | float   |
| `.min()`      | Minimum value       | scalar  |
| `.max()`      | Maximum value       | scalar  |
| `.sum()`      | Sum of values       | scalar  |
| `.count()`    | Non-null count      | int     |
| `.describe()` | Statistical summary | Series  |

**Quantile Methods:**

| Method                     | Purpose             | Returns         |
| -------------------------- | ------------------- | --------------- |
| `.quantile(q)`             | Value at quantile q | float or Series |
| `.quantile([q1, q2, ...])` | Multiple quantiles  | Series          |

**Boolean Properties:**

| Property                   | Description                | Returns |
| -------------------------- | -------------------------- | ------- |
| `.is_unique`               | All values unique          | bool    |
| `.is_monotonic_increasing` | Values strictly increasing | bool    |
| `.is_monotonic_decreasing` | Values strictly decreasing | bool    |

### Data Loading Best Practices

```python
# Handling Mixed-Type Columns
df = pd.read_csv('data.csv', low_memory=False)

# Or specify dtypes explicitly
df = pd.read_csv('data.csv', dtype={'column': 'str'})

# Selective column loading
df = pd.read_csv('data.csv', usecols=['col1', 'col2'])
```

---

## Progress Metrics

| Metric              | Count         |
| ------------------- | ------------- |
| Days Active         | 3             |
| Notebooks Completed | 4             |
| Datasets Analyzed   | 1             |
| Code Cells Executed | 50+           |
| Methods Explored    | 422+ (Series) |
| Concepts Mastered   | 12            |

---

## Advanced Techniques Implemented

### Method Chaining Pattern

Improves code readability and maintains functional programming paradigms:

```python
# Traditional approach
temp1 = city_mpg.add(highway_mpg)
result = temp1.div(2)

# Chained approach (preferred)
result = (city_mpg
          .add(highway_mpg)
          .div(2))
```

### Index Alignment Behavior

Understanding Pandas' automatic index matching prevents unexpected results:

```python
# Cartesian product for duplicate indices
# Index 2 appears twice in both Series
# Results in 2 × 2 = 4 combinations for index 2
s1[2] = [20, 30]
s2[2] = [35, 44]
# Produces: 20+35, 20+44, 30+35, 30+44
```

### Custom Aggregation Functions

Extend built-in functionality with domain-specific logic:

```python
def second_to_last(series):
    """Extract penultimate value from Series"""
    return series.iloc[-2]

# Use with .agg() for flexible aggregation
city_mpg.agg([np.mean, np.std, second_to_last])
```

---

## Resources & References

### Official Documentation

-   [Pandas API Reference](https://pandas.pydata.org/docs/reference/index.html)
-   [Pandas User Guide](https://pandas.pydata.org/docs/user_guide/index.html)
-   [NumPy Documentation](https://numpy.org/doc/)

### Dataset Sources

-   [EPA Fuel Economy Data](https://www.fueleconomy.gov/feg/download.shtml)

---

## Development Notes

### Session Log: January 2, 2026

**Module: Series Deep Dive**

-   Implemented comprehensive Series attribute exploration
-   Successfully loaded and processed 49,580-record dataset
-   Identified and handled mixed-type column warnings
-   Documented 422 available Series methods and attributes

### Session Log: January 3, 2026

**Module: Operators & Dunder Methods**

-   Explored Python operator implementation through dunder methods
-   Mastered index alignment behavior and Cartesian product generation
-   Implemented broadcasting for scalar operations
-   Applied fill_value parameter for handling misaligned indices
-   Practiced method chaining for cleaner, more readable code

**Module: Aggregate Methods**

-   Implemented statistical aggregation methods (mean, var, max)
-   Performed quantile analysis across multiple percentiles
-   Combined boolean operations with aggregations for analytical queries
-   Created custom aggregation functions for domain-specific analysis
-   Analyzed 29.62% of vehicles exceed 20 MPG city fuel economy

**Technical Insights:**

-   Index alignment creates NaN for non-matching indices
-   Duplicate indices generate Cartesian products in operations
-   `.agg()` accepts both built-in and custom functions
-   Boolean masks combined with `.sum()` and `.mean()` enable percentage calculations

**Next Steps:**

-   Explore boolean indexing and filtering techniques
-   Implement advanced method chaining patterns
-   Study time-based aggregations
-   Analyze correlations between city and highway MPG

---

## Code Examples Repository

### Operator Examples

```python
# Dunder method demonstration
(2).__add__(4)  # 6

# Average MPG calculation
avg_mpg = (city_mpg + highway_mpg) / 2

# Handling missing indices
s1.add(s2, fill_value=0)

# Method chaining
(city_mpg
 .add(highway_mpg)
 .div(2)
 .round(2))
```

### Aggregation Examples

```python
# Basic statistics
city_mpg.mean()    # Average
city_mpg.std()     # Standard deviation
city_mpg.quantile(.75)  # 75th percentile

# Boolean aggregations
efficient_cars = city_mpg.gt(25).sum()
efficiency_rate = city_mpg.gt(25).mul(100).mean()

# Multiple aggregations
city_mpg.agg(['mean', 'median', 'std', 'min', 'max'])

# Custom aggregation
def range_calc(s):
    return s.max() - s.min()

city_mpg.agg(['mean', range_calc])
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

**Last Updated:** January 3, 2026  
**Repository Status:** Active Development  
**Current Focus:** Series Operations & Statistical Analysis
