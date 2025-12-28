<div align="center">

# 🐼 My Pandas Learning Journey

[![Python](https://img.shields.io/badge/Python-3.14.2-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Latest-green.svg)](https://pandas.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

_A comprehensive documentation of my daily journey learning data analysis with Pandas_

[Getting Started](#-getting-started) • [Progress](#-learning-progress) • [Resources](#-resources)

</div>

---

## About This Repository

This repository tracks my daily progress as I learn Pandas, the powerful Python library for data manipulation and analysis. Each day, I explore new concepts, write code, and document my understanding.

> **Started:** December 28, 2024  
> **Current Focus:** Series Fundamentals

---

## Learning Objectives

-   [ ] Master Pandas Series and DataFrames
-   [ ] Understand data manipulation techniques
-   [ ] Learn data cleaning and preprocessing
-   [ ] Explore data visualization with Pandas
-   [ ] Work with real-world datasets
-   [ ] Build practical data analysis projects

---

## Learning Progress

### Current Status

| Metric              | Count               |
| ------------------- | ------------------- |
| Days Studied        | 1                   |
| Notebooks Completed | 1                   |
| Topics Mastered     | Series Fundamentals |
| Current Focus       | Series Operations   |

### Completed Topics

-   **Series Fundamentals** - Understanding one-dimensional data structures
-   **Index Abstraction** - Custom indices and axis labels
-   **Missing Data** - NaN handling and nullable integers
-   **Categorical Data** - Ordered and unordered categories

### Up Next

-   🔜 Series Operations and Methods
-   🔜 Boolean Indexing and Filtering
-   🔜 DataFrame Basics
-   🔜 Data Loading and Saving

---

## Tools & Setup

### Prerequisites

```bash
Python 3.14.2
pandas
numpy
jupyter notebook
```

### Installation

```bash
# Clone this repository
git clone https://github.com/yourusername/pandas-learning-journey.git

# Navigate to directory
cd pandas-learning-journey

# Create virtual environment
python -m venv venv

# Activate virtual environment
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install pandas numpy jupyter
```

### Running Notebooks

```bash
jupyter notebook
```

---

## Key Learnings Summary

<details>
<summary><b>Series Fundamentals</b></summary>

-   **Definition:** One-dimensional labeled array
-   **Components:** Index + Data + Name
-   **Data Types:** Can hold integers, floats, strings, objects
-   **Missing Data:** Represented as `NaN` or `<NA>`
-   **Categorical Data:** Memory-efficient representation with optional ordering

</details>

<details>
<summary><b>Important Methods</b></summary>

| Method     | Description              |
| ---------- | ------------------------ |
| `.count()` | Count non-NaN values     |
| `.size`    | Total number of elements |
| `.mean()`  | Calculate average        |
| `.index`   | Access the index         |
| `.values`  | Access the values        |

</details>

---

## Resources

### Official Documentation

-   [Pandas Documentation](https://pandas.pydata.org/docs/)
-   [Pandas User Guide](https://pandas.pydata.org/docs/user_guide/index.html)
-   [NumPy Documentation](https://numpy.org/doc/)

---

## Code Snippets Collection

### Creating Different Types of Series

```python
# From list
s = pd.Series([1, 2, 3, 4])

# From dictionary
s = pd.Series({'a': 1, 'b': 2, 'c': 3})

# With custom index
s = pd.Series([1, 2, 3], index=['x', 'y', 'z'])

# Categorical data
s = pd.Series(['S', 'M', 'L'], dtype='category')
```

---

## Statistics

```
Total Days Studied: 1
Notebooks Completed: 1
Concepts Learned: 6
Code Examples: 15+
```

---

## Next Steps

-   [ ] Learn Series operations and methods
-   [ ] Explore DataFrame basics
-   [ ] Practice with real datasets
-   [ ] Work on data cleaning techniques

---

## Notes & Reflections

### Day 1 Reflection

> Today I learned the fundamentals of Pandas Series. The concept of index abstraction is powerful - it's like having a labeled array that can be accessed by position or by label. The handling of NaN values is elegant, and I'm excited to explore more complex operations.

---

## Contributing

This is a personal learning repository, but suggestions and resources are always welcome!

---

## License

This project is licensed under the MIT License - feel free to use this template for your own learning journey!

---

<div align="center">

### Keep Learning, Keep Growing!

_"Data is the new oil, and Pandas is the refinery."_

**[⬆ Back to Top](#-my-pandas-learning-journey)**

</div>
