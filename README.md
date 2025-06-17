# 🎉 Diwali Sales Data Analysis

This Python project performs exploratory data analysis (EDA) on Diwali sales data to uncover customer purchasing patterns. It uses Pandas for data cleaning and manipulation and Seaborn/Matplotlib for visualizations, analyzing factors like gender, age, state, marital status, occupation, and product categories. Ideal for learning data preprocessing and visualization techniques.

## Features
- **Data Cleaning**: Removes irrelevant columns, handles missing values, and converts data types for analysis.
- **Exploratory Data Analysis (EDA)**: Visualizes relationships between customer attributes (e.g., gender, age group, state) and sales metrics (orders, amount spent).
- **Key Insights**: Identifies high-spending customer segments, such as married women aged 26–35 from specific states and occupations.
- **Visualizations**: Includes bar plots and count plots to show trends in gender, age, state, marital status, occupation, and product categories.
- **Top Products**: Highlights the most sold products and categories by order volume and revenue.

## Interesting Techniques Used
Let’s dive into the key techniques used in this project, explained step-by-step like we’re sketching it out on a whiteboard. I’ll keep it clear and intuitive, so you can follow along even if you’re new to data analysis.

### 1. Data Cleaning for Reliable Analysis
Before diving into visualizations, we clean the dataset to ensure it’s ready for analysis. This involves removing unnecessary columns, handling missing values, and fixing data types.

- **What’s happening?**: We drop two columns (`Status` and `unnamed1`) that are irrelevant or blank using `df.drop(['Status', 'unnamed1'], axis=1, inplace=True)`. We check for null values with `pd.isnull(df).sum()`, then remove rows with missing values using `df.dropna(inplace=True)`. Finally, we convert the `Amount` column from float to integer with `df['Amount'].astype('int')`.
- **How it works**: For example, if a row has a missing `Amount`, `df.dropna()` removes it to avoid errors in calculations. Converting `Amount` to an integer ensures cleaner numerical operations (e.g., summing sales). Dropping columns reduces noise, focusing on relevant features like `Gender` or `Product_Category`.
- **Why it’s cool**: Clean data is the foundation of good analysis. By removing nulls and fixing types, we ensure our visualizations and aggregations (e.g., total sales by state) are accurate. Check out [Pandas’ documentation on `dropna`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.dropna.html) for more details.

### 2. Grouping and Aggregating for Insights
To understand customer behavior, we group data by attributes like `Gender`, `Age Group`, or `State` and aggregate metrics like `Orders` or `Amount` to find patterns.

- **What’s happening?**: We use `df.groupby(['Gender'], as_index=False)['Amount'].sum()` to calculate total spending by gender. For example, grouping by `State` and summing `Orders` gives us the top 10 states by order volume. We sort results with `.sort_values(by='Amount', ascending=False)` to highlight the biggest contributors.
- **How it works**: Let’s say we group by `Gender`. For each group (`Male`, `Female`), Pandas sums the `Amount` column. If females spent $5M and males spent $3M, the result is a DataFrame with these totals. We then pass this to Seaborn’s `barplot` to visualize the difference.
- **Why it’s cool**: Grouping lets us answer questions like “Which state has the most orders?” or “Which age group spends the most?” in a single line of code. It’s a powerful way to summarize data without manual iteration. See [Pandas’ groupby documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.groupby.html) for more.

### 3. Visualizing Trends with Seaborn
Seaborn’s `countplot` and `barplot` make it easy to visualize categorical data, like the number of buyers by gender or total sales by product category.

- **What’s happening?**: For example, `sns.countplot(x='Gender', data=df)` creates a bar plot showing the count of male vs. female buyers. Adding `hue='Gender'` to `sns.countplot(x='Age Group', hue='Gender', data=df)` splits bars by gender within each age group. We use `ax.bar_label(bars)` to display exact counts on the bars.
- **How it works**: Seaborn takes the grouped data (e.g., counts of `Gender`) and plots bars automatically. For `sales_gen = df.groupby(['Gender'], as_index=False)['Amount'].sum()`, we pass the result to `sns.barplot(x='Gender', y='Amount', data=sales_gen)` to show total spending. The `hue` parameter adds color-coding for additional dimensions (e.g., gender within marital status).
- **Why it’s cool**: Seaborn simplifies complex visualizations, making trends like “females spend more than males” instantly clear. The `bar_label` trick adds precise numbers to plots, avoiding guesswork. Check out [Seaborn’s barplot documentation](https://seaborn.pydata.org/generated/seaborn.barplot.html) for more.

## Non-Obvious Libraries/Tools Used
- **[Pandas](https://pandas.pydata.org/)**: Handles data loading, cleaning, and grouping. Its `groupby` and `dropna` functions are key for preparing data for analysis.
- **[Seaborn](https://seaborn.pydata.org/)**: Simplifies categorical visualizations with `countplot` and `barplot`, offering intuitive `hue` support for multi-dimensional analysis.
- **[Matplotlib](https://matplotlib.org/)**: Used to customize plot sizes (e.g., `sns.set(rc={'figure.figsize':(15,5)})`) and create alternative bar plots for top products.
- **[NumPy](https://numpy.org/)**: Provides numerical utilities, implicitly used by Pandas and Seaborn for calculations.

## Project Folder Structure

- **diwali_sales_analysis.py**: The main Python script with data cleaning, EDA, and visualizations.
- **README.md**: This documentation file.
## Setup and Run
1. **Prerequisites**: Python 3.8+, pip, and a Jupyter environment (e.g., Google Colab or local Jupyter Notebook).
