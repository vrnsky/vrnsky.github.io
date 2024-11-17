---
title: Data preparation techniques
type: docs
sidebar:
open: true
next: data-preparation-practice
prev: data-collection-and-preparation
---

There are several ways to handle missing data:
- Deletion: sometimes we remove records with missing values, but we have to be careful not to lose too much valuable information. This works best when only a small percentage of data is missing
- Imputation: This means filling in missing values using different methods:
  - Mean/Mode/Median imputation: replacing missing values with the average (for numerical data) or most common value (for categorical data)
  - Prediction model: using other variables to predict what the missing values might be
  - Using a new category: for categorical data, sometimes we create a new category call "Unknown" or "Missing"
- Handling outliers: outliers are extreme values that could distort our analysis. We can handle them through:
  - Deletion: if we are confident they are errors of if they are very few
  - Transformation: using techniques like:
    - Log transformation to reduce impact of extreme values
    - Binning (grouping values into ranges)
    - Capping values at certain thresholds (also called Winsorization)
- Data transformation techniques:
  - Data generalization
    - Aggregation: combining detailed data into summary form (like daily sales into monthly totals)
    - Binning: converting continuous data into categories (like age into age groups)
- Data normalization
  - Range transformation (min - max scaling): bring all values into a specific range, usually 0 to 1
  - Z-score transformation: standardizing data to have mean 0 and standard deviation 1
  - Log transformation: useful for handling skewed data
  - Square root and square transformation: help in dealing with certain types of distributions
- Attribute selection and creation:
  - Selection of important attributes
    - Removing redundant or irrelevant attributes
    - Identifying which variables are most important for our analysis
    - Using statistical method to select most relevant feature
  - Creating a new attributes
    - Combining existing attributes to create meaningful new ones
    - Converting raw data into more useful forms (like creating age from birth data)
    - Creating dummy variables for categorical data