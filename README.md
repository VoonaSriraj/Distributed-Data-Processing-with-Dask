# Distributed Data Processing with Dask

A demonstration of distributed data processing using Dask for efficient handling of large datasets.

## Project Overview

This project showcases the implementation of a scalable ETL (Extract, Transform, Load) pipeline using Dask, a flexible parallel computing library for analytics. The project demonstrates how Dask can be used to process large datasets that don't fit into memory, comparing its performance with traditional pandas operations.

## Key Features

- Parallel data processing with Dask DataFrames
- Performance comparison between Dask and pandas
- Data loading and transformation operations
- Memory-efficient processing of large datasets
- Jupyter notebook with detailed analysis and visualizations

## Tech Stack

- Python 3.7+
- Dask
- pandas
- NumPy
- PyArrow
- Matplotlib (for visualizations)
- Jupyter Notebook

## Repository Structure

```
.
├── Distributed_Data_Processing_with_Dask.ipynb  # Main notebook with analysis
├── main.py                                     # Example script
├── large_dataset.csv                           # Sample dataset
├── requirements.txt                            # Project dependencies
└── pyproject.toml                             # Project configuration
```

## Setup and Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/VoonaSriraj/Distributed-Data-Processing-with-Dask.git
   cd "Distributed Data Processing with Dask"
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv .venv
   .\.venv\Scripts\activate  # Windows
   # or
   source .venv/bin/activate  # macOS/Linux
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## How to Run

### Jupyter Notebook
1. Start Jupyter:
   ```bash
   jupyter notebook
   ```
2. Open `Distributed_Data_Processing_with_Dask.ipynb`
3. Run the cells to see the analysis

### Command Line
The project includes a basic Python script:
```bash
python main.py
```

## Notes and Limitations

- The project is primarily a demonstration and learning resource
- Performance gains from Dask are more noticeable with larger datasets
- The included dataset is a sample; for best results, use larger datasets

## Future Improvements

- Add more complex data transformations
- Include additional performance benchmarks
- Extend with real-time data processing examples
- Add error handling and logging
- Implement unit tests

## License

MIT License

Copyright (c) 2023 Voona Sriraj

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## Author / Maintainer

Voona Sriraj
- [Contributing](#-contributing)
- [License](#-license)
- [Acknowledgements](#-acknowledgements)

## 🌟 Project Overview

This project demonstrates how to leverage Dask for efficient processing of large datasets that don't fit into memory. It provides practical examples of common data processing tasks, performance optimizations, and scaling strategies using Dask's parallel computing capabilities.

Whether you're dealing with data that's too large for pandas or looking to speed up your data processing pipelines, this project serves as both a learning resource and a starting point for building scalable data applications.

## ✨ Features

- **Efficient Data Loading**: Read and process large CSV files that don't fit into memory
- **Parallel Processing**: Leverage multi-core CPUs for faster data processing
- **Familiar API**: Dask DataFrames provide a pandas-like interface for easy adoption
- **Scalable**: Scale from single machine to distributed clusters for larger workloads
- **Interactive Exploration**: Jupyter notebook for interactive data analysis
- **Production-Ready Script**: Command-line interface for automated data processing
- **Modular Design**: Easy to extend with custom processing functions

## 📋 Prerequisites

- Python 3.7+
- pip (Python package manager)
- (Optional) Jupyter Lab/Notebook for interactive development

## 🛠️ Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/VoonaSriraj/Distributed-Data-Processing-with-Dask.git
   cd "Distributed Data Processing with Dask"
   ```

2. **Create and activate a virtual environment** (recommended)

   ```bash
   # Windows
   python -m venv .venv
   .\.venv\Scripts\activate
   
   # macOS/Linux
   python3 -m venv .venv
   source .venv/bin/activate
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```
   
   For development with additional tools:
   ```bash
   pip install -r requirements-dev.txt
   ```

## 🚀 Quickstart

### Option 1: Jupyter Notebook (Interactive)

1. Start Jupyter Lab/Notebook:
   ```bash
   jupyter lab  # or jupyter notebook
   ```
2. Open `Distributed_Data_Processing_with_Dask.ipynb`
3. Run the cells interactively

### Option 2: Command Line

```bash
python main.py --input data/large_dataset.csv --output results/processed_data.parquet
```

## 📁 Project Structure

```
.
├── data/                   # Directory for input data files
│   └── large_dataset.csv   # Example dataset
├── notebooks/              # Jupyter notebooks
│   └── Distributed_Data_Processing_with_Dask.ipynb
├── src/                    # Source code
│   └── main.py             # Main processing script
├── tests/                  # Unit and integration tests
├── results/                # Output directory for processed data
├── .gitignore              # Git ignore file
├── requirements.txt        # Production dependencies
├── requirements-dev.txt    # Development dependencies
└── README.md              # This file
```

## 💻 Usage

### Processing Data

```python
from src.processor import process_data

# Process data with default parameters
df_processed = process_data('data/large_dataset.csv')

# Process with custom chunk size
df_processed = process_data('data/large_dataset.csv', chunksize=100000)
```

### Available Script Options

```bash
python main.py --help

Options:
  --input TEXT       Input file path (CSV)  [required]
  --output TEXT      Output file path (CSV/Parquet)  [required]
  --chunksize INTEGER  Number of rows per partition  [default: 100000]
  --help             Show this message and exit.
```

## ⚡ Running with Dask Distributed

For larger datasets, you can leverage Dask's distributed scheduler:

1. **Install additional dependencies**:
   ```bash
   pip install dask[complete] distributed
   ```

2. **Start a local cluster**:
   ```bash
   # Terminal 1: Start the scheduler
   dask-scheduler
   
   # Terminal 2: Start workers (adjust nprocs as needed)
   dask-worker localhost:8786 --nprocs 4 --nthreads 2
   ```

3. **Connect to the cluster in your code**:
   ```python
   from dask.distributed import Client
   
   # Connect to the scheduler
   client = Client('localhost:8786')
   
   # Your Dask code here
   ```

## 🚀 Performance Tips

1. **Partition Size**: Adjust chunk size based on your available memory
2. **Use Efficient Data Types**: Convert to appropriate data types to reduce memory usage
3. **Persist Frequently Used Data**: Use `client.persist()` for data reused in multiple operations
4. **Monitor Performance**: Use Dask's built-in dashboard for performance monitoring
   ```python
   # Print dashboard link
   print(client.dashboard_link)
   ```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgements

- [Dask](https://dask.org/) - For the amazing parallel computing library
- [Pandas](https://pandas.pydata.org/) - For the inspiration and API design
- [NumFOCUS](https://numfocus.org/) - For supporting open-source scientific computing

## 🤝 Contributing

Contributions are welcome! Please open issues or pull requests on the repository. Keep changes focused and add tests where appropriate.

---

## 📝 License

Add your license here (e.g., MIT). If you want me to add a license file, tell me which license to use and I'll add it.

---

## 📬 Contact

Maintainer: `VoonaSriraj` — see the repository for contact details.

---

If you'd like, I can also:

- Add badges (build / license)
- Add a short usage example from `main.py` to the README
- Add a LICENSE file (e.g., MIT)

Let me know which of the above you'd like to include. ✨
