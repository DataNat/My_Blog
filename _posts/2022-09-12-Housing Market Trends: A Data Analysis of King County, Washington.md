---
layout: post
title:  "Housing Market Trends: A Data Analysis of King County, Washington"
tags: [ Real Estate ]
featured_image_thumbnail:
featured_image: /assets/images/posts/2018/12.jpg
---
### Introduction

Since an abrupt but brief recession during the earliest days of the Covid pandemic, the United States housing market has rebounded with increased sales. Those whose jobs went remote were now able to transition from renting near the workplace to buying a larger space further afield. With houses in high demand, increased building costs, and other supply-side constraints, house prices have soared nationwide for the past two years. However, the steep overall inflation of 2022 has rerouted the housing market once again, and economists predict that the months-long decline in house prices will only worsen throughout the year.

**Purpose**

The purpose of this project is to advise a real estate investment firm in King County, Washington. The following Data and Analysis will help the firm predict the market value of a given house, while the conclusions offer recommendations for future investments.

**Method**

I coded the analysis using Python and Scikit-learn. The data came from the King County House Sales dataset (2014–2015) provided by Flatiron, as well as from online sources listed in the Bibliography.

### Data and Analysis

**Correlation**

I calculated the correlation among home prices and various house features. I removed redundant data (e.g., separate measures of square footage for attic and basement, since they are part of the living space). I also removed zip codes since the number does not follow a meaningful order. Our analysis determined that the following four features are most impactful to house price: square footage, grade, number of bathrooms, and view. Using these terms, I then explored investment ççopportunities in certain locations. I will add the zipcodes when I strat modeling the data.

Figure A.

<img src="/My_Blog/assets/images/posts/2018/1_f_1.png" alt="Figure A">


Rumors surrounded an Apple-developed wearable back as far as 2011, which conceptualized the device as a variation of the iPod that would curve around the user’s wrist, and feature Siri integration. On February 10, 2013, both The New York Times and The Wall Street Journal reported that Apple was beginning to develop an iOS-based smartwatch with a curved display. On February 12, 2013, Bloomberg reported that Apple’s smartwatch project was “beyond the experimentation phase in its development”, and had a team of at least 100 designers were working on the project. Further reports in March 2013 indicated that Apple planned to release the device by the end of the year. In July 2013, Financial Times reported that Apple had begun hiring more employees to work on the smartwatch, and that it was targeting a possible retail release in late 2014.

**Size: Square Footage and Number of Bathrooms**

Square footage is directly related to the price of a house, but only up to a certain point. Houses larger than 6,000 sq ft do not show a commensurate increase in price. Nonetheless, the few houses larger than 7,500 sqft range between $3 to $7 million. Lot size does not necessarily affect house price.

Figure B. Figure C.

<img src="/My_Blog/assets/images/posts/2018/sqft_sqft_living.png" alt="Figure B and C">

Figure D.
<img src="/My_Blog/assets/images/posts/2018/bathrooms.png" alt="Figure D">


As seen in Figure D, certain homes are not affected by the increase of bathrooms while other home prices go up as the number of bathrooms increases.




**Location**

House location is assessed based on zip code. Figure E shows which zip codes of low to mid-range prices range from $350K to a little over $1 Million. The average house in this zip code is 2,000–5,700 square feet, has an average or excellent view, and has 3–6 bathrooms.


Figure E

<img src="/My_Blog/assets/images/posts/2018/map.png" alt="Figure E">



**View and Waterfront**

Having a view, which is characterized by natural features such as water, mountains, and greenery, showed to have a significant impact on housing value. Only 7% of houses have what is considered a “good” or “excellent” view, and these range from $800K to $2 million in value. By comparison, 83% of houses do not have a view, and these range from $350K-$500K in value.

In particular, waterfront homes are significantly more valuable than those without. Homes without a waterfront typically range from $300K-$600K, while waterfront homes typically cost more than three times that amount, from $900K-$2.6M.

Figure F

<img src="/My_Blog/assets/images/posts/2018/view.png" alt="Figure E">

Figure G

<img src="/My_Blog/assets/images/posts/2018/waterfront.png" alt="Figure G">

**Grade**

Grade refers to the quality of the materials and appliances used throughout the structure. Grade is directly related to house prices. Houses with a grade rated higher than 10 range from roughly $1.5 to $4 million.

Figure H

<img src="/My_Blog/assets/images/posts/2018/grade.png" alt="Figure H">

**Seasonality**

In our data, I encountered 45 houses that were resold in 2014 and 2015. The majority of these were resold for a higher price. The grade or condition of the houses did not change, but the resale took place in a different time of the year. The resale price was highest during the month of May, followed by January and March. In the summer, there were no resales, and those that did take place (August) lost money. This suggests that the timing of the sale makes a difference. Given the small sample of houses, the next step would be to gather further data of houses that resold and solidify whether the seasonality trends hold.


Figure I.

<img src="/My_Blog/assets/images/posts/2018/month.png" alt="Figure I">

### Predicting Prices Using Linear Regression

I predicted prices using linear regression. I used a stepwise selection function on the independent variables to determine which features to use for the linear regression model. The model showed R Squared as 79% in house prices, as explained by 82 housing features. See Figure J for full OLS Regression Results.




The test of our model was successful. See below.

Figure J.


<img src="/My_Blog/assets/images/posts/2018/ols.png" alt="Figure J">


Training Root Mean Squared Error: $203K

Training R squared: 0.64

## Conclusions

I have determined that the most valuable assets of a house in King County are zip code, view, grade and condition, square footage, and seasonality. Below are investment recommendations for Edegon and Company:

LOCATION: Consider investing in zip codes 98125, 98115, 98144, 98178, 98199, 98116,98136 whose market value is currently low to mid-range but also include some of the most profitable housing features.

VIEW: Prioritize a house with a great view, particularly if it has a waterfront.

GRADE: Grade is more important than house age. Investing in high quality materials will lead to a profitable outcome.

SIZE: Prioritize the size of the indoor, living area rather than the size of the lot. Houses ranging from 2,500 sqft to 5,000 sqft have a high correlation to house prices.

**Next Steps**

Gather more data from previous years
Focus on profitable transactions (buy/ sell) with the new data.
Create a racking system for the 16 housing features already mentioned above in order to see which are the most influential on house prices.

The complete code can be found on my [GitHub repository](https://github.com/DataNat/Data-Analysis-Real-Estate-in-King-County-Washington).


**Bibliography**

U.S. Federal Housing Finance Agency, All-Transactions House Price Index for King County, WA [ATNHPIUS53033A], retrieved from FRED, FeSderal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/ATNHPIUS53033A, August 3, 2022.

King County Department of Assessments, 2014 Annual Update. https://kingcounty.gov/depts/assessor/Reports/area-reports/2014/residential-northwest/~/media/depts/assessor/documents/AreaReports/2014/Residential/ImpPic/033ImpPics.pdf

“Parcel Record Assessor extract table” http://www5.kingcounty.gov/sdc/FGDCDocs/PARCEL_EXTR_faq.htm

S&P Dow Jones Indices LLC, S&P/Case-Shiller U.S. National Home Price Index [CSUSHPISA], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/CSUSHPISA, August 16, 2022.

