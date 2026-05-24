# Insurance Cost Analysis: EDA, Preprocessing, and Feature Engineering

This project analyzes the `insurance.csv` dataset and builds a clean, model-ready table through:
- Exploratory Data Analysis (EDA)
- Data cleaning and preprocessing
- Feature engineering and extraction
- Basic statistical feature relevance checks

The full workflow is implemented in the notebook:
- `notebooks/dataVisualization.ipynb`

## Dataset

- Source file: `data/insurance.csv`
- Target variable: `charges`
- Original features: `age`, `sex`, `bmi`, `children`, `smoker`, `region`

## What The Notebook Covers

### 1. Exploratory Data Analysis
- Shape, head, info, and summary statistics
- Missing-value checks
- Distribution analysis with histograms
- Categorical frequency plots (`children`, `sex`, `smoker`)
- Outlier checks with boxplots
- Correlation heatmap

### 2. Data Cleaning and Preprocessing
- Copy raw dataframe to avoid mutating original data
- Drop duplicate rows
- Encode binary categorical fields:
  - `sex` -> `is_female` (male=0, female=1)
  - `smoker` -> `is_smoker` (no=0, yes=1)
- One-hot encode `region` with `drop_first=True`
- Convert boolean dummy columns to integer values

### 3. Feature Engineering and Extraction
- Create BMI category bands with `pd.cut`
- One-hot encode BMI category
- Standardize numeric features (`age`, `bmi`, `children`) using `StandardScaler`
- Rank selected features using Pearson correlation with `charges`
- Perform chi-square tests on categorical engineered features against binned `charges`
- Create a compact final feature table (`final_df`)

## Key Insights (From Correlation Analysis)

- `is_smoker` has the strongest positive association with `charges`
- `age` has a moderate positive association with `charges`
- `bmi` has a mild positive association with `charges`
- Region indicators and `is_female` show relatively weak direct linear relationships with `charges`

## Project Structure

```text
Day1/
  data/
    insurance.csv
  notebooks/
    dataVisualization.ipynb
  requirements.txt
```

## Environment Setup

Use the existing virtual environment or create a new one.

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

## Run The Notebook

1. Open `notebooks/dataVisualization.ipynb`
2. Select the `.venv` Python kernel
3. Run cells from top to bottom

## Dependencies

Dependencies are tracked in:
- `requirements.txt`

Main libraries used:
- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `scikit-learn`
- `scipy`

## Notes

- If encoding cells are re-run without resetting `df_cleaned`, mapped columns can become `NaN` due to remapping numeric values.
- Best practice: rerun from the data-copy/preprocessing start cell when re-executing pipeline steps.
