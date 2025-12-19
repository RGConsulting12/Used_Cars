
Used Vehicle Price Modeling Report

Overview and Methodology

This analysis examined a dataset of approximately 350,000 used vehicles to identify the factors that most strongly influence vehicle pricing and to develop a predictive model suitable for dealership pricing decisions. The original dataset included a mix of numerical features (e.g., year, odometer, cylinders) and high-cardinality categorical features (e.g., manufacturer, model, condition).

Vehicle prices were heavily right-skewed, the response variable was transformed using log(price) to stabilize variance and improved model conditioning. All models were evaluated using 5-fold cross-validation to ensure generalization performance.

The modeling workflow followed a progressive approach:
	1.	Baseline linear regression (log-price) to establish a reference.
	2.	Regularized linear models (Lasso, Ridge, ElasticNet) to address multicollinearity and high-dimensional categorical features.
	3.	Nonlinear comparison model (KNN) to evaluate whether local similarity-based pricing improved predictive accuracy.
	4.	Model comparison using RMSE and dollar-interpretable error metrics to balance accuracy, interpretability, and scalability.


Q1: Which predictor variables are most strongly associated with decreases in car price?

Negative associations with price were identified primarily using the Lasso regression model, which performs feature selection by shrinking unimportant coefficients to zero. Because the model was trained on log(price), coefficient signs and magnitudes can be interpreted as approximate percentage effects.

The strongest predictors associated with price decreases include:

- Vehicle condition (Fair or worse)
Vehicles listed in fair condition showed the largest negative coefficients, corresponding to approximately 40–50% lower prices relative to baseline condition categories.
- High odometer readings
Mileage exhibited a consistent negative relationship with price. Higher mileage vehicles command lower prices even after controlling for age and model.
- Older model years
Year was one of the strongest numeric predictors; older vehicles consistently reduced expected price.
- Non-clean title status
Vehicles without a clean title experienced a substantial price penalty, reflecting increased buyer risk.
- Lower engine specifications
Fewer cylinders and lower performance configurations were associated with lower resale values.

These results indicate that vehicle condition, mileage, age, and title quality are the dominant drivers of price depreciation in the used car market.


Q2: Which predictor variables contribute the largest positive effect on car price?

Positive associations with price were identified through coefficient inspection of the Lasso model and corroborated by performance stability in Ridge regression.
- Newer model years
Year was one of the strongest positive predictors, reflecting standard depreciation curves.
- Diesel fuel type
Diesel vehicles showed a significant price premium, likely due to durability and utility in trucks and commercial vehicles.
- Brand effects (Manufacturer)
Brands such as Toyota and Porsche exhibited strong positive price effects, reflecting reliability and luxury premiums.
- Model-specific premiums
Certain models (e.g., Wrangler, Corvette) showed substantial positive coefficients, indicating strong resale demand.
- Clean title status
Clean titles were associated with meaningful price premiums.
- Higher engine capacity (cylinders)
Vehicles with more cylinders tended to command higher prices, capturing performance and class effects.

Given the positive pricing; signals were derived from a combination of the following: vehicle age, fuel type, brand reputation, model desirability, and mechanical capability.


Q3: Which feature combinations produce the most accurate predictions for commonly selected price ranges?

Model performance was evaluated using cross-validated RMSE on log(price) and translated into multiplicative dollar error for interpretability. The following results summarize model performance:

### Model Performance Comparison

| Rank | Model            | RMSE (log) | RMSE ($, multiplicative) |
|------|------------------|------------|--------------------------|
| 1    | KNN (log)        | 0.449      | 0.567                    |
| 2    | Ridge (log)      | 0.462      | 0.588                    |
| 3    | ElasticNet (log) | 0.488      | 0.629                    |
| 4    | Lasso (log)      | 0.499      | 0.647                    |
| 5    | Baseline Linear  | 0.607      | 0.835                    |

Best Performing Feature Combinations
- Age + mileage + condition form the core predictive structure.
- Brand and model indicators significantly refine predictions within popular consumer price ranges.
- Fuel type and engine specifications improve accuracy in mid- to high-price segments.

The KNN model achieved the lowest overall error, indicating that local similarity among vehicles provides strong predictive signal. However, KNN required substantial computation time and lacked interpretability, making it unsuitable for large-scale deployment.

The Ridge regression model achieved nearly equivalent accuracy while remaining computationally efficient and stable. Ridge effectively leveraged many correlated features simultaneously, suggesting that vehicle pricing is influenced by distributed effects rather than a small sparse subset of predictors.

Final Model Selection and Recommendation

Although KNN produced the lowest raw error, Ridge regression on log-transformed prices was selected as the final recommended model due to:
- Near-optimal predictive accuracy
- Excellent scalability to large datasets
- Robust handling of correlated categorical features
- Operational feasibility for dealership pricing systems

Conclusion:
Used car pricing is best modeled using a combination of vehicle age, mileage, condition, brand, model, and mechanical attributes, with regularized linear models providing the optimal balance between accuracy, interpretability, and deployment readiness.
