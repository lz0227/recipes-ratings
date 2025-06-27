# More Sugar  == More Happiness ? 🧐

<svg xmlns="http://www.w3.org/2000/svg" viewbox="0 0 750 180" width="500" height="200" style="opacity: 0.5; filter: grayscale(0.5);"><text x="0em" y="1em" font-size="75" transform="rotate(0 46.875 45)">🍦</text><text x="1.25em" y="2em" font-size="75" transform="rotate(0 140.625 120)">🍨</text><text x="2.5em" y="1em" font-size="75" transform="rotate(0 234.375 45)">🍰</text><text x="3.75em" y="2em" font-size="75" transform="rotate(0 328.125 120)">🍜</text><text x="5em" y="1em" font-size="75" transform="rotate(0 421.875 45)">🍕</text><text x="6.25em" y="2em" font-size="75" transform="rotate(0 515.625 120)">🍔</text><text x="7.5em" y="1em" font-size="75" transform="rotate(0 609.375 45)">🌮</text><text x="8.75em" y="2em" font-size="75" transform="rotate(0 703.125 120)">🥘</text></svg>

## Introduction

​		Our original datasets came from two csv files, “recipes” and “ratings”, scraped from [food.com](https://www.food.com/). They include information about recipes posted on the website after 2008. In order to get the average rating per recipe, we merged these two datasets and used groupby method. We also replace any rating of 0 to be null value because the lowest rating someone can give is 1. Having a rating of 0 means the user did not leave a star rating, but maybe other forms of interaction like a comment or review. Then, we assigned the average rating column we created back to the recipes dataset. Hence, the dataset we worked with in our project is the original recipes dataset with an additional column average rating generated from the ratings datasets. 

Using this dataset, we hope to answer the following question:

> **What is the relationship between the amount of sugar and the happiness of people?**

By answering this question, we will be able to learn more about people’s feelings towards sweet food and figure out whether they will bring happiness to people. This will help people to determine if sweet food is what they should eat more often to keep them feeling happy. 

There is a total of 83782 rows in our dataset and some relevant columns to our question are “nutrition” which includes multiple nutritious values including the percentage of the daily value of sugar, and “avg_rating” which is the average rating for the recipe on a scale from 1 to 5. 



------



## Cleaning & Exploratory Data Analysis

### **Data Cleaning**

​	In order to clean our data, we first expanded the nutritions column so that each value is in its own column thus making it easier for us to access the value we want, which is the amount of sugar in that recipe. We also changed the type of each of these nutritious values to float so we can use them to generate meaningful insights like taking the mean of them. 

​	Then we added a boolean column named "healthy" that tells us whether each recipe is healthy or not based on a standard we developed using the amount of protein and carbohydrate in that recipe. For the sake of this project, we consider a healthy recipe to be ones that have more protein and less carbohydrates. To quantify this, we use the average value of proteins and carbohydrates as the threshold to determine if values in a recipe are considered low or high.

​	We also want to determine whether people are happy with each recipe. Here we assume that a high rating means that reviewers are happy from eating the dish they cooked based on this recipe. Opposite of this means that reviewers are sad from eating the dish they cooked based on this recipe. Thus, we created a new column named happiness to determine if people are happy or sad to a recipe on average. 

​	Next, we converted the "submitted", a column that contains the date a recipe was submitted to the website, into pandas timestamp type, which allows us to extract the year out of the date and created a column named "published_year".

​	We also dealt with the outliers in the "minutes" column, which contains the time in minutes it takes to cook the recipe. We consider a recipe with a cooking time over 1 day to be unreasonable because they are outliers that do not give valuable information to our analysis, thus we will consider them as missing for the purpose of our project. We also consider a time of 0 minutes to be missing value since it is unlikely to have 0 minutes as the time needed for cooking a dish. 



<table border="1" class="dataframe">   <thead>     <tr style="text-align: right;">       <th></th>       <th>name</th>       <th>id</th>       <th>minutes</th>       <th>contributor_id</th>       <th>submitted</th>       <th>n_steps</th>       <th>n_ingredients</th>       <th>avg_rating</th>       <th>calories (#)</th>       <th>total fat (PDV)</th>       <th>sugar (PDV)</th>       <th>sodium (PDV)</th>       <th>protein (PDV)</th>       <th>saturated fat (PDV)</th>       <th>carbohydrates (PDV)</th>       <th>healthy</th>       <th>happiness</th>       <th>published_year</th>     </tr>   </thead>   <tbody>     <tr>       <th>0</th>       <td>1 brownies in the world    best ever</td>       <td>333281</td>       <td>40.0</td>       <td>985201</td>       <td>2008-10-27</td>       <td>10</td>       <td>9</td>       <td>4.0</td>       <td>138.4</td>       <td>10.0</td>       <td>50.0</td>       <td>3.0</td>       <td>3.0</td>       <td>19.0</td>       <td>6.0</td>       <td>False</td>       <td>happy</td>       <td>2008</td>     </tr>     <tr>       <th>1</th>       <td>1 in canada chocolate chip cookies</td>       <td>453467</td>       <td>45.0</td>       <td>1848091</td>       <td>2011-04-11</td>       <td>12</td>       <td>11</td>       <td>5.0</td>       <td>595.1</td>       <td>46.0</td>       <td>211.0</td>       <td>22.0</td>       <td>13.0</td>       <td>51.0</td>       <td>26.0</td>       <td>False</td>       <td>happy</td>       <td>2011</td>     </tr>     <tr>       <th>2</th>       <td>412 broccoli casserole</td>       <td>306168</td>       <td>40.0</td>       <td>50969</td>       <td>2008-05-30</td>       <td>6</td>       <td>9</td>       <td>5.0</td>       <td>194.8</td>       <td>20.0</td>       <td>6.0</td>       <td>32.0</td>       <td>22.0</td>       <td>36.0</td>       <td>3.0</td>       <td>False</td>       <td>happy</td>       <td>2008</td>     </tr>     <tr>       <th>3</th>       <td>millionaire pound cake</td>       <td>286009</td>       <td>120.0</td>       <td>461724</td>       <td>2008-02-12</td>       <td>7</td>       <td>7</td>       <td>5.0</td>       <td>878.3</td>       <td>63.0</td>       <td>326.0</td>       <td>13.0</td>       <td>20.0</td>       <td>123.0</td>       <td>39.0</td>       <td>False</td>       <td>happy</td>       <td>2008</td>     </tr>     <tr>       <th>4</th>       <td>2000 meatloaf</td>       <td>475785</td>       <td>90.0</td>       <td>2202916</td>       <td>2012-03-06</td>       <td>17</td>       <td>13</td>       <td>5.0</td>       <td>267.0</td>       <td>30.0</td>       <td>12.0</td>       <td>12.0</td>       <td>29.0</td>       <td>48.0</td>       <td>2.0</td>       <td>False</td>       <td>happy</td>       <td>2012</td>     </tr>   </tbody> </table>

For this dataframe, we showed the first five rows of our cleaned dataframe. Because there are too many texts in the columns called tags, steps, description and ingredients, we do not show them in this table.

### Univariate Analysis

​		We used a box plot to show the distribution of sugar (PDV). For the purpose of showing the trend, we did not show the recipe with sugar (PDV) of more than 200. In our plot, the smallest value is 0, the first quartile is 8, the median is 21, and the third quartile is 50. There is a big difference between the median and the third quartile. Though we set the upper limit as 200 to ignore some outliers, there are recipes that have a sugar value of more than 200 which is not included in our graph. This box plot suggests that most of the recipes are between 0 and 115.

<iframe src="assets/dist_sugar_amount.html" width=800 height=600 frameBorder=0></iframe>





### Bivariate Analysis

​		We used a scatter plot to show the relationship between average rating and sugar (PDV). As mentioned in Univariate Analysis, most of the recipes are between 0 sugar (PDV) and 115 sugar (PDV). For the purpose of showing the trend, we show the recipe with sugar (PDV) of more than 1000 to cover most of the recipes. Based on the scatter plot, we can see that most of the recipes were clustered between 0 - 200 (sugar (PDV)) and 3 - 5 (average rating).

<iframe src="assets/avg_rating_vs_sugar_pdv_new.html" width=800 height=600 frameBorder=0></iframe>

### Interesting Aggregates

Our pivot table shows how much sugar (PDV) sad recipes and happy recipes have on average for each year. It is significant because from our pivot table, we can see that the sad recipes tend to have more sugar than the happy recipes before 2015. From 2016 to 2018, the happy recipes had a sugar spike and exceeded the sad recipes.

|   published_year |    happy |      sad |
|-----------------:|---------:|---------:|
|             2008 |  67.5513 |  67.4426 |
|             2009 |  66.6881 |  75.3277 |
|             2010 |  63.1394 |  65.3088 |
|             2011 |  72.996  |  71.4495 |
|             2012 |  64.9092 |  94.5102 |
|             2013 |  68.216  |  99.0137 |
|             2014 |  67.9798 |  89.3721 |
|             2015 |  58.729  | 154      |
|             2016 |  94.625  |  69      |
|             2017 | 187.347  | 114.643  |
|             2018 | 239.043  | 146      |

------



## Assessment of Missingness

### NMAR Analysis

​		After examining which columns have missing values, we do believe there is a column in our dataset that is not missing at random (NMAR). The “description” column contains the description of recipes provided by the users. We can say that this column is NMAR, which means its missingness depends on its own value and does not depend on other columns. That is because if a recipe is a well-known recipe that most people already know about, then they would not really need a description column. Some might argue that we can tell what recipe it is from the name column, but the name would not tell us information about how popular a recipe is and how many people know about it. So we still conclude that the description column is NMAR.

​		If we do in fact want to obtain additional data that could explain the missingness of the description column and make it MAR, we would need to have information about the popularity of a recipe and how often it is being cooked by people. 


### Missingness Dependency

##### Missingness on average_rating & published year of recipe

  ​		Created a pivot table that shows the proportion of recipes in each year for missing ratings and not missing ratings, then plotted it to compare the distribution of published years when rating is missing and not missing.

  <iframe src="assets/published_year_vs_rating_missing.html" width=800 height=600 frameBorder=0></iframe>

  ​		Then we did a permutation test on the missingness of average rating where we used total variation distance (TVD) as our test statistics since the published year is categorical data and set the critical value to be 0.05. We did the permutation test 1000 times to generate an empirical distribution of our test statistic and present it in the following graph with the observed statistics. 

  <iframe src="assets/Empirical Distribution of the TVD.html" width=800 height=600 frameBorder=0></iframe>

  ​		After calculating the p-value, we get 0.0 which means that we would reject the null that the published year of recipes that are missing average ratings and not missing average ratings come from the same distribution. So the difference between them might not be due to random chance. Thus, the missingness of the average rating might be dependent on the published year. 

##### Missingness on average_rating & number of ingredients

  ​	We created an overlaid histogram with box plots to show the distribution of the number of ingredients when the average rating is missing and not missing. 

  <iframe src="assets/Number_of_Ingredients_by_Missingness_of_Average_Rating.html" width=800 height=600 frameBorder=0></iframe>
  ​		Since the number of ingredients is quantitative data, we used the Kolmogorov-Smirnov test statistic and did 1000 permutation tests on the missingness of the average rating. We used the same critical value as before, which is 0.05 to keep it consistent. Then we generated the empirical distribution of our test statistic and presented it in the following graph with the observed statistics.
  <iframe src="assets/Empirical Distribution of the K-S Statistic.html" width=800 height=600 frameBorder=0></iframe>
  ​		After calculating the p-value, we get 0.11 which means that we failed to reject the null that the number of ingredients of recipes that are missing average ratings and not missing average ratings comes from the same distribution. So the difference between them might be due to random chance. Thus, the missingness of the average rating might not be dependent on the published year. 


------



## Hypothesis Testing

- **Null Hypothesis**: In the population, the amount of sugar in recipes that make people happy and recipes that make people sad have the same distribution, and the observed differences in our samples are due to random chance.

- **Alternative Hypothesis**: In the population, recipes that make people sad have more sugar than recipes that make people happy, on average. The observed difference in our samples cannot be explained by random chance alone.

- **Test Statistic**: Difference in group means.

  > mean sugar amount of sad recipe−mean sugar amount of happy recipe

- **Significance Level**: We choose 0.05 as our significance level for our hypothesis testing.

- **Resulting p-value**: 0.13

- **Conclusion**: we failed to reject the null hypothesis that the two groups come from the same distribution. Therefore the difference in the observed data could be just due to random chance.



​		Recall that our question is “What is the relationship between the amount of sugar and the happiness of people?” Hence, to discover the relationship between sugar and happiness, we try to have one null hypothesis that we can test, which is that recipes that make people sad and recipes that make people happy have the same distribution of sugar amount. This means whether the recipe makes people happy or sad has no relationship with the amount of sugar. Our alternative hypothesis is that recipes that make people sad tend to have more sugar than recipes that make people happy based on our observation of the mean sugar amount in the happy and sad recipes from our observed data. Since we want to test whether both recipes have the same distribution, we need to do a permutation test and shuffle the columns to make whether people are happy or sad at random. Because the data we have are categorical (sad or happy) and numerical (sugar amount), we can use the difference between the two group means as our test statistic. 

​		After the simulation of permutation tests, we get the resulting p-value as 0.13, which is greater than 0.05. This means that we fail to reject our null hypothesis and the difference in the observed data could be just due to random chance. This means that the difference between the average sugar amount for happy recipes and sad recipes we observed based on the given data might have just been due to random chance and does not really show sad recipes will have more sugar than happy recipes.



  <iframe src="assets/Empirical Distribution of the Differences in Group Mean Sugar Amount in PDV (Sad - Happy).html" width=800 height=600 frameBorder=0></iframe>


# Guess the Calories 🤤
Our exploratory data analysis on this dataset can be found [here](https://elijahzyp.github.io/recipes_ratings/).

### Framing the Problem

​		For our project, our objective is to estimate the **calories** of each recipe through feature engineering and modeling techniques. 

> **Prediction problem**: Predict calories of recipes

​		This is a regression problem. We selected calories as a significant variable for recipes because, if accurately predicted using other parameters, it can provide users with a straightforward guide for recipe selection. To forecast the numerical value of calories, we have opted for the DecisionTreeRegressor method to get a regression. We picked this model for our project because we are predicting a continuous numerical value and DecisionTreeRegressor can capture linear and non-linear relationships and is also robust to outliers. At this time, we know 22 other features including sugar, total fat, sodium, average rating, etc. To assess the accuracy of our model, we employ the R-squared metric instead of root mean squared error (RMSE), as it effectively evaluates the model's fit and its ability to explain the observed data. That is because RMSE cannot directly show the goodness of the model in a standard scaling (e.g. 0 to 1).



------



### Baseline Model

​		Our baseline model uses two features, which are published_year and total fat (PDV), to predict the calories. Among three features, one feature (total fat (PDV)) is quantitative and one feature (published_year) is categorical and ordinal. For feature engineering, we used OneHotEncoder() to encode the published_year feature. To avoid multicollinearity, we used the drop = “First” parameter, which drops the first column from the result of the encoding. Finally, we used DecisionTreeRegressor with a max_depth of 5 to fit the model and make a prediction. The hyperparameter max_depth is set to 5 randomly and we will tune it in the later section when we build our final model.

​		We test this baseline model on both training data and testing data so we can see how our model performs on unseen data. In the end, we have an R-squared value of 0.7947850043984259 for training data and 0.6751961883585864 for testing data. Generally, We think that this is a fair model that can make an okay prediction. Since R squared value is from 0 to 1 with higher being better, our model is not the worst model we can have but there are definitely improvements that we can make to get a better model.



------



### Final Model

​		In our final model, we decided to add more features that are related to calories. We decided to add sugar to the model to help improve R squared value. That is because high sugar is usually associated with high calories. Hence, we add this quantitative feature to our model. Besides sugar, we also added healthiness (whether each recipe is healthy or not based on a standard we developed using the amount of protein and carbohydrates in that recipe) as one of our features. Healthiness is a categorical binary feature (True or False: True for healthy; False for not healthy). We think this feature is good for our prediction because high calories can often be associated with “not healthy”, so this feature will help us better predict the calories of a recipe. Another feature we added is the number of ingredients for each recipe. We think this feature will help with our prediction because the more ingredients a recipe has, the higher chance it will have a higher calorie value since there are many different ingredients. This is a discrete numerical value. 

​		For our final model, we still used the DecsionTreeRegressor for the reasons we stated in the baseline model section. However, to find the optimal value for the hyperparameter, max_depth, we use GridSearchCV (K-Fold Cross Validation) with a cv of 5 (5 folds) to figure out the best hyperparameter, which is 8 at the end. With a max_depth of 8 for the DecisionTreeRegressor in our model, we got an R-squared value of 0.907312276504803 for our training data, and 0.8486574302087885 for our testing data. Since a higher R-squared value means that a higher proportion of the variation in the recipe’s calories can be explained by the regressors, our final model with a higher R-squared value for both training and testing data has improved from our baseline model. 



------



### Fairness Analysis

​		For our fairness analysis, we will look at two different groups of recipes. One of which is recipes that were published before 2012 (old recipes), and the other is recipes published after 2012 (new recipes). The two different groups are old and new recipes. Our evaluation metric will be the R-squared values. The null hypothesis is that our model is fair; the R-squared value for the old recipes and the new recipes are the same, and any differences are due to random chance. Our alternative hypothesis is that our model is unfair; the R-squared value for old recipes is lower than the value for new recipes. We choose the difference in the R squared value for both groups (old - new) to be our test statistic and the significance level is 0.05. The resulting p-value is 0.26, which is greater than the critical value of 0.05. Thus we fail to reject the null hypothesis that our model is fair. Our conclusion is that there is not clear sign that our model is unfair for old and new recipes but it is not certain to say that our model is 100% fair. 



<iframe src="assets/fairness_test.html" width=800 height=600 frameBorder=0></iframe>

