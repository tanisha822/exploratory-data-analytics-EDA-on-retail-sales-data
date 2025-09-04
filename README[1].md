# Exploratory Data Analysis (EDA) on Retail Sales Data

A complete, ready-to-run data analytics project for retail sales EDA.  
Upload this repository to GitHub and replace the sample data with your own *Dataset 1* and *Dataset 2* (CSV files or direct links).

## Project Structure

```
eda-retail-sales-project/
├─ data/
│  ├─ dataset1_retail_sales.csv              # Sample Dataset 1 (replace with your file or link)
│  └─ dataset2_product_catalog.csv           # Sample Dataset 2 (replace with your file or link)
├─ notebooks/
│  └─ eda_retail_sales.ipynb                 # Main EDA Notebook
├─ reports/
│  └─ eda_report.md                          # Report template
├─ src/
│  └─ helpers.py                             # Helper functions
├─ requirements.txt
└─ .gitignore
```

## How to Use

1. **Create a virtual environment (optional but recommended):**
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # Windows: .venv\Scripts\activate
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Open the notebook:**
   ```bash
   jupyter notebook notebooks/eda_retail_sales.ipynb
   ```

4. **Replace the data:**
   - Put your files at `data/dataset1_retail_sales.csv` and `data/dataset2_product_catalog.csv`, **or**
   - Edit the first cell in the notebook to point to your *Dataset 1 Link* and *Dataset 2 Link* (direct CSV URLs).

## Learning Objectives

- Perform data loading and cleaning
- Compute descriptive statistics (mean, median, mode, std)
- Conduct time series analysis of sales trends
- Analyze customer and product performance
- Build clear visualizations (bar charts, line plots, heatmaps)
- Derive actionable recommendations

## Notes

- The included sample data is synthetic so the notebook runs end-to-end. Replace it with your real datasets when ready.
- Visuals use matplotlib only (no seaborn), matching many exam/lab constraints.