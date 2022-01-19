# Budget Analysis for King County Healing Association
![kcha_logo](https://github.com/sabinabains/dsc-phase-2-project/blob/main/images/kcha_logo.png)

King County Healing Association is an established nonprofit organization that has a variety of successful initiatives such as rehabilitation centers, medical assistance, career services, and temporary housing for those re-entering their communities. **The organization now wants to expand on their housing opportunities and needs our help estimating a budget for a program that helps eliminate bias in the housing process against those who are prepared to transition into a permanent residence**

Unfortunately, those with criminal records tend to be discriminated against even after serving their sentence, and often banks do not lend money to these individuals. Additionally, those previously incarcerated could have bad credit or a lack of savings. Because of all this, KCHA plans to borrow from banks themselves and provide the down payment for applicants of this program. The new tenants can then pay off their mortgage to KCHA monthly, while additionally paying back the down payment over time. KCHA would ideally choose a **budget of 500k** for the first year. 

Along with requirements to ensure the applicants have a stable income and can pay off their debt, KCHA requires tenants to choose homes within the same zipcode of their parole officer (if applicable).

KCHA doesn't plan to launch this service for another 3 years, and therefore are in the preliminary stages. The organization estimates they will assist 5 families in their first year of the program, and would like our help estimating the total down payment cost based on these family's parole office location, household size, and general preferences.

Details of the 5 Family's being considered for the first year of this program:
* Family 1 would like a 3 bedroom, 2 bathroom house in zipcode 98011. They prefer a basement and a home quality of at least 6/13
* Family 3 would like a 2 bedroom, 1 bathroom house in zipcode 98032. They would prefer a home quality of at least 10/13
* Family 3 would like a 1 bedroom, 1 bathroom house in zipcode 98045. They would prefer a home quality of at least 8/13
* Family 4 would like a 4 bedroom, 3 bathroom house in zipcode 98112. They prefer a basement and a home quality of at least 6/13
* Family 5 would like a 1 bedroom, 2 bathroom house in zipcode 98001. They would prefer a home quality of at least 5/13

## Methodology and Modeling

This dataset ([linked here](https://www.kaggle.com/harlfoxem/housesalesprediction)) contains house sale prices for King County, Washington. The dataset has a sample of 21,597 homes sold between May 2014 and May 2015, and has the following columns:

* id : A notation for a house
* date: Date house was sold
* price: Price is prediction target
* bedrooms: Number of bedrooms
* bathrooms: Number of bathrooms
* sqft_living: Square footage of the home
* sqft_lot: Square footage of the lot
* floors :Total floors (levels) in house
* waterfront :House which has a view to a waterfront
* view: Has been viewed
* condition :How good the condition is overall
* grade: overall grade given to the housing unit, based on King County grading system
* sqft_above : Square footage of house apart from basement
* sqft_basement: Square footage of the basement
* yr_built : Built Year
* yr_renovated : Year when house was renovated
* zipcode: Zip code
* lat: Latitude coordinate
* long: Longitude coordinate
* sqft_living15 : Living room area in 2015(implies-- some renovations) This might or might not have affected the lotsize area
* sqft_lot15 : LotSize area in 2015(implies-- some renovations

"price" was used as the dependent variable in our regression. The distribution of this variable had a positive skew:

![price hist](https://github.com/sabinabains/dsc-phase-2-project/blob/main/images/price_hist.png)

correlation between potential predictors were checked prior to modeling. sqft_lot15, sqfoot_living15, sqft_living, and sqft_above were dropped as they demonstrated a correlation > 0.7 with each other / other predictors.

![correlation](https://github.com/sabinabains/dsc-phase-2-project/blob/main/images/correlation.png)

A linear relationship between remaining potential predictors and price was checked, our model uses the following predictors that passed the assumption of linearity:

![bathroom](https://github.com/sabinabains/dsc-phase-2-project/blob/main/images/bathrooms_scatter.png)
![bedrooms](https://github.com/sabinabains/dsc-phase-2-project/blob/main/images/bedrooms_scatter.png)
![grade](https://github.com/sabinabains/dsc-phase-2-project/blob/main/images/grade_scatter.png)

## Model Iterations

Our first model did not pass the assumption of Homoscedasticity, and it's residuals did not follow that of a normal distribution

![qplot_1](https://github.com/sabinabains/dsc-phase-2-project/blob/main/images/qqplot_1.png)
![error_plot_1](https://github.com/sabinabains/dsc-phase-2-project/blob/main/images/error_plot_1.png)

After performing a natural log transformation on our price dependent variable, our model passed these assumptions:

![qplot_2](https://github.com/sabinabains/dsc-phase-2-project/blob/main/images/qqplot_2.png)
![error_plot_2](https://github.com/sabinabains/dsc-phase-2-project/blob/main/images/error_plot_2.png)

Zipcodes were encoded and represented in the model as binary categorical values, as the client was interested prediction price based on location. While some Zipcodes remained in the final model, we removed the following zipcodes, as they failed to reject the null hypothesis that they had an effect on price:

* zipcode 98002
* zipcode 98003
* zipcode 98030
* zipcode 98032

Our final model had an adj. R squared value of 0.802, suggesting ~80% of variance in the data can be explained by our model's features. This result has the highest F-Statistic, and an associated lowest P-value of < 0.001, meaning we reject the null hypothesis that an intercept-only model would be a better predictor. All features also have an associated P-value of < 0.05, meaning there is less than a 5% chance that these variables have no effect on house price. Lastly, since this model is built for preliminary insights only and is mainly focused on changes in price due to location, we do not have too many specific features that require input, such as exact square footage of the home / lot / basement. Below states the value of a home at it's base (with no features), as well as changes in sale price value for each additional unit of a feature, assuming all other variables are held constant. The changes are reported as a percentage
change, as the sale variable is log transformed.

* A home in zipcode 98001, with a value of 0 for all other features, would have a sale price of $43,398
* A one unit increase in bedrooms would increase the house price by 5.5%
* A one unit increase in bathrooms would increase the house price by 9.3%
* A one unit increase in grade would increase the house price by 21.8%
* Purchasing a home in zipcode_98004 would increase the house price by 216.3%
* Purchasing a home in zipcode_98005 would increase the house price by 113.6%
* Purchasing a home in zipcode_98006 would increase the house price by 98.2%
* Purchasing a home in zipcode_98007 would increase the house price by 86.1%
* Purchasing a home in zipcode_98008 would increase the house price by 96.8%
* Purchasing a home in zipcode_98010 would increase the house price by 40.2%
* Purchasing a home in zipcode_98011 would increase the house price by 56.3%
* Purchasing a home in zipcode_98014 would increase the house price by 51.6%
* Purchasing a home in zipcode_98019 would increase the house price by 43.5%
* Purchasing a home in zipcode_98022 would increase the house price by 17.1%
* Purchasing a home in zipcode_98023 would decrease the house price by 5.3%
* Purchasing a home in zipcode_98024 would increase the house price by 73.7%
* Purchasing a home in zipcode_98027 would increase the house price by 68.5%
* Purchasing a home in zipcode_98028 would increase the house price by 52.2%
* Purchasing a home in zipcode_98029 would increase the house price by 69.2%
* Purchasing a home in zipcode_98031 would increase the house price by 6.0%
* Purchasing a home in zipcode_98033 would increase the house price by 120.5%
* Purchasing a home in zipcode_98034 would increase the house price by 68.3%
* Purchasing a home in zipcode_98038 would increase the house price by 20.0%
* Purchasing a home in zipcode_98039 would increase the house price by 289.0%
* Purchasing a home in zipcode_98040 would increase the house price by 160.9%
* Purchasing a home in zipcode_98042 would increase the house price by 7.6%
* Purchasing a home in zipcode_98045 would increase the house price by 43.0%
* Purchasing a home in zipcode_98052 would increase the house price by 85.7%
* Purchasing a home in zipcode_98053 would increase the house price by 91.7%
* Purchasing a home in zipcode_98055 would increase the house price by 13.8%
* Purchasing a home in zipcode_98056 would increase the house price by 41.6%
* Purchasing a home in zipcode_98058 would increase the house price by 17.1%
* Purchasing a home in zipcode_98059 would increase the house price by 45.0%
* Purchasing a home in zipcode_98065 would increase the house price by 60.6%
* Purchasing a home in zipcode_98070 would increase the house price by 77.3%
* Purchasing a home in zipcode_98072 would increase the house price by 67.9%
* Purchasing a home in zipcode_98074 would increase the house price by 74.5%
* Purchasing a home in zipcode_98075 would increase the house price by 86.2%
* Purchasing a home in zipcode_98077 would increase the house price by 69.5%
* Purchasing a home in zipcode_98092 would increase the house price by 4.2%
* Purchasing a home in zipcode_98102 would increase the house price by 128.5%
* Purchasing a home in zipcode_98103 would increase the house price by 106.2%
* Purchasing a home in zipcode_98105 would increase the house price by 148.2%
* Purchasing a home in zipcode_98106 would increase the house price by 26.6%
* Purchasing a home in zipcode_98107 would increase the house price by 103.4%
* Purchasing a home in zipcode_98108 would increase the house price by 34.5%
* Purchasing a home in zipcode_98109 would increase the house price by 151.2%
* Purchasing a home in zipcode_98112 would increase the house price by 169.8%
* Purchasing a home in zipcode_98115 would increase the house price by 116.1%
* Purchasing a home in zipcode_98116 would increase the house price by 104.0%
* Purchasing a home in zipcode_98117 would increase the house price by 110.4%
* Purchasing a home in zipcode_98118 would increase the house price by 53.7%
* Purchasing a home in zipcode_98119 would increase the house price by 143.7%
* Purchasing a home in zipcode_98122 would increase the house price by 98.4%
* Purchasing a home in zipcode_98125 would increase the house price by 71.3%
* Purchasing a home in zipcode_98126 would increase the house price by 64.1%
* Purchasing a home in zipcode_98133 would increase the house price by 50.0%
* Purchasing a home in zipcode_98136 would increase the house price by 90.0%
* Purchasing a home in zipcode_98144 would increase the house price by 84.9%
* Purchasing a home in zipcode_98146 would increase the house price by 34.0%
* Purchasing a home in zipcode_98148 would increase the house price by 13.1%
* Purchasing a home in zipcode_98155 would increase the house price by 52.5%
* Purchasing a home in zipcode_98166 would increase the house price by 47.8%
* Purchasing a home in zipcode_98168 would increase the house price by 7.8%
* Purchasing a home in zipcode_98177 would increase the house price by 89.3%
* Purchasing a home in zipcode_98178 would increase the house price by 19.0%
* Purchasing a home in zipcode_98188 would increase the house price by 9.0%
* Purchasing a home in zipcode_98198 would increase the house price by 10.8%
* Purchasing a home in zipcode_98199 would increase the house price by 125.5%
* A one unit increase in has_basement_1.0 would increase the house price by 5.7%
* A one unit increase in renovated_1.0 would increase the house price by 13.3%

## Estimated Total Budget

The cost details for each of the families are listed below after inputting their family size, parole location, and general preferences (estimating a 30% down payment):

The predicted cost of a home for Family 1 would be $ 328,112, requiring a down payment of at least $ 98,433
The predicted cost of a home for Family 2 would be $ 378,468, requiring a down payment of at least $ 113,541
The predicted cost of a home for Family 3 would be $ 345,946, requiring a down payment of at least $ 103,784
The predicted cost of a home for Family 4  would be $ 653,298, requiring a down payment of at least $ 195,989
The predicted cost of a home for Family 5 would be $ 146,478, requiring a down payment of at least $ 43,944

**Total Budget Required: At least $ 555,691**


## Repository Structure

```
├── data
├── images
├── other_code (previous iterations of code)
├── README.md
├── Phase 2 Project - Sabina Bains - 1.19.22 .pptx (Presentation in PDF form)
├── Phase 2 Project - Sabina Bains - 1.19.22 .pdf  (Presentation for Stakeholders)
├── README.md (description of repo)
├── KCHA_budget_analysis.pdf (PDF version of jupyter notebook for modeling)
└── KCHA_budget_analysis.ipynb (jupyter notebook used for modeling)
```
