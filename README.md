# Housing Price Prediction – Taiwan Real Estate

### This project focuses on predicting residential property prices in Taiwan using supervised machine learning techniques. The objective was to identify the key drivers of housing prices and build models capable of generating accurate out-of-sample predictions.

## Project Overview

Using the Taiwan Real Estate Valuation dataset, the workflow included:

	•	Data cleaning and preprocessing
	•	Exploratory data analysis (EDA)
	•	Feature engineering
	•	Model training and comparison
	•	Performance evaluation

The dataset contains variables such as transaction date, house age, distance to MRT stations, number of nearby convenience stores, and geographic coordinates. The target variable is house price per unit area.



**Models Implemented**

	•	Linear Regression
	•	Random Forest Regressor
	•	Gradient Boosting Regressor

**Model performance was evaluated using:**

	•	R² (coefficient of determination)
	•	Mean Squared Error (MSE)
	•	Cross-validation to ensure robustness


**Results**

	•	Tree-based ensemble models significantly outperformed linear regression.
	•	Gradient Boosting achieved the strongest predictive performance, delivering the highest R² and lowest MSE among the tested models.
	•	Random Forest also performed well, capturing nonlinear patterns that linear regression could not fully model.
	•	Linear regression provided a useful baseline but struggled with complex interactions between features.

**Feature importance analysis revealed that:**

	•	Distance to MRT stations was one of the strongest predictors of property value.
	•	The number of nearby convenience stores had a positive relationship with prices.
	•	House age showed a negative correlation with price per unit area.

Overall, ensemble methods demonstrated superior ability to model nonlinear relationships and feature interactions present in real estate pricing data.



## **Conclusion**

This project highlights the importance of model selection in regression problems involving structured, real-world data.

While linear regression offers interpretability and simplicity, ensemble methods such as Random Forest and Gradient Boosting provide substantially better predictive performance when relationships are nonlinear.

Key takeaways:

	•	Location-based variables play a critical role in price determination.
	•	Nonlinear modeling techniques can meaningfully improve prediction accuracy.
	•	Cross-validation is essential to obtain reliable performance estimates.

This project demonstrates a complete end-to-end machine learning workflow, from data exploration to model comparison and interpretation, with a strong focus on both predictive accuracy and practical insight.
