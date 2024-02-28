
# Understanding Coupon Acceptance

# Overview

The goal of this project is to use what I know about visualizations and probability distributions to distinguish between customers who accepted a coupon for a restaurant less than $20 versus those who did not.

The complete analysis can be found here: [Jupyter Notebook](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/notebook/prompt.ipynb)
## Question statement:
* How does income, marital status, having children, age, gender, and weather impact the acceptance rate of coupons for restaurants with a value of less than $20?

# Data collection:
We begin by filtering the dataset to isolate coupons designated for restaurants with a value of less than $20, as indicated in the 'coupon' column. This initial filtering yields 2786 data entries, exhibiting an acceptance rate of 70.5%. Within this dataset, individuals boast an average income of $52,676. Notably, the acceptance rate remains consistent at 70% for both those with incomes below and above the average.

# Driver attributes used for this analysis:
* Marital Status: single, married partner, unmarried partner, or widowed
* Number of children: 0, 1, or more than 1.
* Annual income: less than $12500, $12500 - $24999, $25000 - $37499, etc.
* Number of times that he/she eats at a restaurant with an average expense of less than $20 per person: 0, less than 1, 1 to 3, 4 to 8 or greater than 8.
#### We'll be using Python to explore the given dataset. Libraries used are Pandas, seaborn, matplotlib, and Numpy.
# Data Setup:
To prepare our data, we had to do some data cleaning.
* Columns like age, bar, coffeeHouse, carryAway, RestaurantLessThan20,Restaurant20To50, and salary should be int64 values but our data has them as objects. These fields were converted to int64 for better analysis.
* For values like salary that are range-based, the mean can be used to replace the string format.
* Remove null values that we don't need so our data is not skewed.

# Analysis
 Let's analyze the relationship between Marital Status and income level:
 
![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/boxplot.png)
* From this boxplot, we observe that Married partners have an average higher income than other marital statuses. Using this, we can further explore how many of each marital group have accepted coupons for restaurants with an average expense of less than $20.
* Let's look at the acceptance rate (Column 'Y' = 1) of each marital status.
    - We can find the acceptance rate by taking the mean of the 'Y' column: `data['Y'].mean()`. This is     possible due to the 'Y' column being a boolean. Therefore, the mean of a boolean logic (values with 0s and 1s) will always give us the ratio of 1s to the total number of values.
### Acceptance rate by Marital status:

![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/maritalAcceptance.png)
* We can see that Single individuals have the highest acceptance rate compared to other marital statuses. Therefore, we can conclude that Single individuals are more likely to accept coupons for restaurants with an average expense of less than $20.

* Our next analysis is how will the result we got from the previous plot change if we add income and one of the other factors.
* To analyze this, we will group our data using `groupby(['maritalStatus', 'income'])`.
* Let's first analyze how our data will look if we sum up all individuals who accepted the coupon and plot them in their income and marital status category.
### Total acceptance by income:

![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/totalAcc.png)
* among individuals with incomes below $56,249, a higher proportion of single individuals tend to accept the coupon. Conversely, for those with incomes exceeding this threshold, there is a notable increase in the acceptance rate among married partners.

### Acceptance rate by Income:

![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/incomeVacc.png)

* However, we don't see the same pattern when analyzing the acceptance rat. When we take into account the acceptance rate within each group, we see that Divorced marital status on average have a higher acceptance rate when income is below $56,249 and we see unmarried partners having a slightly higher acceptance rate in income group above $56,249.

* We can hypothesize that the observation from this plot is due to other marital statuses having a higher mean acceptance rate, evening out the spike we saw with single individuals.

Would having children affect the acceptance rate between each marital status?

### Acceptance rate by Marital status and Children:
![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/maritalAccBych.png)

* We can see that on average, people with children have a higher acceptance rate compared to individuals with no kids.
We can further observe this correlation by plotting all 4 columns on a heatmap:
### marital status with/without children and income:
![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/heatmap.png)
* We see that over the average income range, single parents have a higher chance of accepting this coupon.

### Gender and Weather by Income:
![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/Genheatmap.png)
* There is a strong correlation between weather and acceptance rate and we also see that there's a slight increase in acceptance rate of males compared to females.
### Weather vs Age:
![Logo](https://github.com/Ziggy-Z/Coupon-Acceptance/blob/main/images/Weatheatmap.png)
* We can see whether weather and age affect the acceptance rate. Weather and acceptance rate have a positive correlation whereas age and acceptance rate have a negative correlation.

### Conclusion:
 - Income and marital status have an effect on coupon acceptance with having children also positively affecting the acceptance rate. 
 - Marital status combined with children has a slight effect on the acceptance rate.
 - Gender and weather can affect acceptance rate: Males have a slightly higher acceptance rate overall across all weather.
 - Weather has a strong positive correlation to the acceptance rate by each age group. Age and acceptance rate have a negative correlation. As age increases, the acceptance rate decreases.

### Next step:
 - Add other factors that contribute to the acceptance rate of cheaper restaurants (<$20) like direction to the restaurant and distance to make our analysis robust.
 - Finalize our analysis to start building our training model.
