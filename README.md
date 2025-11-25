GDG Task 1: Exploratory Data Analysis (EDA) and Encoding Impact on Linear Models
Table of Contents
Introduction
Setup and Dependencies
Data Loading and Initial Exploration
Data Cleaning and Preprocessing
Exploratory Data Visualization
Feature Engineering
Model Comparison: One-Hot Encoding vs. Label Encoding
Conclusion
How to Run the Notebook
1. Introduction
This notebook serves as the first task for the GDG committee, focusing on Exploratory Data Analysis (EDA) concepts. We start from the basics of data investigation, summarizing main characteristics using statistics and graphical representations. The task also delves into feature engineering techniques like One-Hot Encoding, Normalization, and Standardization, culminating in a comparison of linear model performance using different encoding strategies for categorical features.

The dataset used pertains to various measurements of crabs and their age.

2. Setup and Dependencies
To run this notebook, you will need the following Python libraries. Some are pre-installed in Google Colab, while ydata-profiling needs to be explicitly installed.

!pip install ydata-profiling -q
Key libraries imported:

pandas for data manipulation and analysis
numpy for numerical operations
ydata_profiling for automated EDA reports
matplotlib.pyplot for basic plotting
seaborn for enhanced data visualization
sklearn.preprocessing.LabelEncoder for label encoding
sklearn.model_selection.train_test_split for splitting data
sklearn.linear_model.LinearRegression for building linear models
sklearn.metrics for model evaluation (R-squared, MSE)
sklearn.preprocessing.MinMaxScaler for normalization
sklearn.preprocessing.StandardScaler for standardization
3. Data Loading and Initial Exploration
The dataset, Task1.csv, is loaded into a pandas DataFrame. Initial steps include:

Loading the dataset from /content/Task1.csv.
Viewing the first 5 rows (df.head()).
Listing column names (df.columns).
Dropping the redundant 'id' column.
Checking the DataFrame's shape (df.shape).
Getting a summary of data types and non-null counts (df.info()).
Viewing descriptive statistics for numerical columns (df.describe()).
Printing unique values for 'Sex' and 'Age' columns.
Counting occurrences of each gender in the 'Sex' column (df['Sex'].value_counts()).
Generating a comprehensive ydata-profiling report (report.html) for a quick and detailed EDA overview.
4. Data Cleaning and Preprocessing
Handling Zero Height: Rows where 'Height' is recorded as 0 (an impossible measurement for a crab) are removed from the dataset, and the index is reset.
Creating 'Lost Weight' Feature: A new feature, Lost_Weight, is engineered to represent the difference between the total 'Weight' and the sum of 'Shucked Weight', 'Viscera Weight', and 'Shell Weight'. This is converted into a binary feature (0 if Lost_Weight_Calc <= 0, else 1) and inserted into the DataFrame.
5. Exploratory Data Visualization
Visualizations are used to gain deeper insights into the data:

Bar Plot: Average Age of Crabs by Sex.
Box Plot: Age Distribution by Sex, showing median, quartiles, and outliers.
KDE Plots: Kernel Density Estimate plots for 'Age', 'Length', and 'Weight' to visualize their distributions.
Scatter Plot: Relationship between 'Age' and 'Diameter'.
Correlation Matrix: A heatmap displaying the correlation of all numerical features with 'Age', identifying key relationships (e.g., 'Shell Weight' has a strong correlation with 'Age').
Violin Plot: Age Distribution by 'Lost_Weight' to compare age patterns between crabs with and without 'lost weight'.
6. Feature Engineering
One-Hot Encoding: The categorical 'Sex' column is converted into numerical format using one-hot encoding, creating Sex_F, Sex_I, and Sex_M binary columns.
Normalization (MinMaxScaler): Numerical features are scaled to a range between 0 and 1 using MinMaxScaler.
Standardization (StandardScaler): Numerical features (excluding one-hot encoded and binary Lost_Weight columns) are standardized to have a mean of 0 and a standard deviation of 1 using StandardScaler.
7. Model Comparison: One-Hot Encoding vs. Label Encoding
To demonstrate the impact of encoding choices on linear models, two LinearRegression models are trained to predict 'Age':

Model 1 (One-Hot Encoded): Uses the df DataFrame with 'Sex' one-hot encoded.
Model 2 (Label Encoded): Uses a copy of the cleaned df_original_sex DataFrame with 'Sex' label-encoded.
Both datasets are split into training and testing sets (80/20 split, random_state=42). The models are trained and evaluated using R-squared and Mean Squared Error (MSE).

Results:

One-Hot Encoded Model:
R-squared: 0.5537
Mean Squared Error: 4.3396
Label Encoded Model:
R-squared: 0.5407
Mean Squared Error: 4.4659
8. Conclusion
The comparison shows that the One-Hot Encoded Model performed marginally better, with a higher R-squared and lower MSE. This reinforces the principle that for nominal categorical variables (like 'Sex', where there's no inherent order), one-hot encoding is generally preferred for linear models. Label encoding can mislead linear models by implying an artificial ordinal relationship, which was reflected in the slightly lower performance of the label-encoded model in this case.

9. How to Run the Notebook
Open in Google Colab: Upload the .ipynb file to Google Colab.
Mount Google Drive (Optional): If prompted to mount Google Drive for data access, follow the authentication steps.
Install Dependencies: Run the cell containing !pip install ydata-profiling -q.
Execute Cells: Run all cells sequentially from top to bottom.
Review Output: Examine the outputs of each cell, including plots and printed statistics, and the generated report.html for a detailed EDA.
