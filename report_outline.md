# Report outline

Use this outline to fill the lecturer's report template. Write the findings from your own notebook outputs and explain them in your own words.

1. **Title and group members**
2. **Abstract** - summarize the problem, three data sources, methods, main results, and conclusion after analysis is complete.
3. **Problem definition** - describe record-level and reporting-period anomalies and why a health data manager may want a review list. State the project question and the boundary: the system flags unusual data; it does not diagnose patients or prove data errors.
4. **Dataset selection** - describe the eICU demo, OWID COVID case series, and selected ADBench healthcare subset. Give source, version/date accessed, unit of analysis, relevant columns, data license, and citation for each.
5. **Data exploration and preprocessing** - describe missingness, duplicate handling, units, selected features, aggregation by ICU stay, date handling, and any exclusions. Explain why each step was needed.
6. **Methods** - explain Isolation Forest, the autoencoder reconstruction score, and rolling median/MAD for the time-series part. State how scores become flags and why thresholds are practical comparison choices rather than approved operating rules.
7. **Evaluation** - report the synthetic corruption experiment for eICU, ranking metrics from the labeled ADBench dataset, and the time-series examples. Explain which labels were used only for evaluation and what each evaluation can and cannot support.
8. **Results** - include actual tables and figures from the completed notebooks. Compare methods on the same dataset; keep results across the three datasets separate.
9. **Interpretation** - discuss representative flags, whether they may be errors or valid extremes, and what a data manager would check next.
10. **Limitations and ethics** - cover the small eICU demo sample, no verified eICU error labels, synthetic corruption assumptions, benchmark transfer limits, reporting changes, privacy, and the need for human review.
11. **Conclusion and future work** - answer the project question based on the evidence; suggest domain review and validation with real registry quality labels.
12. **References and GitHub link** - include all data and method citations plus the repository URL.

Before exporting, replace this outline with the course report template, check every result against the notebook, remove any placeholder text, and save the submitted PDF using the filename convention in the exam instructions.
