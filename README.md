# Welcome to an exploration of King County real-estate!

![hello](https://github.com/tiaplagata/dsc-phase-2-project-online/blob/master/images/King%20County%20Real%20Estate.png?raw=true)

# Navigation

* [Project Overview](#Project-Overview)
* [Question 1](#Question-1)
* [Question 2](#Question-2)
* [Question 3](#Question-3)
* [EDA Conclusion](#EDA-Conclusion)
* [Linear Regression Model](#Linear-Regression-Model)
* [Future Work](#Future-Work)

# Important Links

* [Slideshow Presentation](https://github.com/tiaplagata/dsc-phase-2-project-online/blob/master/King%20County%20Real%20Estate.pdf)
* [Non-Technical Video Presentation](https://youtu.be/vTKpMueOnNg)
* [Jupyter Notebook with Cleaning](https://github.com/tiaplagata/dsc-phase-2-project-online/blob/master/notebooks/Cleaning_Workbook.ipynb)
* [Jupyter Notebook with Exploratory Data Analysis (EDA)](https://github.com/tiaplagata/dsc-phase-2-project-online/blob/master/notebooks/EDA_Questions_Notebook.ipynb)
* [Jupyter Notebook with Linear Regression Modeling and Validation](https://github.com/tiaplagata/dsc-phase-2-project-online/blob/master/notebooks/Linear_Regression_Workbook.ipynb)

# Project Overview

King County Real-Estate is trying to compete with the bigger real-estate companies by creating a feature on their app that will predict home prices. They have hired a junior data scientist to learn more about their county's home prices and the features that affect home prices. Next, they would like for me to build a linear regression model to accurately predict the price of homes in their county. They believe this app would be useful to King County homeowners who are looking to sell their home in the near or distant future in order to get an idea of their home's value before deciding to list it with a realtor. 

In the process, I explored the following questions: 
* Q1: What is the effect of zipcode on home price?
* Q2: What is the impact of home and lot square footage on home price? What is the average price per square foot for different zipcodes?
* Q3: What is the effect of population density on home price?

**Key Stakeholders**

* Real-estate company app product manager
* Real-estate company board of directors
* Marketing department who may want to integrate the feature into their email campaigns or other promotions
* App users, such as homeowners currently looking to sell and homeowners interested in selling their home in the near/distant future
 
**Scope & Data Used**

This project used the kc_housing_data dataset, which can be found in the data folder. In order to effectively use explore and build a model from this data, I removed the following outliers:
- homes under $100,000 
- homes over $1,000,000
The cleaned dataset contained over 20,000 homes sold in 2014 or 2015 in King County. It included the home price and a plethora of features describing the home (living square footage, bedrooms, bathrooms, condiiton, waterfront, etc).

# Question 1

## What is the effect of zipcode on home price? Which zipcode has the highest home prices? 
### Further exploration: is highest-priced zipcode mostly waterfront property?

**Findings**

The top 3 zipcodes with the highest mean home prices are: 98039, 98040 and 98006. Of the top 15, only 2 of the zipcodes contain waterfront homes: 98006 and 98074. Looking solely at waterfront homes, the mean home prices are all over $500K. 

In contrast, the zipcodes with the lowest mean home prices are 98002, 98168 and 98032. Of the bottom 15, none of the zipcodes contain waterfront homes. 

We can conclude that waterfront homes are generally more expensive homes, but not all of the highest-priced neighborhoods contain waterfront homes. This brings up the question of which features are causing the home prices in the high-priced zipcodes to be so high.


# Question 2

## What is the impact of home and lot square footage on home price? What is the price per square foot for different zipcodes?

**Findings**

When we look at the correlation coefficients, the living square footage has a bigger impact on the price than the lot square footage (0.6 and 0.09 respectively).

Breaking this down into price per square footage for both the living space and lot space, we can rank the zipcodes by most expensive and least expensive per square foot.

For price per lot square footage:
* Most expensive zipcodes: 
    * 98102, 98119, 98112, 98109 and 98107
    * Mean prices between  241− 320 USD per lot square foot

* Least expensive zipcodes: 
    * 98070, 98014, 98024, 98010 and 98077
    * Mean prices between  14− 24 USD per lot square foot 
    
Interestingly, 98070 is also a zipcode with waterfront homes. It is possible that part of this area is in a flood zone, or has a lot of run-down homes selling for renovation to explain its low land prices.

For price per living square footage: 
* Most expensive zipcodes:
    * 98039, 98004 , 98109 , 98119 and 98112
    * Mean prices between  400− 620 per living square foot
* Least expensive zipcodes:
    * 98023, 98002, 98001, 98032 and 98030
    * Mean prices between  145− 155 per living square foot 
    
The most expensive zipcodes in terms of living square footage price are similar to our findings from the first question. Surprisingly, none of them are waterfront and many of them are also the most expensive in terms of land price.

It would be interesting to dig deeper and see what makes these zipcodes so much more expensive. Based on these findings, we can conclude that the home on the lot has a big impact on its price, but the land is also expensive, so it could be the population density of these areas driving up the price of homes and land. We will explore this further in the next question.


# Question 3

## What is the effect of population density on home price?

**Findings**

In conclusion, there is a relationship between population density and price per living sqft. There is a positive correlation of about 0.5, meaning it is not a very strong correlation, but it is still a positive one. As the population density increases, so does the price per sq ft.

When looking at the different zipcodes, we can easily see a cluster of zipcodes where there is a high population density, and also high prices per sq ft. These zipcodes are chronologically from 98102 to 98122, so we can expect that these zipcodes represent Seattle proper, and not the suburbs (98122 is actually the official city center zipcode). Of these zipcodes, 98109, 98102 and 98119 are the most expensive per sq ft, but also some of the most densely populated. The only exception is 98039, in which homes are the most expensive per sq ft, but not as densely populated as the city-center zipcodes.

Therefore, it is generally more expensive to live in the city-center, where the population is more dense.


# EDA Conclusion

In conclusion, the home price is greatly affected by the location of the home and the living square footage. Although lot square footage also has an impact on price, living square footage is a better indicator of price.

Waterfront homes are generally more expensive than non-waterfront homes, but they are not the factor influencing the most expensive zipcodes. In fact, population density is a better indication of home price than whether or not a home is waterfront. The more dense the population, the higher the price of the home, which is likely caused by sheer supply and demand. The most densely populated zipcodes are an indication of the Seattle city center as opposed to suburbs. However, there are a few suburban zipcodes that are just as expensive, if not more expensive than the city-center zipcodes. 

These findings can be very useful when creating our model and considering the which features to use. 


# Linear Regression Model

This linear regression model is able to predict the housing price in King County with roughly 70% accuracy. The average difference between actual price and predicted price is 116,728-117,571 USD (train and test rsme respectively).
    
**Features Used to predict home price:**
- Living square footage
- Lot square footage
- Latitude coordinate of home location
- Age of home
- Difference in lot size between home lot size and that of 15 closest neighbors
- Number of bedrooms and bathrooms
- Waterfront property (Y/N)
- Rating of view from home (0-4)
- Grade given to home by King County
- Zipcode
- If/when home was renovated

In conclusion, this model functions fairly well, but could benefit from more tinkering to increase the r2 score (see more in future work).


# Future Work

If I had time to explore further, I would investigate the following:

* Dig deeper into the qualities of the homes in these areas, such as home condition and grade to see what other characteristics besides the home's location and sq footage affect the price.
* Look at some of the characteristics of the most expensive zipcodes that are not densely populated (ex. 98039) to see what makes them so expensive.
* Look at renovated homes vs non renovated homes built in the same year to see how much value a renovation adds.

