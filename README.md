# Mosaic Summit Analysis System

A Python-based recommendation and analysis engine for investor-company meeting requests. This system provides intelligent company recommendations and cohort-based behavioral analysis for financial conference organizers.

## Features

### Company Recommendations
- **Pairwise Method**: Correlation-based recommendations using company request patterns
- **Multivector Method**: Collaborative filtering using investor similarity profiles
- Generates top-N recommendations based on historical meeting request patterns

### Cohort Analysis
- Time-based investor grouping (daily, weekly, monthly, quarterly)
- Cohort retention tracking and behavioral analysis
- Early adopter pattern identification
- Cohort-specific recommendation generation

### Model Evaluation
- Train/validation split evaluation framework
- Accuracy metrics (precision, recall, F1-score, hit rate)
- Method comparison tools
- Cross-validation support

## Quick Start

### Prerequisites
- Python 3.13+
- Required packages: pandas, numpy, scikit-learn, openpyxl, plotly

### Installation

```bash
# Clone the repository
git clone <your-repo-url>
cd Learning/mosaicproj

# Create and activate virtual environment
python -m venv mosaic_env
source mosaic_env/bin/activate  # On Windows: mosaic_env\Scripts\activate

# Install dependencies
pip install pandas numpy scikit-learn openpyxl plotly
```

### Usage

Run the main interactive system:

```bash
python main.py
```

The system will prompt you to:
1. Choose analysis type (Company Recommendations or Cohort Analysis)
2. Enter source company ID
3. Select recommendation method
4. View results

## Project Structure

```
mosaicproj/
├── main.py                      # Main entry point
├── engines/
│   ├── recommender_engine.py    # Core recommendation algorithms
│   ├── cohort_analysis.py       # Cohort analysis engine
│   ├── model_evaluator.py       # Evaluation framework
│   └── recommender_helpers.py   # Utility functions
├── data/                        # Input data files
├── simple_recommender_test.py   # Simple evaluation script
└── test_recommender_accuracy.py # Advanced evaluation script
```

## Example Use Cases

### Generate Company Recommendations

```python
from engines.recommender_engine import recommend
import pandas as pd

# Load data
df = pd.read_excel("data/Conf 2024 Request List Update.xlsx")

# Get recommendations for investor ID 1000
recommendations = recommend(
    df, 
    source_company_id=1000,
    method='multivector',  # or 'pairwise'
    top_n=10
)
```

### Run Cohort Analysis

```python
from engines.cohort_analysis import CohortAnalyzer

analyzer = CohortAnalyzer(df)
cohorts = analyzer.define_cohorts(cohort_period='M', min_requests=2)
cohort_matrix = analyzer.create_cohort_matrix()
behavior = analyzer.analyze_cohort_behavior()
```

### Evaluate Model Accuracy

```bash
# Simple evaluation
python simple_recommender_test.py

# Advanced evaluation with metrics
python test_recommender_accuracy.py
```

## Recommendation Methods

### Pairwise Correlation
Finds companies that are frequently requested together by analyzing correlation patterns. Best for identifying companies with similar investor appeal.

### Multivector Collaborative Filtering
Uses cosine similarity between investor profiles to find similar investors and recommend companies they've requested. More sophisticated and handles sparse data better.

## Data Format

The system expects an Excel file with the following columns:
- `Source Company`: Investor/company making the request
- `Target Company`: Company being requested for a meeting
- `Request Date`: Date of the meeting request

## Output

- **Recommendations**: Ranked list of companies with similarity/correlation scores
- **Cohort Analysis**: Retention matrices, behavioral patterns, and cohort-specific insights
- **Evaluation Results**: CSV files with accuracy metrics and test results

## Documentation

Detailed documentation available in `read_mes/`:
- `COHORT_ANALYSIS_README.md` - Comprehensive cohort analysis guide
- `RECOMMENDER_EVALUATION_README.md` - Evaluation framework documentation
