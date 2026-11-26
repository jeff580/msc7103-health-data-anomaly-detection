# Health data anomaly detection

This project looks at whether machine learning can help a health data team decide which records or reporting days to check first. We use three public datasets to evaluate the methods proposed in our concept paper. The data are useful for a prototype, but they are not a live Ugandan health registry. A model flag means “please review this”; it does not prove that a record is wrong.

**Repository:** https://github.com/jeff580/msc7103-health-data-anomaly-detection

## What we did

The project has three parts. In the eICU demo, we combine repeated vital sign readings into one summary for each ICU stay and score unusual stays. For COVID-19 reports from Uganda, Kenya, Rwanda, and Tanzania, we look for days that differ from recent reports and compare regression forecasts with a simple forecast based on the previous week. Finally, we use ADBench's labelled annthyroid dataset to compare anomaly scores with supervised classifiers. We report each part separately because the datasets and evaluation questions are different.

## Notebooks

- `01_static_eicu.ipynb` prepares the eICU vital sign data, summarizes it by stay, and compares MAD, Isolation Forest, and an autoencoder. It also tests whether the methods rank deliberately altered examples as unusual.
- `02_dynamic_owid.ipynb` reviews daily case reports using a rolling MAD score and compares four regression methods with a previous week forecast.
- `03_adbench_validation.ipynb` compares unsupervised anomaly scores with Gaussian Naive Bayes and a Decision Tree on a labelled benchmark.

Across the notebooks, we use robust statistics, regression, Ridge and Lasso regularization, SGD fitting, cross validation, train and test splits, and evaluation measures. The benchmark notebook also shows the difference between supervised learning, which uses training labels, and unsupervised scoring, which does not.

## Data sources

Download the data from the sources below and save the files at the listed paths. The raw data folder is excluded from this public repository, so the datasets are not uploaded here.

| Dataset | File expected | Source |
|---|---|---|
| eICU demo v2.0 | `data/eicu/vitalPeriodic.csv.gz` | [PhysioNet eICU demo](https://physionet.org/content/eicu-crd-demo/2.0/) |
| OWID COVID-19 cases and deaths | `data/owid/cases_deaths.csv` | [Our World in Data COVID-19 data](https://docs.owid.io/projects/etl/api/covid/) |
| ADBench annthyroid | `data/adbench/2_annthyroid.npz` | [ADBench repository](https://github.com/Minqi824/ADBench), `adbench/datasets/Classical/` |

Please check the source pages for current access and citation terms. The eICU demo is deidentified; this is the demo dataset, not the full credentialed eICU database.

## Set up and run

From the project folder, create a Python environment, install the listed packages, and start Jupyter:

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab
```

Open the notebooks in order and run each from top to bottom after placing the data files in the locations above. Public datasets can be updated, so the exact results may change if a newer data release is used.

## What the results tell us

**eICU demo.** We summarized 1,634,960 vital sign readings into 2,375 ICU stays. At a 5% review limit, each scoring method selected 119 stays. In the experiment with deliberately altered examples, ROC-AUC and average precision were 0.653 and 0.648 for MAD, 0.676 and 0.601 for Isolation Forest, and 0.813 and 0.801 for the autoencoder. These scores describe how the methods ranked the artificial changes we introduced. They do not measure detection of confirmed clinical errors.

**COVID-19 reports.** The rolling MAD method flagged 119 days in Kenya, 78 in Rwanda, 118 in Tanzania, and 155 in Uganda. In the later test period, the regression forecasts had higher MAE than the previous week forecast in all four countries, and their test R squared values were negative. In this run, the more complex forecasts did not improve on the simple baseline. Eighteen regression residuals were flagged for Tanzania and none for the other countries; these have not been checked against verified error labels.

**ADBench annthyroid.** The test set had 2,160 rows, of which 7.41% were labelled anomalies. The Decision Tree had ROC-AUC 0.985 and average precision 0.868. At a 5% review limit, its precision was 0.887 and recall was 0.638. These results apply to annthyroid and should not be taken as evidence that the model will perform the same way on registry data.

There is no single accuracy score for the whole project: each dataset answers a different question. The detailed outputs and plots are in the notebooks. Please check the final notebook results before quoting any numbers in the report or presentation.

## Report and presentation

The `report` folder contains the current report files. Use the report template and check its instructions before submission. Add the group members' names and only describe contributions that both members agree are accurate. Include the repository link in the submitted report. Do not put student numbers or other private identifiers in this public repository.

## References

- Johnson, A., Pollard, T., Badawi, O., and Raffa, J. (2019). *eICU Collaborative Research Database Demo (version 2.0).* PhysioNet. https://doi.org/10.13026/gxmm-es70
- Our World in Data. *COVID-19 data documentation.* https://docs.owid.io/projects/etl/api/covid/
- Han, S., Hu, X., Huang, H., Jiang, M., and Zhao, Y. (2022). *ADBench: Anomaly Detection Benchmark.* NeurIPS. https://github.com/Minqi824/ADBench
