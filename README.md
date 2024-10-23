# ANOVA Analysis of Marketing Campaigns

## **Project Overview**

In this project, I will perform hypothesis testing using historical marketing promotion data. The analysis will utilize analysis of variance (ANOVA) techniques to determine if there are significant differences in sales across various marketing promotion methods. The objective is to answer key business questions regarding the effectiveness of TV and influencer promotions on sales, providing valuable insights for stakeholders to inform their marketing strategies.

The project will involve conducting a one-way ANOVA test, along with post hoc analysis, to ascertain whether any notable differences exist among the means of the different promotional methods. Through this analysis, I aim to communicate clear findings to non-technical stakeholders, enabling data-driven decision-making.

## **Table of Contents**

- [Introduction](#Introduction)
- [Step 1: Imports](#Step-1:-Imports)
- [Step 2: Data Exploration](#Step-2:-Data-Exploration)
- [Step 3: Model Building](#Step-3:-Model-Building)
- [Step 4: Results and Evaluation](#Step-4:-Results-and-Evaluation)
- [Conclusion](#Conclusion)
- [How to Run](#how-to-run)
- [References](#References)

## **Introduction**

Analysis of variance (commonly called ANOVA) is a group of statistical techniques that test the difference of means among three or more groups. It's a powerful tool for determining whether population means are different across groups and for answering a wide range of business questions.

In this project, I will be working with historical marketing promotion data. I will use the data to run a one-way ANOVA and a post hoc ANOVA test. Then, I will communicate the results to stakeholders.

In the dataset, each row corresponds to an independent marketing promotion, where the business uses TV, social media, radio, and influencer promotions to increase sales. Stakeholders want to know if sales are significantly different among various TV and influencer promotion types.

To address this request, a one-way ANOVA test will enable us to determine if there is a statistically significant difference in sales among groups. This includes:
* Using plots and descriptive statistics to select a categorical independent variable
* Creating and fitting a linear regression model with the selected categorical independent variable
* Checking model assumptions
* Performing and interpreting a one-way ANOVA test
* Comparing pairs of groups using an ANOVA post hoc test
* Interpreting model outputs and communicating the results to nontechnical stakeholders

## Step 1: Imports

### Import packages
- Import the necessary libraries for data manipulation, visualization, and modeling.

### Load the dataset
- Load the marketing dataset that contains information on promotional spending and corresponding sales.


## **Step 2: Data Exploration**
**Some reasons for conducting an EDA before constructing a simple linear regression model:** 
* To understand which variables are present in the data
* To consider the distribution of features, such as minimum, mean, and maximum values
* To plot the relationship between the independent and dependent variables and visualize which features have a linear relationship
* To identify issues with the data, such as incorrect or missing values.

**Using a boxplot to determine how `Sales` vary based on the `TV` promotion budget category.**

- There is considerable variation in `Sales` across the `TV` groups. The significance of these differences can be tested with a one-way ANOVA.

**Using a boxplot to determine how `Sales` vary based on the `Influencer` size category.**


- There is some variation in `Sales` across the `Influencer` groups, but it may not be significant.

### Checking and Removing Missing Data if Exists

## **Step 3: Model Building**

Fitting a linear regression model that predicts `Sales` using one of the independent categorical variables in `data`.

**Question:** Which categorical variable did you choose for the model? Why?
* `TV` was selected as the preceding analysis showed a strong relationship between the `TV` promotion budget and the average `Sales`.
* `Influencer` was not selected because it did not show a strong relationship to `Sales` in the analysis.

### Checking Model Assumptions

**Linearity** 

- Because the model doesn't have any continuous variables, the linearity assumption isn't required. 

**Independent Observation**

- The independent observation assumption states that each observation in the dataset is independent. As each marketing promotion (row) is independent from one another, the independence assumption is not violated.

**Normality Assumption**

Verifying that the normality assumption is upheld for the model.

- There is reasonable concern that the normality assumption is not met when `TV` is used as the independent variable predicting `Sales`. The normal Q-Q plot forms an 'S' that deviates off the red diagonal line, which is not desired behavior. 

**Log Transformation**

We use log transformation in this case to stabilize variance and reduce the influence of potential outliers, helping to normalize the residuals and improve the linearity of the relationship between independent variables and the dependent variable `Sales`. This transformation allows for better model fitting and interpretation while addressing the non-normality observed in the residuals.

**Model Building After the Transformation**

Building the model again after transforming the dependent variable `Sales` because of the violation of the normality assumption.

Verifying that the normality assumption is upheld for the model after the transformation.

- The residuals almost form a 'bell shape,' indicating they are normally distributed.

**Constant Variance (Homoscedasticity) Assumption** 

Verifying the constant variance (homoscedasticity) assumption is met for this model.

- The variance where there are fitted values is similarly distributed, validating that the constant variance assumption is met.

## **Step 4: Results and Evaluation**


**The Interpretation of the Model's R-squared**

79.6% of the variation in Sales is explained by the variation in TV promotion.

**The Interpretation of the Coefficient Estimates**

The coefficient for the "Low" TV category (-1.2555) indicates that sales are approximately 71.51% lower compared to the "High" category, while the "Medium" category (-0.4211) has sales about 34.4% lower than "High." Both coefficients are statistically significant with p-values < 0.0001, meaning the differences in sales between the categories are not due to random chance. Thus, the TV categories have a significant impact on sales in the model.

Note: The percentage is calculated by this formula because the dependent variable was log transformed: (e^-0.4211−1)×100

### Perform a One-Way ANOVA Test

With the model fitted, I will run a one-way ANOVA test to determine whether there is a statistically significant difference in `Sales` among groups. 

**The Null and Alternative Hypotheses for the ANOVA Test**

$H_0$: The mean of the 3 categories is equal, and any difference is due to chance and not statistically significant.

$H_A$: At least one of the 3 categories is different from the others.

### ANOVA Results

- The F-test statistic is 1105.98 and the p-value is $2.97 * 10^-196 (i.e., very small). Because the p-value is less than 0.05, I would reject the null hypothesis that there is no difference in `Sales` based on the `TV` promotion budget.

**Post Hoc Analysis**

- The all categories rejecting the null hypothesis which is the mean of sales among the 3 categories is equal, so we can conclude that there is a statistically significat difference in the mean of sales among the 3 categories.
- A post hoc test was conducted to determine which `TV` groups are different and how many are different from each other. This provides more detail than the one-way ANOVA results, which can at most determine that at least one group is different. Further, using the Tukey HSD controls for the increasing probability of incorrectly rejecting a null hypothesis from peforming multiple tests. 

- The results were that `Sales` is not the same between any pair of `TV` groups. 

## **Conclusion**

The results of this project indicate that there are significant differences in sales across various marketing promotions, particularly with TV promotions having a noteworthy impact on sales. The analysis and findings support the notion that businesses should strategically invest in TV marketing, as it leads to greater sales compared to other promotional methods.

**Key Insights**

- Sales Variation: 79.6% of the variation in Sales is explained by differences in TV promotion categories.

- Impact of TV Categories: Sales are approximately 71.51% lower for the "Low" TV category and 34.4% lower for the "Medium" category compared to "High." These differences are statistically significant (p < 0.0001).

- Statistical Significance: The results of both the one-way ANOVA and Tukey’s HSD tests confirm significant differences in Sales between TV promotion categories.

**Summary for Stakeholder**

The analysis shows that 79.6% of the variation in Sales can be attributed to differences in TV promotion categories. Sales in the "Low" TV category are approximately 71.51% lower, and sales in the "Medium" category are about 34.4% lower compared to the "High" category. The model is a reliable predictor of Sales with an R-squared value of 0.796. Statistical tests, including one-way ANOVA and Tukey’s HSD, confirm significant differences between all TV promotion categories, meaning TV promotion has a substantial impact on sales.

## How to Run

1. **Clone the repository**:

    ```bash
    git clone <https://github.com/MahmoudKhaled98/ANOVA-Analysis-of-Marketing-Campaigns.git>
    ```

2. **Install the required dependencies**:

    ```bash
    pip install -r requirements.txt
    ```

3. **Run the Jupyter notebook**:

    ```bash
    jupyter notebook
    ```
## References

- Saragih, H.S. (2020). [*Marketing and Sales Data*](https://www.kaggle.com/datasets/harrimansaragih/dummy-advertising-and-sales-data).

- [Pandas Documentation](https://pandas.pydata.org/)
- [Seaborn Documentation](https://seaborn.pydata.org/)
- [Matplotlib Documentation](https://matplotlib.org/stable/contents.html)
- [Statsmodels Documentation](https://www.statsmodels.org/stable/index.html)
