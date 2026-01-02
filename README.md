# Pandas Data Analysis Learning Repository

[![Python](https://img.shields.io/badge/Python-3.14.2-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Latest-green.svg)](https://pandas.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## Overview

A comprehensive, systematic approach to mastering data analysis with Pandas. This repository documents practical implementations, methodologies, and best practices for data manipulation and analysis using real-world datasets.

**Initiated:** December 28, 2025  
**Current Phase:** Series Data Structures & Operations

---

## Repository Structure

```
pandas-learning-journey/
│
├── notebooks/
│   ├── 1_Series_Fundamentals.ipynb
│   ├── 2_Series_Deep_Dive.ipynb
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
-   [ ] Series Operations
-   [ ] Boolean Indexing

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

### Series Deep Dive Analysis

**Notebook:** `2_Series_Deep_Dive.ipynb`

**Dataset:** EPA Vehicle Fuel Economy Data (`vehicles.csv`)

-   **Records:** 49,580 vehicles
-   **Features:** 83 columns including city/highway MPG ratings
-   **Source:** U.S. Environmental Protection Agency

**Key Implementations:**

```python
# Data Loading with Type Handling
df = pd.read_csv('datasets/vehicles.csv')
city_mpg = df.city08      # City fuel economy
highway_mpg = df.highway08 # Highway fuel economy

# Series Exploration
city_mpg.shape    # (49580,)
city_mpg.dtype    # int64
len(dir(city_mpg)) # 422 attributes/methods
```

**Analysis Focus:**

-   Series attribute exploration
-   Memory-efficient data handling
-   Mixed-type column management
-   Statistical operations on large datasets

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

**Essential Attributes:**

| Attribute | Description                  | Usage                  |
| --------- | ---------------------------- | ---------------------- |
| `.index`  | Returns the index object     | Access/modify labels   |
| `.values` | Returns the underlying array | Direct data access     |
| `.dtype`  | Data type of values          | Type checking          |
| `.size`   | Number of elements           | Quick count            |
| `.shape`  | Dimensionality               | Structure verification |
| `.name`   | Series identifier            | Labeling               |

**Critical Methods:**

| Method        | Purpose              | Returns |
| ------------- | -------------------- | ------- |
| `.count()`    | Non-null value count | int     |
| `.mean()`     | Arithmetic average   | float   |
| `.std()`      | Standard deviation   | float   |
| `.min()`      | Minimum value        | scalar  |
| `.max()`      | Maximum value        | scalar  |
| `.describe()` | Statistical summary  | Series  |

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

## Dataset Information

### EPA Vehicle Dataset

**Description:** Comprehensive fuel economy data from the U.S. Environmental Protection Agency covering multiple vehicle model years.

**Key Features:**

-   `city08`: City MPG for regular gasoline
-   `highway08`: Highway MPG for regular gasoline
-   Mixed-type columns requiring careful handling
-   Large-scale dataset suitable for performance testing

**Data Quality Considerations:**

-   Mixed data types in columns 69, 71-75, 77, 80
-   Requires dtype specification or low_memory=False flag
-   Suitable for demonstrating real-world data challenges

---

## Progress Metrics

| Metric              | Count        |
| ------------------- | ------------ |
| Days Active         | 1            |
| Notebooks Completed | 2            |
| Datasets Analyzed   | 1            |
| Code Cells Executed | 20+          |
| Methods Explored    | 422 (Series) |

---

## Resources & References

### Official Documentation

-   [Pandas API Reference](https://pandas.pydata.org/docs/reference/index.html)
-   [Pandas User Guide](https://pandas.pydata.org/docs/user_guide/index.html)
-   [Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/)

### Dataset Sources

-   [EPA Fuel Economy Data](https://www.fueleconomy.gov/feg/download.shtml)

---

## Development Notes

### Session Log: January 2, 2026

**Completed:**

-   Implemented comprehensive Series attribute exploration
-   Successfully loaded and processed 49,580-record dataset
-   Identified and handled mixed-type column warnings
-   Documented 422 available Series methods and attributes

**Technical Insights:**

-   Mixed-type columns require explicit dtype specification or low_memory flag
-   Series object contains extensive functionality (422 attributes/methods)
-   Efficient data loading critical for large datasets

**Next Steps:**

-   Deep dive into Series operations (arithmetic, comparison)
-   Implement boolean indexing techniques
-   Explore memory optimization strategies
-   Statistical analysis of vehicle fuel economy data

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

**Last Updated:** January 2, 2026  
**Repository Status:** Active Development
