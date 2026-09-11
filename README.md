<div align="center">
  <h1>SKU Variant Analysis</h1>
  <p><strong>Selecting three HMUG variants for standalone listing tests</strong></p>

  <p align="center">
    <img src="https://img.shields.io/badge/Domain-E--commerce-0D47A1?style=flat-square" alt="Domain E-commerce">
    <img src="https://img.shields.io/badge/Analysis-Descriptive-17785D?style=flat-square" alt="Descriptive Analysis">
    <img src="https://img.shields.io/badge/Status-Completed-success?style=flat-square" alt="Status Completed">
  </p>

  <p align="center">
    A June to August 2026 sales analysis designed to reduce catalog dependence on a single parent SKU. The project covers data quality auditing, duplicate-value reconciliation, candidate ranking, sensitivity analysis, and business recommendations.
  </p>
</div>

## Tech Stack

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626.svg?style=for-the-badge&logo=Jupyter&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-ffffff?style=for-the-badge&logo=Matplotlib&logoColor=black)

## Overview

The store carries 2,830 SKUs, yet 49.8% of its revenue comes from only three parent SKUs. HMUG is one of the largest contributors and remains heavily concentrated in a single leading variant.

This analysis identifies at least three HMUG variants with the strongest sales evidence for standalone listing tests. A standalone listing gives each variant its own product page so its performance, inventory, advertising, and promotions can be evaluated independently.

## Key Findings

- Total store revenue over the three-month period was Rp816,449,942.
- Raw HMUG variant records totaled Rp259,906,900 and contained Rp82,201,479 in excess duplicated values.
- After counting each identical value group once, HMUG revenue reconciled to Rp177,705,421 with a monthly difference of Rp0.
- Of 38 HMUG variants, 25 had `Normal` status and 8 met every candidate requirement.
- A01/01 and C01/03 ranked in the top three across all six robustness tests.
- D02/01 ranked in the top three in four of six tests and was retained because its revenue was fully attributable.

## Recommendations

| Priority | Variant | Confirmed revenue | Units | Robustness |
|---:|---|---:|---:|---:|
| 1 | A01/01 | Rp94,297,119 | 629 | 6 of 6 tests |
| 2 | C01/03 | Rp12,827,862 | 71 | 6 of 6 tests |
| 3 | D02/01 | Rp8,446,915 | 44 | 4 of 6 tests |

These recommendations are priorities for standalone listing tests, not guarantees of additional revenue. Actual impact must be measured through a pilot or controlled experiment.

## Method

1. Audit workbook structure, data types, missing values, key duplication, variant status, and total consistency.
2. Identify sales and unit combinations repeated exactly across multiple variants.
3. Apply a conservative attribution rule that does not credit ambiguous revenue to primary candidates.
4. Retain variants with `Normal` status, fully attributable revenue, and positive sales in all three months.
5. Rank candidates by revenue, units, median monthly revenue, and weakest-month revenue.
6. Test robustness through three attribution scenarios and three leave-one-month-out evaluations.
7. Evaluate catalog concentration and business impact scenarios without presenting them as forecasts.

See the [methodology document](docs/methodology.md) for the complete analytical rationale and limitations.

## Repository Structure

```text
data/raw/                              Source workbook
notebooks/sku_variant_analysis.ipynb   Main analysis and saved outputs
reports/sku_variant_recommendation.pdf Analysis presentation
docs/methodology.md                    Methods, assumptions, and limitations
```

## Running the Notebook

Clone the repository and enter its directory:

```bash
git clone https://github.com/ababilkhoerulimam/sku-variant-analysis.git
cd sku-variant-analysis
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it with Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

On macOS or Linux:

```bash
source .venv/bin/activate
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

Launch Jupyter from the repository root and open `notebooks/sku_variant_analysis.ipynb`:

```bash
jupyter lab
```

The notebook can also be launched from the `notebooks` directory because its source-file lookup supports both working directories.

## Project Files

- [Analysis notebook](notebooks/sku_variant_analysis.ipynb)
- [Recommendation presentation](reports/sku_variant_recommendation.pdf)
- [Methodology and limitations](docs/methodology.md)

## Limitations

- The dataset covers only three months, and August is recorded through the 28th.
- No transaction ID is available to identify the true owner of repeated variant values.
- The data does not include COGS, marketplace fees, advertising spend, returns, or inventory availability.
- ASP is not a profit margin, and the what-if scenarios are not forecasts.
- A launch decision still requires inventory-readiness validation and a business experiment.

## License

This repository is available under the [MIT License](LICENSE).
