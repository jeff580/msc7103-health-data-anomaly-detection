# Notes for completing the project report

Use the course report template and these notes to check that we have explained the main parts of our project. Write the final explanations in your own words and compare each number with the completed notebooks.

1. **Problem:** Explain that we are looking for unusual health records or reporting days that may need a person's review. A flag is not a diagnosis or proof of an error.
2. **Data:** Introduce the eICU demo, Our World in Data case reports, and the ADBench annthyroid benchmark. Give the source, unit of analysis, main fields, and citation for each.
3. **Preparation and exploration:** Explain how we handled missing values, dates, vital sign summaries, feature scaling, and the training and test groups.
4. **Methods:** Describe MAD, Isolation Forest, and the autoencoder. Then explain the regression methods (Linear Regression, Ridge, Lasso, and SGD) and the benchmark classifiers (Gaussian Naive Bayes and Decision Tree). Connect these to topics covered in class.
5. **Evaluation:** Describe the synthetic eICU check, the time ordered COVID-19 forecast comparison, and the held aside annthyroid test set. Explain which models used labels and when.
6. **Results:** Include the actual tables or figures and use the right measures for each task. Keep the three datasets separate; they do not produce one overall accuracy score.
7. **Discussion:** Explain what the results mean, including where a simple baseline did better and why a method may perform differently across datasets. Treat unverified flags as candidates for review.
8. **Limitations and ethics:** Mention the lack of confirmed eICU error labels, the artificial changes in the eICU test, the country level nature of COVID-19 reports, and the limits of applying benchmark results to a health registry.
9. **Conclusion and future work:** Answer the project question using the results. Explain what additional reviewed data would be needed before these methods could be used in practice.
10. **References and repository:** Cite datasets and methods, include the GitHub link, and follow the exam paper's requirements for the report and presentation.

Before submission, check the course template, remove these notes from the report, and make sure any group member or contribution details are accurate and required by the template.
