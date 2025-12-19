# Used_Cars 
This project analyzes a large used car dataset from Kaggle to identify the key factors influencing vehicle prices. Using a 426K-record subset for scalable modeling, regression and machine learning methods are applied to deliver data-driven pricing insights for a used car dealership.

## Data Source

The dataset used in this project was provided as part of a University of California, Berkeley
Machine Learning course. The data represents a curated subset derived from a publicly
available Kaggle used cars dataset and is intended for educational and non-commercial use.

Original data source:
- Kaggle Used Cars Dataset (derived subset)
- Used in accordance with course and dataset licensing terms

Notebook found here ==> [Jupyter Notebook File](https://github.com/RGConsulting12/Used_Cars/blob/main/Used_Cars-Regression.ipynb)

Modeling Report can be found => [Used Cars Report Markdown File](https://github.com/RGConsulting12/Used_Cars/blob/main/Used_Cars_Report.md)


## Executive Summary

Post data wrangling, approximately 350,000 were analyzed from used vehicle listings to identify the key factors that influence used car prices and to develop a scalable, data-driven pricing model suitable for dealership decision-making. The dataset contains a mix of numerical attributes (e.g., year, mileage, engine size) and high-cardinality categorical features (e.g., manufacturer, model, condition).

Because vehicle prices are heavily right-skewed, prices were modeled using a log(price) transformation to stabilize variance and improve model conditioning. All models were evaluated using 5-fold cross-validation to ensure robust generalization.

A progressive modeling approach was used:
	1.	Baseline linear regression (log-price)
	2.	Regularized linear models (Lasso, Ridge, ElasticNet)
	3.	A nonlinear comparison model (K-Nearest Neighbors)
	4.	Model selection based on predictive accuracy, interpretability, and scalability

Key Findings:

Price decreases are most strongly associated with:
	•	Poor vehicle condition (fair or worse)
	•	High mileage
	•	Older model years
	•	Non-clean titles
	•	Lower engine specifications

Price increases are driven by:
	•	Newer vehicles
	•	Diesel fuel type
	•	Strong brand reputation (e.g., Toyota, Porsche)
	•	High-demand models (e.g., Wrangler, Corvette)
	•	Clean titles
	•	Higher engine capacity

Across all models, the most predictive feature combinations consistently included vehicle age, mileage, condition, brand, model, and mechanical attributes.

Performance Summary:

| Model | RMSE (log) | RMSE ($, multiplicative) |
|------|-----------|----------|
| KNN | 0.449 | 0.567 |
| Ridge | 0.462 | 0.588 |
| ElasticNet | 0.488 | 0.629 |
| Lasso | 0.499 | 0.647 |

The KNN model achieved the lowest prediction error, indicating strong local similarity effects in vehicle pricing. However, KNN was computationally expensive, difficult to scale, and lacked interpretability.

Recommendations:

Ridge regression on log-transformed prices was selected as the final recommended model. While slightly less accurate than KNN, Ridge offers:
	•	Near-optimal predictive performance
	•	Excellent scalability to large datasets
	•	Robust handling of correlated categorical features
	•	Clear operational feasibility for dealership pricing systems

Conclusion:

Used vehicle prices are influenced by many correlated factors rather than a small sparse subset of features. Regularized linear models—particularly Ridge regression—provide the best balance between accuracy, interpretability, and deployability for real-world pricing applications.
