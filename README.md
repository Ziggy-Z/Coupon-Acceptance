
# Will a Customer Accept the Coupon?

### Overview

The goal of this project is to use what I know about visualizations and probability distributions to distinguish between customers who accepted a driving coupon for a restaurant less than $20 versus those who did not.
#### Question statement: Do income, marital status, and having children affect the acceptance rate of coupons for less expensive restaurants (< $20)?

#### Driver attributes used for this analysis
* Marital Status: single, married partner, unmarried partner, or widowed
* Number of children: 0, 1, or more than 1.
* Annual income: less than $12500, $12500 - $24999, $25000 - $37499, etc.
* Number of times that he/she eats at a restaurant with an average expense of less than $20 per person: 0, less than 1, 1 to 3, 4 to 8 or greater than 8.
#### For this analysis, I'll be using Python to explore the given dataset. Libraries used are Pandas, seaborn, matplotlib, and numpy.







### Data Setup
To prepare our data, we had to do some data cleaning.
* Columns like age, bar, coffeeHouse, carryAway, RestaurantLessThan20,Restaurant20To50, and salary should be int64 values but our data has them as objects. These fields were converted to int64 for better analysis.
* For values like salary that are range-based, the mean can be used to replace the string format.
* Filter our data for *Restaurant(<20)* coupons from column *'coupon'*.
* Remove null values that we don't need so our data is not skewed.

### Analysis
 Let's analyze the relationship between Marital Status and income level
 
![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/boxplot.png)
* From this boxplot, we observe that Married partners have an average higher income than other marital statuses. Using this, we can further explore how many of each marital group have accepted coupons for restaurants with an average expense of less than $20.
* let us look at the acceptance rate (Column 'Y' = 1) of each marital status.
    - We can find the acceptance rate by taking the mean of the 'Y' column: `data['Y'].mean()`. This is     possible due to the 'Y' column being a boolean. Therefore, the mean of a boolean logic (values with 0s and 1s) will always give us the ratio of 1s to the total number of values.
When we plot the acceptance rate, this is what we see:

![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/maritalAcceptance.png)
* We can see that Single individuals have the highest acceptance rate compared to other marital statuses. Therefore, we can conclude that Single individuals are more likely to accept coupon for a restaurants with average expense less than $20.

* Our next analysis is how will the result we got from the previous plot change if we add income and one of the other factors.
* To analyze this, we will group our data using `groupby(['maritalStatus', 'income'])`.
* Let's first analyze how our data will look if we sum up all individuals who accepted the coupon and plot them in their income and marital status category.
This is the plot we get:

![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/totalAcc.png)
* We can see that when income is lower than $56,249, More single individuals accept the coupon. But with income above that value, we see that more married partners accept the coupons.

Now let's see if this same trend applies to the acceptance rate of each marital status based on their income:

![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/incomeVacc.png)

* We don't see the same pattern. When we take into account the acceptance rate within each group, we see that Divorced marital status on average have a higher acceptance rate when income is below $56,249 and we see unmarried partners having a slightly higher acceptance rate in income group above `$56,249`.

* We can hypothesize that the observation from this plot is due to other marital statuses having a higher mean acceptance rate.

Let's add another dimension to our plot. Would having children affect the acceptance rate between each marital status?


![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/maritalAccBych.png)

* We can see that on average, people with children have a higher acceptance rate compared to individuals with no kids.
We can further observe this correlation by plotting all 4 columns on a heatmap:

![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/heatmap.png)

* Overall, we can conclude that income and marital status have an effect on coupon acceptance with having children also positively affecting the acceptance rate. The next step would be to possibly include age, and occupation to get more robust data. However, we have analyzed a positive correlation to build a model.


### Data Setup
To prep our data, we had to do some data cleaning.
* Columns like age, bar, coffeeHouse, carryAway, RestaurantLessThan20,Restaurant20To50, and salary should be int64 values but our data has them as objects. These fields were converted to int64 for better analysis.
* For values like salary that are range based, the mean can be used to replace the string format.
* Filter our data for *Restaurant(<20)* coupons from column *'coupon'*.
* Remove null values that we don't need so our data is not skewed.

### Analysis
 Let's analyze the relationship between Marital Status and income level
 
![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/boxplot.png)
* From this boxplot, we observe that Married partners have an average higher income than other marital status. Using this, we can further explore how many of each marital groups have accepted coupons for restaurants with average expense less than $20.
* Lets look at the acceptance rate (Column 'Y' = 1) of each marital status.
    - We can find the acceptance rate by taking the mean of 'Y' column: `data['Y'].mean()`. This is     possible due to 'Y' column being a boolean. Therefore, the mean of a boolean logic (values with 0s and 1s) will always give us the ratio of 1s to the total number of values.
### Acceptance rate by marital status:

![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/maritalAcceptance.png)
* We can see that Single individuals have the highest acceptance rate compared to other marital statuses. Therefore, we can conclude that Single individuals are more likely to accept coupon for a restaurants with average expense less than $20.

* Our next analysis is how will our result we got from the previous plot change if we add income and one of the other factor.
* To analize this, we will group our data using `groupby(['maritalStatus', 'income'])`.
* Lets first analyze how our data will look like if we sum up all individuals that accepted the coupon and plot them in their income and marital status catagory.
### Total acceptance by income:

![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/totalAcc.png)
* We can see that when income is lower than $56,249, More single individuals accept the coupon. But income above that value, we see that more married partners accept the coupons.

### Acceptance rate by income:

![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/incomeVacc.png)

* We don't see the same pattern. When we take account the acceptance rate within each group, we actually see that Divorced marital status on average have a higher acceptance rate when income is below $56,249 and we see unmarried partners having slightly higher acceptance rate on income group above $56,249.

* We can hypothesize that the observation from the this plot is due to other marital statuses having higher mean acceptance rate.

Would having childern affect the acceptance rate between each marital statuses?

### Acceptance rate by marital satus and childern:
![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/maritalAccBych.png)

* We can see that on average, people with childern have a higher acceptance rate compared to individuals with no kids.
We can further observe this correlation by plotting all 4 columns on a heatmap:
### marital status with/without childern and income:
![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/heatmap.png)
* We see that over the average income range, single parents have a higher chance of accepting this coupon.

### Gender and weather by income:
![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/Genheatmap.png)
* There is a strong correlation between weather and acceptance rate and we also see that there's a slight increase in acceptance rate of males compared to females.
### Weather vs age:
![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/Weatheatmap.png)
* We can see weather and age have an effect on acceptance rate. Weather and acceptance rate have positive correlation whereas age and acceptance rate have a negative correlation.

### Conclusion:
 - Income and marital status have an effect on coupon acceptance with having children also positively having an effect on acceptance rate. 
 - Marital status combined with childern has a slight effect on acceptance rate.
 - Gender and weather can affect acceptance rate: Males having a slightly higher acceptance rate overall across all weather.
 - Weather has a strong positive correlation to acceptance rate by each age group. Age and acceptance rate have a negative correlation. As age increases, acceptance rate decreases.

### Next step:
 - Add other factors that contribute to the acceptance rate of cheaper restaurants (<$20) like direction to restaurant and distance to make our analysis robust.
 - Finalize our analysis to start building our training model.
