# Data anomaly detection in health data

This coursework project asks whether machine-learning methods can help a health data team identify records or reporting periods that deserve a closer look. It follows the accepted concept paper and uses public datasets as practical stand-ins for a health registry. The project does not use a live or national registry, and its flags are not verified errors.

**GitHub repository:** https://github.com/jeff580/msc7103-health-data-anomaly-detection

The analysis has three parts. First, vital signs are summarized by ICU stay in the eICU demo and scored with a robust MAD baseline, Isolation Forest, and an autoencoder. Second, daily COVID-19 case reports for Uganda and nearby countries are reviewed with rolling median/MAD scores and a regression comparison. Third, the labeled ADBench annthyroid dataset provides a separate holdout comparison of unsupervised scores and supervised classifiers.

## Connection to course topics

The shared course timetable lists regression topics including linear regression, gradient-based fitting, bias-variance, underfitting and overfitting, Ridge/Lasso regularization, cross-validation, and regression metrics. The time-series notebook applies Linear Regression, Ridge, Lasso, and SGD regression to forecast week-to-week changes. It uses an expanding time-series split, compares against a weekly-naive forecast, and reports MAE, RMSE, and R-squared. The results also show why a model must be compared with a simple baseline: the regressions did not generalize as well as the weekly-naive forecast on the later holdout.

The benchmark notebook adds Gaussian Naive Bayes and a Decision Tree as supervised classification comparisons alongside the unsupervised methods. It uses stratified cross-validation for model selection and keeps a final test partition aside. These labels belong to the benchmark only; they are not labels for eICU or local health registry errors.

## Notebooks

- `01_static_eicu.ipynb` - data exploration, aggregation by ICU stay, MAD/Isolation Forest/autoencoder scores, and a held-out synthetic corruption experiment.
- `02_dynamic_owid.ipynb` - daily case series, a rolling robust score, and time-ordered regression forecasting with a weekly-naive baseline.
- `03_adbench_validation.ipynb` - held-out benchmark comparison of MAD, Isolation Forest, an autoencoder, Gaussian Naive Bayes, and a Decision Tree.
- `report_outline.md` - prompts for completing the lecturer-provided report template.

## Data setup

Download each dataset from its source and place the files at these paths. The `.gitignore` excludes `data/`, so raw data are not added to this public repository.

| Dataset | File expected | Source |
|---|---|---|
| eICU demo v2.0 | `data/eicu/vitalPeriodic.csv.gz` | [PhysioNet eICU demo](https://physionet.org/content/eicu-crd-demo/2.0/) |
| OWID COVID cases and deaths | `data/owid/cases_deaths.csv` | [OWID COVID data and metadata](https://docs.owid.io/projects/etl/api/covid/) |
| ADBench annthyroid | `data/adbench/2_annthyroid.npz` | [Official ADBench repository](https://github.com/Minqi824/ADBench), `adbench/datasets/Classical/` |

For each download, check the license and citation requirements. Do not commit source data. The eICU demo is deidentified and open access under its stated license; use the demo rather than the full credentialed eICU database.

## Run the notebooks

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab
```

Open the notebooks in numerical order and run each from top to bottom. The notebooks expect the data paths in the table above. Public data releases can change, so check the printed columns and metadata against the current data file before interpreting results.

## Methods and interpretation

The eICU analysis has no verified labels for data errors. Its synthetic exercise adds a controlled feature shift to held-out stays and checks whether scores rank altered rows above unchanged rows. It evaluates the artificial changes, not clinical validity.

For the time series, rolling MAD compares each day with recent reports. The regression models forecast the weekly change from lagged values and then compare with a one-week-naive forecast. In the current holdout, none of the selected regressions beat the weekly-naive baseline, and test R-squared was negative in all four countries. Regression residual flags should therefore be treated as an unsuccessful comparison in this run, not as validated alerts. The rolling MAD flags also need a human to check reporting notes and context.

On ADBench, the supervised classifiers use training labels; the unsupervised models do not. All metrics are calculated on a separate test partition. This benchmark measures performance on annthyroid only and cannot establish performance on real registry errors.

## Results from the current run

**eICU demo:** 1,634,960 vital-sign rows were aggregated into 2,375 ICU stays. At a 5% review rate, each of the three scoring methods flagged 119 stays. In the held-out synthetic experiment (713 unchanged and 713 altered stays), ROC-AUC / average precision were 0.653 / 0.648 for MAD, 0.676 / 0.601 for Isolation Forest, and 0.813 / 0.801 for the autoencoder. These figures concern only the artificial changes used in this exercise.

**OWID time series:** the rolling MAD method flagged 119 days for Kenya, 78 for Rwanda, 118 for Tanzania, and 155 for Uganda. Each country had 493 later-period test days for regression. The selected models were Linear Regression for Kenya and Lasso for Rwanda, Tanzania, and Uganda. Their test MAE values were 0.0296, 0.0500, 0.0526, and 0.0982 cases per million, while the weekly-naive MAE values were 0.0009, 0.0009, 0.0048, and 0.0023. The regression forecasts did not generalize well to this later period; negative test R-squared values reinforce that result. Eighteen regression residuals were flagged for Tanzania and none for the other countries, but these flags are not validated alerts.

**ADBench annthyroid:** the stratified holdout had 2,160 test rows and a 7.41% anomaly share. Decision Tree achieved ROC-AUC 0.985 and average precision 0.868; Gaussian Naive Bayes scored 0.908 and 0.639. MAD scored 0.953 and 0.651, Isolation Forest 0.820 and 0.333, and the autoencoder 0.451 and 0.063. At a fixed 5% review rate, Decision Tree precision and recall were 0.887 and 0.638. The selected unbounded tree had a higher training cross-validation score than validation/test score, so discuss possible overfitting and the benchmark's limited transferability.

Keep results from the three datasets separate. The notebooks contain detailed tables and plots; report only what the run produced and do not describe the counts as a validated alert rate.

## Setup and submission

Use the lecturer's report template, include the final GitHub repository link, and prepare a 20-minute presentation. Replace the report outline with the provided template before submission. Add group members and their actual contributions according to the course instructions. Keep student numbers and other personal identifiers out of this public repository.

## References

- Johnson, A., Pollard, T., Badawi, O., & Raffa, J. (2019). *eICU Collaborative Research Database Demo (version 2.0).* PhysioNet. https://doi.org/10.13026/gxmm-es70
- Our World in Data. COVID-19 data documentation. https://docs.owid.io/projects/etl/api/covid/
- Han, S., Hu, X., Huang, H., Jiang, M., & Zhao, Y. (2022). *ADBench: Anomaly Detection Benchmark.* NeurIPS. https://github.com/Minqi824/ADBench
