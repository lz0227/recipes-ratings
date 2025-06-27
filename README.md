# Recipes & Ratings Analysis 🍽️

A comprehensive data analysis project exploring the relationship between sugar content and recipe ratings, plus a machine learning model to predict recipe calories.

## 📊 Project Overview

This project analyzes recipe data from [food.com](https://www.food.com/) to answer two key questions:

1. **"More Sugar == More Happiness?"** - Investigating the relationship between sugar content and recipe ratings
2. **"Guess the Calories"** - Building a machine learning model to predict recipe calories

## 🏗️ Project Structure

```
recipes-ratings/
├── index.html              # Main page: "More Sugar == More Happiness?"
├── guess-calories.html     # Machine learning page: "Guess the Calories"
├── assets/                 # Interactive visualizations and charts
│   ├── dist_sugar_amount.html
│   ├── avg_rating_vs_sugar_pdv_new.html
│   ├── published_year_vs_rating_missing.html
│   ├── fairness_test.html
│   └── ... (other visualization files)
└── README.md              # This file
```

## 🚀 How to Use

### Viewing the Website
1. Open `index.html` in any modern web browser
2. Navigate between the two main pages using the navigation bar
3. All visualizations are interactive and embedded directly in the pages

### No Setup Required
- **No server needed** - Pure HTML/CSS/JavaScript
- **No dependencies** - Works offline
- **Cross-platform** - Works on any device with a web browser

## 📈 Analysis 1: More Sugar == More Happiness?

### Research Question
> What is the relationship between the amount of sugar and the happiness of people?

### Dataset
- **Source**: Food.com recipes and ratings (2008+)
- **Size**: 83,782 recipes
- **Key Features**: Sugar content (PDV), average ratings (1-5 scale), recipe metadata

### Key Findings
- **Hypothesis Test**: p-value = 0.13 (failed to reject null hypothesis)
- **Conclusion**: No significant relationship found between sugar content and recipe happiness
- **Missingness Analysis**: Rating missingness depends on published year but not number of ingredients

### Visualizations Included
- Sugar distribution box plot
- Average rating vs. sugar content scatter plot
- Missingness analysis charts
- Hypothesis testing empirical distributions

## 🤖 Analysis 2: Guess the Calories

### Machine Learning Task
> Predict recipe calories using other nutritional and recipe features

### Model Performance

#### Baseline Model
- **Features**: Published year, total fat (PDV)
- **Training R²**: 0.795
- **Testing R²**: 0.675

#### Final Model
- **Features**: Published year, total fat (PDV), sugar (PDV), healthiness, number of ingredients
- **Algorithm**: Decision Tree Regressor (max_depth=8)
- **Training R²**: 0.907
- **Testing R²**: 0.849

### Fairness Analysis
- **Groups**: Old recipes (pre-2012) vs. New recipes (post-2012)
- **Test**: Permutation test on R² differences
- **Result**: p-value = 0.26 (model appears fair across time periods)

## 🎨 Design Features

### Modern UI/UX
- **Responsive Design**: Works on desktop, tablet, and mobile
- **Gradient Backgrounds**: Beautiful visual appeal
- **Card-based Layout**: Clean, organized information presentation
- **Interactive Navigation**: Smooth transitions between pages

### Color Scheme
- **Primary**: Teal (#4ecdc4) and Coral (#ff6b6b)
- **Background**: Purple gradient (#667eea to #764ba2)
- **Accents**: Gold highlights for important information

## 📊 Data Processing

### Cleaning Steps
1. **Merged datasets**: Recipes + ratings to get average ratings per recipe
2. **Handled missing values**: Replaced 0 ratings with null (users didn't rate)
3. **Expanded nutrition data**: Split nutrition column into individual features
4. **Created derived features**:
   - `healthy`: Boolean based on protein/carbohydrate ratios
   - `happiness`: Categorical (happy/sad) based on rating thresholds
   - `published_year`: Extracted from submission dates
5. **Outlier handling**: Removed recipes with cooking times > 24 hours

### Key Features Used
- **Nutritional**: Calories, sugar (PDV), total fat (PDV), protein (PDV), carbohydrates (PDV)
- **Recipe**: Number of ingredients, cooking time, published year
- **Derived**: Healthiness, happiness classification

## 🔬 Statistical Methods

### Hypothesis Testing
- **Permutation tests** for missingness dependency
- **Kolmogorov-Smirnov tests** for distribution comparisons
- **Total Variation Distance** for categorical data

### Machine Learning
- **Decision Tree Regressor** for calorie prediction
- **Grid Search CV** for hyperparameter tuning
- **One-Hot Encoding** for categorical features
- **Train/Test Split** for model validation

## 👥 Authors

**Luran Zhang, Yunpeng Zhao**

## 📝 Technical Notes

### Browser Compatibility
- Modern browsers (Chrome, Firefox, Safari, Edge)
- JavaScript enabled for interactive visualizations
- No special plugins required

### File Formats
- **HTML**: Main content pages
- **CSS**: Embedded styles for consistent design
- **JavaScript**: Interactive charts (embedded via iframes)

### Data Sources
- Original data from Food.com scraping
- Processed and cleaned for analysis
- Visualizations created with Plotly

## 🎯 Key Insights

1. **Sugar vs. Happiness**: No significant correlation found between sugar content and recipe ratings
2. **Calorie Prediction**: Machine learning model achieves 84.9% accuracy on test data
3. **Model Fairness**: No evidence of bias between old and new recipes
4. **Data Quality**: Missingness patterns reveal interesting temporal trends

## 📚 Future Work

Potential extensions of this analysis:
- Explore other nutritional factors affecting ratings
- Build recommendation systems based on user preferences
- Analyze seasonal trends in recipe popularity
- Develop more sophisticated calorie prediction models

---

*This project demonstrates comprehensive data analysis skills including data cleaning, exploratory analysis, hypothesis testing, machine learning, and fairness evaluation.* 