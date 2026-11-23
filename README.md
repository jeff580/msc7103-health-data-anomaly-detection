# Data anomaly detection in health data

This coursework project explores a practical question: can anomaly scores help health data teams find records or reporting periods that deserve a closer look? It follows the accepted concept paper while keeping the analysis small enough to explain and reproduce. The public datasets are stand-ins for the cloud registry setting; the project does not use a live or national health registry.

**GitHub repository:** https://github.com/jeff580/msc7103-health-data-anomaly-detection

The project has three related parts. The static analysis summarizes vital signs by ICU stay in the eICU demo and compares Isolation Forest with an autoencoder. The dynamic analysis looks for unusual daily changes in reported COVID-19 cases for Uganda and nearby countries. A small labeled ADBench healthcare dataset provides a separate check of how the two models rank known benchmark anomalies. Results from these different datasets should be discussed separately; none proves that a health registry error has been found.

## Notebooks

- `01_static_eicu.ipynb` - static analysis using the eICU demo. It includes preprocessing, exploratory checks, model scores, flagged stays, and a held-out synthetic corruption exercise.
- `02_dynamic_owid.ipynb` - time-series analysis using OWID daily case reports and a rolling median/MAD score.
- `03_adbench_validation.ipynb` - labeled benchmark comparison with Isolation Forest and an autoencoder.
- `report_outline.md` - report structure to adapt to the instructor-provided template.

## Data setup

Download each dataset from its source and place the files at these paths. The `.gitignore` excludes `data/`, so raw data will not be added to the repository.

| Dataset | File expected | Source |
|---|---|---|
| eICU demo v2.0 | `data/eicu/vitalPeriodic.csv.gz` | [PhysioNet eICU demo](https://physionet.org/content/eicu-crd-demo/2.0/) |
| OWID COVID cases and deaths | `data/owid/cases_deaths.csv` | [OWID COVID data and metadata](https://docs.owid.io/projects/etl/api/covid/) |
| ADBench annthyroid | `data/adbench/2_annthyroid.npz` | [Official ADBench repository](https://github.com/Minqi824/ADBench), `adbench/datasets/Classical/` |

For each download, check the accompanying license and citation requirements. Do not commit source data. The eICU demo is deidentified and open access under its stated license; use the small demo for this coursework rather than the full credentialed eICU database.

## Run the notebooks

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab
```

Open the notebooks in numerical order and run each from top to bottom. The notebooks expect the data paths in the table above. Check the printed columns against the current data file; public data releases can change. Save figures and actual metric outputs for the report only after you run the notebooks.

## Evaluation and interpretation

Isolation Forest and the autoencoder produce anomaly scores. They do not produce verified error labels. In the eICU notebook, the synthetic exercise adds known changes to held-out records and measures whether the scores rank those changes highly. In the ADBench notebook, benchmark labels are withheld from model fitting and used only to calculate metrics. Neither evaluation establishes performance on real health-registry errors.

For the daily time series, a rolling robust score flags periods that depart from recent reports. Reporting changes, backlogs, missing values, and genuine shifts can all create unusual patterns. A health data manager should review the source and context before deciding what a flag means.

## Results from the current run

All three notebooks ran successfully with the data versions described above. The eICU demo supplied 1,634,960 vital-sign rows, aggregated into 2,375 ICU stays. At a 5% review rate, the MAD baseline, Isolation Forest, and autoencoder each flagged 119 stays. In the held-out synthetic corruption exercise (713 unchanged and 713 altered stays), ROC-AUC / average precision were 0.653 / 0.648 for MAD, 0.676 / 0.601 for Isolation Forest, and 0.813 / 0.801 for the autoencoder. These scores describe the artificial changes used in that exercise only.

On the labeled ADBench annthyroid benchmark, Isolation Forest scored 0.802 ROC-AUC and 0.289 average precision; the autoencoder scored 0.462 and 0.065. At the same 5% flag rate, Isolation Forest precision and recall were 0.367 and 0.247. The autoencoder did not perform well on this dataset. This is a useful result to report honestly, and it shows that one model did not work equally well on both tasks.

The OWID rolling method flagged 119 days for Kenya, 78 for Rwanda, 118 for Tanzania, and 155 for Uganda. These historical flags can reflect reporting changes or genuine shifts as well as data problems. The notebooks contain the detailed tables and figures; do not treat this count as a validated alert rate.

## Setup and submission

Use the lecturer's report template, include the final GitHub repository link, and prepare a 20-minute presentation. The results above came from this run; rerun the notebooks if you change the data or code, then update the report to match. Add group members in the report according to the course instructions. Keep student numbers and other personal identifiers out of this public repository.

## References

- Johnson, A., Pollard, T., Badawi, O., & Raffa, J. (2019). *eICU Collaborative Research Database Demo (version 2.0).* PhysioNet. https://doi.org/10.13026/gxmm-es70
- Our World in Data. COVID-19 data documentation. https://docs.owid.io/projects/etl/api/covid/
- Han, S., Hu, X., Huang, H., Jiang, M., & Zhao, Y. (2022). *ADBench: Anomaly Detection Benchmark.* NeurIPS. https://github.com/Minqi824/ADBench
