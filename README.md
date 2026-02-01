# Airbnb Pricing Model: Milan Case Study

## Business Case
This project aims to develop a robust pricing model for a chain of Airbnb rentals to optimize revenue. Operating a chain of short-term rentals requires an accurate understanding of price drivers to remain competitive while maximizing occupancy. Using data from **Inside Airbnb**, we focus on **Milan** as our primary market and evaluate the model's validity across different time periods and a different geographic location (**Venice**).

<<<<<<< HEAD
## Repository Structure
* `data/raw`: Folder containing raw CSV datasets:
    * `milan_listings.csv`: Core dataset for model training (Earlier quarter).
    * `milan_listings_2.csv`: Dataset for time validity check (Later quarter).
    * `venice_listings.csv`: Dataset for spatial validity check (Other city).
* `airbnb_milan_model.ipynb`: The main Jupyter Notebook containing the full workflow: data wrangling, feature engineering, modeling, and external validation.
* `requirements.txt`: List of Python dependencies required for a reproducible environment.
* `README.md`: Project documentation and business discussion.
=======
## Project Structure

Data Analysis 3/
│
├── data
│ ├── milan_listings.csv 
│ ├── milan_listings_2.csv
│ ├── venice_listings.csv
├── airbnb_milan_models.ipynb 
├── README.md
├── requirements.txt
├── .gitignore

>>>>>>> dc444a3 (Airbnb pricing models)

## Requirements
This project requires daenv (Python 3.12.4) and the libraries listed in `requirements.txt`. 

<<<<<<< HEAD
## Models
We compared 5 different predictive models to find the best fit for Airbnb pricing:

- OLS (Ordinary Least Squares): Baseline linear regression.

- LASSO: Regularized regression using an extended set of predictors and interaction terms.

- Random Forest: An ensemble of decision trees tuned via GridSearchCV.

- GBM (Gradient Boosting Machine): Capturing complex non-linear relationships.

- LightGBM: Gradient boosting framework optimized for speed and performance.
=======
## Data

The data comes from [Inside Airbnb](http://insideairbnb.com).

- **Milan (Italy)**  
  - Earlier quarter (training sample)  
  - Later quarter (temporal validation)  
  - ~20,000 listings

- **Venice (Italy)**  
  - External geographic validation  
  - >3,000 listings

All datasets are publicly available and included in the repository for reproducibility.

## Part I — Modelling

### Feature Engineering

- Log transformation of price (`log_price`)
- Numerical features prefixed with `n_`
- Categorical features prefixed with `f_`
- Binary indicators prefixed with `flag_`
- Interaction terms between key variables
- Dummy encoding handled via `patsy`

The design matrix is constructed using a formula-based approach to ensure consistency and transparency.
>>>>>>> dc444a3 (Airbnb pricing models)

## Variable selection

Before modeling, I considered which factors economically drive Airbnb prices.

Location & accessibility: Central or attractive neighborhoods command higher prices
- latitude
- longitude
- neighbourhood

Listing type & privacy: Entire homes are priced higher than private/shared rooms
- room_type

Demand & reputation: Popular and well-reviewed listings can charge higher prices
- number_of_reviews
- reviews_per_month
- number_of_reviews_ltm
- last review

Availability & restrictions: Scarcity and booking constraints affect pricing
- availability_365
- minimum_nights

Host professionalism: Hosts managing multiple listings may apply systematic pricing
- calculated_host_listings_count
<<<<<<< HEAD
=======


## Models
We compared 5 different predictive models to find the best fit for Airbnb pricing:

- OLS (Ordinary Least Squares): Baseline linear regression.

- LASSO: Regularized regression using an extended set of predictors and interaction terms.

- Random Forest: An ensemble of decision trees tuned via GridSearchCV.

- GBM (Gradient Boosting Machine): Capturing complex non-linear relationships.

- LightGBM: Gradient boosting framework optimized for speed and performance.

Models are compared using RMSE and R² on a held-out test set.

### Model Comparison

A horserace table summarizes predictive performance. Tree-based models outperform linear models in-sample, while regularization improves generalization for linear approaches.

---

### Model Interpretation

Random Forest and LightGBM are analyzed in detail:

- Feature importance is extracted
- Top 10 predictors are compared
- Differences in variable relevance are discussed

---

## Part II — Validity

### Temporal Validity

All models are applied to a later quarter of Milan data using the same design matrix structure as the training sample.

### Geographic Validity

Models trained on Milan are applied to Venice listings. Unseen neighbourhood categories are recoded as `"Other"` to preserve compatibility.

Performance deterioration across cities highlights the limits of geographic transportability.

---

## Key Findings

1. Model performance on the initial Milan dataset

On the initial Milan dataset, tree-based ensemble models clearly outperformed linear models. LightGBM achieved the best predictive performance, with the lowest RMSE and the highest R², while also maintaining relatively low computation time. Random Forest and Gradient Boosting also performed well, confirming the importance of capturing non-linear relationships in Airbnb pricing. OLS and LASSO served as useful baselines but showed limited explanatory power, with substantially lower R² values.Overall, the horserace comparison demonstrated that price formation in the Airbnb market is highly non-linear, making machine learning models more suitable than classical linear approaches.

2. Model stability over time: Later Milan dataset

When applying the trained models to a later Milan dataset, predictive performance declined moderately but remained meaningful: Random Forest and LightGBM preserved relatively high explanatory power, indicating good temporal stability. Linear models showed only marginal changes, but their overall performance remained weak. This suggests that pricing patterns in Milan are reasonably stable over time, and that ensemble models are capable of generalizing to future periods within the same city.

3. Geographical validity: Venice dataset

In contrast, applying the Milan-trained models to Venice revealed a sharp deterioration in performance: All models, including Random Forest and LightGBM, exhibited high RMSE and negative R² values. This indicates that the models failed to generalize across cities, even within the same country. The result highlights strong location-specific dynamics in Airbnb pricing. Differences in tourism structure, housing stock, seasonality, and neighborhood effects make city-level transferability extremely limited.
---


>>>>>>> dc444a3 (Airbnb pricing models)
