# Budget Analysis for King County Healing Association
![kcha_logo](https://github.com/sabinabains/dsc-phase-2-project/blob/main/kcha%20logo.png)

King County Healing Association is an established nonprofit organization that has a variety of successful initiatives such as rehabilitation centers, medical assistance, career services, and temporary housing for those re-entering their communities. The organization now wants to expand on their housing opportunities by rolling out a new service to help those who are prepared to transition into a permanent residence.  

Unfortunately, those with criminal records tend to be discriminated against even after serving their sentence, and often banks do not lend money to these individuals. Additionally, those previously incarcerated could have bad credit or a lack of savings. Because of all this, KCHA plans to borrow from banks themselves and provide the down payment for applicants of this program. The new tenants can then pay off their mortgage to KCHA monthly, while additionally paying back the down payment over time. 

Along with requirements to ensure the applicants have a stable income and can pay off their debt, KCHA requires tenants to choose homes within the same zipcode of their parole officer (if applicable).

KCHA doesn't plan to launch this service for another 3 years, and therefore are in the preliminary stages. The organization estimates they will assist 5 families in their first year of the program, and would like our help estimating the total down payment cost based on these family's parole office location, household size, and general preferences.

Details of the 5 Family's being considered for the first year of this program:
* Family 1 would like a 3 bedroom, 2 bathroom house in zipcode 98011. They prefer a basement and a home quality of at least 6/10
* Family 3 would like a 2 bedroom, 1 bathroom house in zipcode 98032. They would prefer a home quality of at least 6/10
* Family 3 would like a 1 bedroom, 1 bathroom house in zipcode 98045. They would prefer a home quality of at least 8/10
* Family 4 would like a 4 bedroom, 3 bathroom house in zipcode 98065. They prefer a basement and a home quality of at least 6/10
* Family 5 would like a 1 bedroom, 2 bathroom house in zipcode 98001. They would prefer a home quality of at least 5/10

## Methodology

This dataset ([linked here](https://www.kaggle.com/harlfoxem/housesalesprediction)) contains house sale prices for King County, Washington. The dataset has a sample of 21,597 homes sold between May 2014 and May 2015, and has the following columns:

* id
* date
* price
* bedrooms
* bathrooms
* sqft_living
* sqft_lot
* floors
* waterfront
* view
* condition
* grade
* sqft_above
* sqft_basement
* yr_built
* yr_renovated
* zipcode
* lat
* long
* sqft_living15
* sqft_lot15

"price" was used as the dependent variable in our regression. The distribution of this variable had a positive skew:
![price hist](https://github.com/sabinabains/dsc-phase-2-project/blob/main/images/price%hist.png)

## Repository Structure

```
├── data
├── images
├── previous code
├── README.md
├── Presentation.pdf
└── analysis.ipynb
```
