---
title: Data collection and preparation
type: docs
sidebar:
open: true
next: data-preparation-techniques
prev: what-is-data-mining
---

Data collection and preparation is like building a strong foundation for a house - 
if you don't get this part right, everything built on top of it could be problematic.
Let's dive into what is really means:

### Data understanding
Before we even start collecting data, we need to understand what we are looking at.
This involves exploring the data's basic characteristics. For example, if we have customer data, we need 
to know what kinds of information we have - it is their purchase history? Demographic information? Website browsing 
behavior?

### Types of data we might encounter
1. Categorical data - like gender, product categories, or customer status
2. Numerical data - things we can measure, like age, income, or purchase amounts
3. Time-series data - information collected over time, like daily sales figures
4. Text data - like customer reviews or comments
5. Multimedia data - such as images, videos, or audio files

### Data quality issues
Here is where thing get interesting. Real - world data is rarely perfect, and we often encounter several common problems:
1. Missing values: sometimes data just not there. For instance, some customers might not provide their age or income. We can handle this by
   1. Filling in missing values with averages
   2. Using predictive models to estimate missing values
   3. Sometimes removing records with too many missing values
4. Outliers: These are unusual values that don't seem to fit with the rest of the data. For example, if most customers spend between 10-100 dollars, but one transaction shows $10 000, that is an outlier. We need to:
   1. Investigate if these are errors or genuine unusual cases
   2. Decide whether to keep, modify, or remove them
   3. Consider how they might affect our analysis
4. Inconsistent data: This happens when the same information is recorded differently in different places. For instances, "New York", "NY", and "New York City" might all refer to the same place

### Data transformation
Once we have identified and cleaned up these issues, we often need to transform the data to make it more useful for analysis:
- Normalization: Getting numerical values onto the same scale
- Aggregation: Combining multiple data points into summary statistics
- Feature creation: Creating new, meaningful data point from existing ones
- Encoding: Converting categorical data into numerical format that computers can process

### The really important path
The key thing to remember is that data preparation is not just a technical exercise. Every decision we make during this phase
affect our final results. For instance, how we handle missing value could significantly impact our predictions. If we 
are not careful with outliers, our models might be skewed.