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

