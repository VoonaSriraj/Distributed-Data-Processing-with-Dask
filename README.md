# Distributed Data Processing with Dask
[![Python](https://img.shields.io/badge/python-3.7%20%7C%203.8%20%7C%203.9%20%7C%203.10-blue)](https://www.python.org/)
[![Dask](https://img.shields.io/badge/Dask-FF6B6B?style=flat&logo=dask&logoColor=white)](https://dask.org/)

This repository provides a practical demonstration and performance comparison of a scalable ETL (Extract, Transform, Load) pipeline using Dask versus Pandas. The core of this project is a Jupyter notebook that processes a large dataset, showcasing Dask's ability to handle data that may not fit into memory and to parallelize computations for significant speed improvements.

## 📋 Table of Contents
- [Overview](#-overview)
- [Key Concepts](#-key-concepts)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Usage](#-usage)
- [Pipeline Details](#-pipeline-details)
- [Performance Results](#-performance-results)
- [Conclusion](#-conclusion)

## 🌟 Overview

The primary goal of this project is to illustrate the advantages of using Dask for processing large datasets. By running the same ETL task with both Dask and Pandas, the notebook provides a clear, quantitative comparison of their performance.

The ETL task consists of:
1.  **Extract**: Loading a large CSV file.
2.  **Transform**: Filtering rows based on a value threshold.
3.  **Load**: Grouping the data by category and aggregating to calculate count, mean, and sum.

## ⚙️ Key Concepts

*   **Lazy Evaluation (Dask)**: Dask builds a task graph of all operations without executing them immediately. Computation is only triggered when a result is explicitly requested (e.g., via the `.compute()` method). This allows for complex query optimization.
*   **Parallel Processing (Dask)**: Dask breaks the DataFrame into multiple partitions (smaller Pandas DataFrames) and operates on them in parallel across multiple CPU cores, drastically reducing wall-clock time.
*   **In-Memory Processing (Pandas)**: Pandas loads the entire dataset into memory before performing operations. This is fast for datasets that fit in RAM but fails or becomes extremely slow for larger-than-memory datasets.

## 📋 Prerequisites

*   Python (>=3.12 recommended)
*   A large CSV dataset to test the pipelines. The notebook assumes a file named `large_dataset.csv` with `category` and `value` columns. You will need to provide your own and update the file path in the notebook.

## 🛠️ Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/VoonaSriraj/Distributed-Data-Processing-with-Dask.git
    cd Distributed-Data-Processing-with-Dask
    ```

2.  **Create and activate a virtual environment (recommended):**
    ```bash
    # For Windows
    python -m venv .venv
    .\.venv\Scripts\activate

    # For macOS/Linux
    python3 -m venv .venv
    source .venv/bin/activate
    ```

3.  **Install the required dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

## 🚀 Usage

1.  Place your large CSV dataset (e.g., `large_dataset.csv`) in the project directory.

2.  Open the Jupyter notebook and update the `csv_path` variable to point to your dataset:
    ```python
    # In Distributed_Data_Processing_with_Dask.ipynb
    csv_path = Path("path/to/your/large_dataset.csv")
    ```

3.  Start Jupyter and run the notebook:
    ```bash
    jupyter notebook Distributed_Data_Processing_with_Dask.ipynb
    ```
    or
    ```bash
    jupyter lab
    ```

4.  Execute the cells in the notebook to run both pipelines and see the performance comparison.

## ⚙️ Pipeline Details

The notebook defines two functions, `dask_etl_pipeline` and `pandas_etl_pipeline`, which perform the same set of operations.

### Dask ETL Pipeline
```python
def dask_etl_pipeline(csv_path, value_threshold):
    # Data loading is lazy and creates a Dask DataFrame
    df = dd.read_csv(
        csv_path,
        blocksize="128MB",
        assume_missing=True,
        dtype_backend="pyarrow"
    )

    # Transformations build a task graph
    df = df[df["value"] > value_threshold]
    result = (
        df.groupby("category")
        .agg(
            count=("value", "count"),
            mean_value=("value", "mean"),
            sum_value=("value", "sum"),
        )
    )
    
    # Computation is triggered here
    output = result.compute()
    return output
```

### Pandas ETL Pipeline
```python
def pandas_etl_pipeline(csv_path, value_threshold):
    # Data is loaded entirely into memory
    df = pd.read_csv(csv_path)

    # Transformations are executed immediately
    df = df[df["value"] > value_threshold]
    output = (
        df.groupby("category")
        .agg(
            count=("value", "count"),
            mean_value=("value", "mean"),
            sum_value=("value", "sum"),
        )
    )
    return output
```

## 📊 Performance Results

The notebook automatically times each stage of the pipelines and generates a comparison table. The results clearly show Dask's superiority for this task, primarily due to its lazy and parallel nature. Dask's data loading time is near-zero, as it only scans the file metadata initially. The heavy lifting is done during the transformation phase, which runs in parallel.

An example output from the notebook:

| Framework | Total Time (seconds) | Data Loading Time (seconds) | Transformation Time (seconds) | Speedup (Pandas / Dask) | Time Reduction (%) |
| :-------- | :------------------- | :-------------------------- | :---------------------------- | :---------------------- | :----------------- |
| **Dask**  | 166.97               | 0.06                        | 166.91                        | -                       | -                  |
| **Pandas**| 517.65               | 299.96                      | 217.69                        | 3.10x                   | 67.74%             |

As shown, Dask completed the task more than **3 times faster** than Pandas, with a total time reduction of nearly 68%. This performance gap widens significantly as dataset sizes increase beyond the available system RAM.

## ✅ Conclusion

This project serves as a clear and effective demonstration of Dask's power for scalable data processing. For ETL workloads involving large datasets, Dask provides a robust, scalable, and high-performance alternative to single-machine tools like Pandas. Its familiar API, modeled after Pandas, makes it an accessible tool for data scientists and engineers looking to scale their data pipelines.

