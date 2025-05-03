# Sarker_What-Really-Drives-Wine-Ratings
Does a statistically significant relationship exist between measurable chemical properties (independent variables) and expert-rated wine quality (dependent variable)?



# Investigating the Relationship Between Physicochemical Properties and Red Wine Quality

## #### Introduction

This report investigates whether measurable chemical properties of red wine can predict expert-assigned quality ratings. Understanding these relationships has significant implications for wine producers, who can potentially optimize production processes to enhance quality, and for consumers seeking to understand the technical aspects behind wine appreciation.

Red wine quality is traditionally assessed through sensory evaluation by wine experts, resulting in somewhat subjective quality scores. However, if strong relationships exist between objective chemical measurements and these quality assessments, producers could potentially use laboratory analysis to predict consumer reception and guide production decisions.

## #### Data Description

The analysis uses the Wine Quality dataset from the UCI Machine Learning Repository, containing 1,599 red wine samples with physicochemical measurements and corresponding quality ratings . Each wine sample includes measurements of 11 chemical properties and an expert-rated quality score on a scale from 0 to 10.

The key variables in the dataset include:

- **Fixed acidity**: Non-volatile acids (primarily tartaric acid) that don't evaporate readily
- **Volatile acidity**: Primarily acetic acid content, which can lead to unpleasant vinegar taste at high levels
- **Citric acid**: Adds freshness and flavor to wines
- **Residual sugar**: Amount of sugar remaining after fermentation
- **Chlorides**: Salt content in the wine
- **Sulfur dioxide**: Both free and total forms (preservative)
- **Density**: Depends on alcohol and sugar content
- **pH**: Acidity level (typically between 3-4)
- **Sulphates**: Additives that contribute to sulfur dioxide levels
- **Alcohol**: Percent alcohol content
- **Quality**: Output variable based on sensory data (score between 0-10)

## #### Exploratory Data Analysis

### Univariate Analysis

Initial exploration revealed several interesting patterns in the data:

- **Quality Distribution**: Most wines in the dataset received ratings of 5-6, with none achieving ratings of 9-10, suggesting a relatively normal distribution centered on average quality .

- **Chemical Properties**: Several chemical properties show significant variation:
  - Acidity measures (fixed acidity, volatile acidity, citric acid, pH) show different distributions, with fixed and volatile acidity displaying positively skewed distributions
  - Alcohol content ranges between 8% and 15%, also with a positively skewed distribution
  - Residual sugar shows extreme positive skew, with most wines having low concentrations

### Correlation Analysis

A correlation matrix revealed several significant relationships:

- **Alcohol content** shows a moderate positive correlation with wine quality (r ≈ 0.48), suggesting that higher alcohol content is associated with better quality ratings .

- **Volatile acidity** displays a moderate negative correlation with quality (r ≈ -0.39), indicating that higher levels of acetic acid tend to reduce quality ratings .

- **Sulphates** show a positive correlation with quality (r ≈ 0.25), suggesting that this additive contributes positively to expert perception .

- **Density** shows a negative correlation with quality (r ≈ -0.30), which may be related to its relationship with alcohol content .

## #### Methodology

To address the research question, I applied two distinct modeling approaches:

### Linear Regression Model

First, I built a linear regression model to establish baseline relationships between chemical properties and quality. The model equation took the form:

```
Quality = β₀ + β₁(fixed_acidity) + β₂(volatile_acidity) + ... + βₙ(alcohol) + ε
```

The linear model provides easily interpretable coefficients that directly quantify the relationship between each chemical property and wine quality, controlling for other variables.

### Random Forest Model

To capture potentially non-linear relationships, I also implemented a Random Forest regression model, which combines multiple decision trees trained on different subsets of the data. This ensemble approach offers several advantages:

- Ability to capture complex, non-linear relationships
- Built-in feature importance measurement
- Less susceptible to overfitting than single decision trees

For both models, performance was evaluated using:
- Root Mean Square Error (RMSE)
- Coefficient of determination (R²)
- Cross-validation to ensure robust performance estimates

## #### Results

### Linear Regression Findings

The linear regression model achieved an R² of approximately 0.40, indicating that about 40% of the variation in wine quality can be explained by the measured chemical properties. The most significant predictors were:

1. **Alcohol content** (positive coefficient): Each percentage point increase in alcohol was associated with approximately a 0.25-point increase in quality rating, holding other variables constant.

2. **Volatile acidity** (negative coefficient): Each g/L increase in volatile acidity was associated with approximately a 1.0-point decrease in quality rating.

3. **Sulphates** (positive coefficient): Higher sulphate concentrations were associated with higher quality ratings.

4. **Total sulfur dioxide** (negative coefficient): Higher levels of this preservative were associated with lower quality ratings.

### Random Forest Model Results

The Random Forest model outperformed the linear regression, achieving an R² of approximately 0.53, indicating that it captured additional non-linear relationships in the data.

Feature importance analysis from the Random Forest model revealed:

1. **Alcohol content** (21.4% importance): Confirmed as the most important predictor of wine quality.

2. **Volatile acidity** (15.3% importance): Second most important feature, with higher levels associated with lower quality.

3. **Sulphates** (12.7% importance): Third most important feature, positively associated with quality.

4. **Total sulfur dioxide** (9.5% importance): Showed non-linear effects on quality that weren't fully captured by the linear model.

5. **Density** (8.8% importance): Showed complex relationships with quality, likely related to its connection with alcohol and sugar content.

These findings largely align with expert wine knowledge, where alcohol content contributes to body and mouthfeel, while volatile acidity (vinegar notes) is generally considered a fault at high levels.

## #### Discussion

### Key Insights

The analysis confirms that physicochemical properties of red wine significantly predict quality ratings assigned by wine experts. Both models demonstrated predictive power well above random chance, though the Random Forest model's superior performance suggests non-linear relationships exist between some chemical properties and wine quality.

**Alcohol Content**: The strong positive relationship between alcohol and quality may reflect several factors. Higher alcohol content is typically associated with riper grapes, which can contribute to more intense flavors and fuller body. However, this relationship may also reflect particular styles of wine that were favored by the experts who rated these samples.

**Volatile Acidity**: The negative impact of volatile acidity aligns with established wine knowledge. At high concentrations, volatile acids produce vinegar-like aromas and flavors that are generally considered faults in wines, except in specific styles like some Italian red wines where slightly higher levels may be traditional.

**Sulphates**: These compounds act as preservatives and antioxidants in wine. Their positive association with quality likely reflects their role in preventing oxidation and preserving fresh fruit characteristics in the wines.


## #### Conclusion

The analysis confirms that physicochemical properties of red wine significantly predict expert quality ratings, with alcohol content, volatile acidity, and sulphates emerging as particularly important predictors. The Random Forest model demonstrated superior predictive performance, suggesting complex, non-linear relationships between some chemical properties and perceived quality.

These findings support the thesis that objective chemical measurements can provide valuable insights into subjective quality assessments. However, the models explained only about 36-52% of the variation in quality ratings, indicating that other unmeasured factors also play substantial roles in determining wine quality.

For future research, incorporating sensory descriptors alongside chemical measurements could provide a more comprehensive understanding of wine quality. Additionally, analyzing wines across different regions, varieties, and price points could reveal how these relationships vary across different market segments and wine styles.
