# Notes for completing the project report

Use the report template and use these notes to check that the main parts of our work are explained. Write the final explanations in your own words and compare every reported number with the completed notebooks.

1. **Problem:** Explain that we are looking for unusual health records or reporting days that may need review. State clearly that a flag is not a diagnosis or proof of an error.
2. **Data:** Introduce the eICU demo, Our World in Data case reports, and the ADBench annthyroid benchmark. Give the source, unit of analysis, relevant fields, and citation for each.
3. **Preparation and exploration:** Explain how we handled missing values, dates, vital sign summaries, feature scaling, and the training and test partitions.
4. **Methods:** Describe MAD, Isolation Forest, and the autoencoder. Explain the regression comparisons (Linear Regression, Ridge, Lasso, and SGD) and the supervised benchmark methods (Gaussian Naive Bayes and Decision Tree). Explain why these methods fit the problem and distinguish anomaly scoring from forecasting and supervised classification.
5. **Evaluation:** Describe the synthetic eICU check, the time ordered COVID forecast comparison, and the held aside annthyroid test set. Say which methods used labels and when.
6. **Results:** Show the actual tables or figures and use the right measures for each task. Keep the three datasets' results separate; they are not one overall accuracy score.
7. **Discussion:** Explain what the results mean, including where a simple baseline did better and where performance differed between datasets. Treat unverified flags as suggestions for review.
8. **Limitations and ethics:** Mention the lack of confirmed eICU error labels, the artificial changes in the eICU test, the country level nature of COVID reports, and the limits of applying benchmark results to a health registry.
9. **Conclusion and future work:** Answer the project question using the results. Explain what additional reviewed data would be needed before the methods could be used in practice.
10. **References and repository:** Cite datasets and methods, include the GitHub link, and follow the exam paper's instructions for the final report and presentation.

Before submission, remove these notes from the report and check the report template. If it asks for group contributions, include only an accurate account agreed by both group members.
