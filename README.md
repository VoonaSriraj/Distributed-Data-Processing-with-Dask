# Distributed Data Processing with Dask 🚀

**A small demo project showing how to use Dask to process large CSV datasets in Python.**

---

## 🔧 Project Overview

This repository contains a Jupyter notebook and a small script demonstrating distributed or parallel data processing using Dask. It is intended as a learning resource and a starting point for handling large tabular datasets.

Files of interest:

- `Distributed_Data_Processing_with_Dask.ipynb` — interactive notebook walkthrough
- `main.py` — example script to run processing tasks from the command line
- `large_dataset.csv` — example dataset used by the notebook/script
- `requirements.txt` — Python dependencies

---

## ✅ Features

- Read large CSV files with Dask
- Parallelize common ETL tasks (filtering, aggregation, joins)
- Demonstrates local Dask usage and an introduction to the Dask distributed scheduler

---

## 🚀 Quickstart

1. Clone the repository

   ```bash
   git clone https://github.com/VoonaSriraj/Distributed-Data-Processing-with-Dask.git
   cd "Distributed Data Processing with Dask"
   ```

2. Create and activate a virtual environment (recommended)

   ```bash
   python -m venv .venv
   .\.venv\Scripts\activate   # Windows
   # macOS / Linux: source .venv/bin/activate
   ```

3. Install dependencies

   ```bash
   pip install -r requirements.txt
   ```

4. Open the notebook

   - Launch Jupyter: `jupyter notebook` or `jupyter lab`, then open `Distributed_Data_Processing_with_Dask.ipynb`

5. Run the example script

   ```bash
   python main.py
   ```

---

## ⚙️ Running with Dask Distributed (optional)

For larger workloads you can run a Dask scheduler and workers locally or on a cluster.

Install the extras (if not already in `requirements.txt`):

```bash
pip install dask[complete] distributed
```

Start a local scheduler and worker in separate terminals:

```bash
dask-scheduler
dask-worker <scheduler-address>
```

Or create a local client inside Python:

```python
from dask.distributed import Client
client = Client()  # starts a local cluster
```

---

## 🧾 Data

The example dataset is `large_dataset.csv`. If the dataset is not present, update the notebook or `main.py` to point to your data source.

---

## 🛠️ Development

- Formatting: use `black` or your preferred formatter
- Tests: none included (feel free to add unit tests or integration tests)

---

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
