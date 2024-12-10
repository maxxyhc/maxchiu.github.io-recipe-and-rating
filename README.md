# CookSmart!Insights into Recipe Complexity and Ratings
by Max Chiu

## 📊 Introduction to the Dataset  

Cooking is both an art and a science, requiring the perfect balance of flavors, preparation methods, and timing. Recipes vary widely in their complexity, from simple dishes with minimal ingredients to intricate meals requiring multiple steps and hours of effort. This dataset provides an extensive collection of recipes, designed for home cooks seeking to explore a variety of cuisines and improve their culinary skills. 

## ❓ Research Question  

**What factors influence the average rating of a recipe?**  

By analyzing key recipe characteristics such as preparation time, the number of steps, and ingredients, we aim to uncover insights into what makes a recipe well-received by users.

## 🌟 Why It Matters  

By analyzing key recipe characteristics such as preparation time, the number of steps, and ingredients, we aim to uncover insights into what makes a recipe well-received by users. This analysis is valuable for home cooks, food bloggers, and culinary businesses seeking to create better, more appealing recipes. Cooking different dishes comes with varying levels of difficulty and complexity; through predictive modeling, we hope to recommend the simplest yet most delicious recipes. Users can also discover recipes tailored to their preferences for a more enjoyable cooking experience.

## 📂 Relevant Columns and Descriptions  

- **`TOTAL ROWS`**: **234,429 rows**
- **`minutes`**: The total preparation and cooking time for the recipe (in minutes).  
- **`n_steps`**: The number of steps required to complete the recipe.  
- **`n_ingredients`**: The number of unique ingredients used in the recipe.  
- **`average_rating`**: The average rating given to the recipe by users (on a scale from 0 to 5).  
- **`ingredients`**: A list of ingredients required to prepare the recipe.  

By analyzing these features, we hope to identify the most significant factors contributing to higher recipe ratings and user satisfaction. 🍽️📊

# 🧹 Data Cleaning and Exploratory Data Analysis  
Cleaning and preparing the dataset was an essential part of ensuring accurate analysis and meaningful insights. The following steps were taken during the data cleaning process:

1. **Merged the DataFrames**  
   We started by merging the two datasets (`RAW_interactions` and `RAW_recipes`) to combine recipe details with user interactions. This allowed us to work with a unified dataset containing both recipe characteristics and user feedback.

2. **Replaced Zero Ratings with NaN Values**  
   All instances where the `rating` column contained a value of 0 were replaced with `np.nan`.  
   - **Why this step was necessary**: A rating of 0 likely represents missing or invalid data rather than a true rating. By treating these values as missing data (`NaN`), we ensured they wouldn’t artificially skew our analyses, particularly when calculating averages.

3. **Added Average Rating Per Recipe**  
   Using the cleaned `rating` column, the average rating for each recipe was calculated and added back to the recipes dataset as a new column, `average_rating`. This step provided a key metric for analyzing recipe performance.

4. **Removed the Bottom 5% of Recipes**  
   The last 5% of the dataset (sorted by `average_rating`) was removed to eliminate recipes that may have had disproportionately low or unrepresentative ratings.  
   - **Why this step was necessary**: These low-performing recipes might introduce noise or outliers into the analysis, making it harder to discern meaningful patterns.

5. **Removed Rows Where `average_rating` Is Zero**  
   Finally, rows where the `average_rating` column still contained a value of 0 were removed. These rows likely indicated recipes with no valid ratings, making them irrelevant for further analysis.  

| name                            |     id |   minutes |   contributor_id | submitted   |
|:--------------------------------|-------:|----------:|-----------------:|:------------|
| secret ingredient  bbq meatloaf | 342620 |        75 |            50969 | 2008-12-09  |
| sexy greek   cocktail           | 423875 |         5 |            65502 | 2010-05-07  |
| sexy greek   cocktail           | 423875 |         5 |            65502 | 2010-05-07  |
| sexy greek   cocktail           | 423875 |         5 |            65502 | 2010-05-07  |
| sexy greek   cocktail           | 423875 |         5 |            65502 | 2010-05-07  |

# 📊 Visualization of Cooking Time Distribution  

<iframe
  src="assets/Distribution-of-Cooking-Time-(minutes)-Outliers-Removed.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The data shows that most recipes require **less than 50 minutes** to prepare, with the frequency significantly declining as cooking time increases. This trend suggests that users prefer recipes with shorter preparation times, likely due to their convenience for everyday cooking.

## Key Observations  
- Recipes with a cooking time under 50 minutes are the most frequent in the dataset.
- Longer cooking times (>100 minutes) occur less frequently, even after removing outliers, suggesting that such recipes may inherently be less common or less appealing for everyday use.

# 📊 Visualization of Calories vs. Average Recipe Ratings Distribution 

<iframe
  src="assets/Calories-vs.-Average-Recipe-Ratings.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The scatter plot demonstrates the relationship between calories and average recipe ratings. Most points cluster in the top-left corner, suggesting that recipes with lower calorie counts tend to receive higher ratings.

Additionally, many recipes have average ratings that are whole numbers. This is likely because these recipes received only a few ratings. Since individual ratings are typically whole numbers, the averages of one or a few rating of the same value will be whole values (e.g., 3, 4, or 5). 

# 📊 Grouped Data: Average Ratings by Cooking Time and Year  

## Pivot Table: Average Recipe Ratings by Cooking Time  

| minutes_bin   |    2008 |    2009 |    2010 |    2011 |    2012 |    2013 |    2014 |    2015 |    2016 |    2017 |    2018 |
|:--------------|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|
| 0-30          | 4.45186 | 4.46313 | 4.48639 | 4.49254 | 4.44288 | 4.4481  | 4.21212 | 3.98246 | 3.82222 | 3.125   | 3.44681 |
| 30-60         | 4.39622 | 4.39526 | 4.36219 | 4.42664 | 4.40462 | 4.33494 | 4.35174 | 4.28889 | 3.76531 | 2.87097 | 3.44068 |
| 60-90         | 4.3321  | 4.32736 | 4.29915 | 4.34734 | 4.31989 | 4.3145  | 4.13008 | 4.40789 | 3.54348 | 2.97938 | 3.14516 |
| 90-120        | 4.32129 | 4.31367 | 4.39192 | 4.26556 | 4.30977 | 4.06042 | 4.38776 | 3.5     | 2.5     | 1.82143 | 3.31579 |
| 120-150       | 4.24064 | 4.34937 | 4.42727 | 4.38506 | 4.28146 | 4.14719 | 4.52525 | 4.7     | 5       | 3.16    | 2.08333 |

### Significance  

This pivot table highlights how cooking times are grouped into ranges (bins), with average recipe ratings calculated for each time range across different years. It helps identify trends in user preferences, showing whether recipes with certain cooking durations consistently receive higher ratings or if preferences shift over time.


# Assessment of Missingness

I believe the description column in the dataset is likely Not Missing At Random (NMAR). The missingness in this column may depend on factors that are not present in the dataset itself. For example, a description might be missing because the person submitting the recipe chose not to provide one, which could be due to personal preferences, time constraints, or simply oversight. These factors are not captured in the dataset, making the missingness NMAR.

To make this missingness Missing At Random (MAR), additional data would be required, such as information about the user submitting the recipe (e.g., their engagement level, experience, or frequency of recipe submissions). With such data, we could analyze whether the missing descriptions are associated with specific user behaviors or other observable factors, thereby turning the missingness into MAR.


# 🔍 Permutation Tests  

## Results of Missingness Permutation Tests  

We conducted permutation tests to examine whether the missingness of the `description` column is associated with differences in the distributions of two variables: **cooking time (`minutes`)** and **number of ingredients (`n_ingredients`)**. The results are summarized below:  

### 1. Test for `minutes`  
- **Observed Mean Difference**: The observed difference in mean cooking times between recipes with missing descriptions and those with descriptions is highlighted in the plot below (red line).  
- **P-Value**: Approximately **0.319**, which is greater than the typical significance threshold (e.g., 0.05).  
- **Interpretation**: There is no statistically significant evidence to suggest that the missingness of `description` is associated with a difference in cooking times.  

### 2. Test for `n_ingredients`  
- **Observed Mean Difference**: The observed difference in the average number of ingredients between recipes with missing descriptions and those with descriptions is highlighted in the plot below (red line).  
- **P-Value**: Approximately **0.017**, which is less than the typical significance threshold (e.g., 0.05).  
- **Interpretation**: There is a statistically significant difference in the average number of ingredients based on whether the description is missing. Recipes with missing descriptions may tend to have fewer or more ingredients than those with descriptions.  

## Implications  

The results of the permutation tests reveal that:  
1. **Missing descriptions are not associated with cooking times (`minutes`)**.  
2. **Missing descriptions are significantly associated with the number of ingredients (`n_ingredients`)**.  

This suggests that the missingness of `description` could be **conditionally missing at random (MAR)** with respect to the number of ingredients. Future analyses should consider this relationship when handling missing values in the dataset.

## Visualizations  

### Permutation Test: Difference in Mean `Minutes` by Missing Description  

<iframe
  src="assets/Permutation-Test/-Difference-in-Mean-'Minutes'-by-Missing-Description.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Permutation Test: Difference in Mean `n_ingredients` by Missing Description  

<iframe
  src="assets/Permutation-Test/-Difference-in-Mean-'n_ingredients'-by-Missing-Description.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/Distribution-of-Minutes-when-Description-is-Missing.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/Distribution-of-Minutes-when-Description-is-not-Missing.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>