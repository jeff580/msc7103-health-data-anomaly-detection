# Report outline

Use this outline to fill the lecturer's report template. Check every claim against the notebooks and explain the reasoning in your own words.

1. **Title and group members** - use the course format and list the actual contribution of each group member.
2. **Abstract** - summarize the problem, datasets, methods, most important results, and conclusion after analysis is complete.
3. **Problem definition** - explain why unusual health records or reporting periods may need review. State the question and clarify that this project flags unusual patterns; it does not diagnose patients or prove data errors.
4. **Dataset selection** - describe the eICU demo, OWID case series, and ADBench annthyroid subset. State source, version or access date, unit of analysis, columns, license, and citation.
5. **Exploration and preprocessing** - discuss missingness, measurement ranges, feature choice, aggregation by ICU stay, date handling, and exclusions. Explain how you checked units and retained unusual values pending review.
6. **Methods and course concepts** - describe the MAD baseline, Isolation Forest, and autoencoder. Then explain Linear Regression, Ridge, Lasso, and SGD regression for forecasting weekly changes; relate regularization to coefficient shrinkage and bias-variance. Explain time-series cross-validation and the weekly-naive comparator. For ADBench, explain Gaussian Naive Bayes assumptions, Decision Tree splits/depth, stratified cross-validation, and the distinction between supervised classifiers and unsupervised scores.
7. **Evaluation design** - explain the held-out synthetic corruption experiment on eICU, chronological train/test comparison on OWID, and stratified benchmark holdout on ADBench. Specify which labels were used for training and which were reserved for scoring.
8. **Results** - include actual tables and figures from the completed notebooks. Keep results on the three datasets separate. Report ROC-AUC, average precision, precision/recall at the stated review rate, and regression MAE/RMSE/R-squared where applicable.
9. **Interpretation and model comparison** - discuss why the autoencoder performed differently across datasets. Explain that the regression models lost to the weekly-naive forecast on the later OWID holdout and what that suggests about generalization/distribution shift. Treat all flags as review candidates.
10. **Limitations and ethics** - cover the small eICU demo, lack of verified eICU error labels, synthetic corruption assumptions, public-data reporting changes, benchmark transfer limits, class imbalance, privacy, and human review.
11. **Conclusion and future work** - answer the project question using evidence only. Recommend validation with domain-reviewed data quality labels before any operational use.
12. **References and GitHub link** - cite all datasets and methods, and include https://github.com/jeff580/msc7103-health-data-anomaly-detection.

Before exporting, replace this outline with the lecturer's report template, remove prompts/placeholders, check every reported value against the final notebook outputs, and save the PDF using the filename convention in the exam instructions.
