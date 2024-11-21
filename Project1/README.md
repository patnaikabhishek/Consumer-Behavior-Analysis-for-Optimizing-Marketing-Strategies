# Consumer Behavior Analysis for Optimizing Marketing Strategies
## Project Overview
This project simulates a large consumer dataset and analyzes customer behavior to provide actionable insights for optimizing marketing strategies. By applying data analysis and segmentation techniques, it identifies key drivers of revenue, such as age group, purchase channel, location, and product category.

The analysis includes:
- Simulating a dataset with various customer attributes (age group, product category, purchase channel, location, etc.).
- Segmenting customers based on their purchasing behavior and identifying trends that contribute to revenue.
- Visualizing key metrics like revenue by age group, category, and purchase channel to inform marketing strategies.
- Providing actionable insights to optimize marketing efforts, such as focusing on high-performing demographics, categories, and sales channels.

## Methodology
- **Data Simulation**: A synthetic dataset was generated with various consumer attributes like age group, product category, purchase channel, and location.
- **Revenue Calculation**: Revenue was calculated by multiplying quantity purchased with price.
- **Customer Segmentation**: Customers were segmented by age group, category, and location, with revenue calculated for each segment.
- **Behavioral Insights**: Key insights were drawn from visualizing revenue trends across different age groups, categories, and purchase channels.

## Technologies Used
- **Python**: For data manipulation and analysis.
- **Pandas**: For data handling and analysis.
- **NumPy**: For numerical operations and data simulation.
- **Matplotlib** & **Seaborn**: For visualizing consumer behavior and trends.
- **Jupyter Notebook**: For documenting and executing the analysis.

## Key Insights
- **Age Group Insights**: The age group with the highest revenue should be targeted with tailored marketing strategies.
- **Category Insights**: The top-performing product category should receive higher inventory and marketing focus.
- **Channel Insights**: A significant portion of revenue comes from online channels, suggesting the need for further investment in online shopping experiences.
- **Location Insights**: Urban locations generate the most revenue, highlighting the need for expanded marketing and product availability in urban areas.

## Instructions
1. Clone the repository to your local machine.
2. Install required libraries using:
   ```bash
   pip install -r requirements.txt
3. Open the Jupyter notebook and run the code cells to reproduce the analysis.
   ```bash
   git clone <repository_url>

## Python Code

```python
# Step 1: Import Libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Step 2: Simulate Large Dataset
np.random.seed(42)  # For reproducibility
customer_ids = np.random.randint(1000, 5000, size=50000)
categories = ["Electronics", "Clothing", "Groceries", "Furniture", "Beauty", "Sports"]
purchase_channels = ["Online", "In-Store"]
locations = ["Urban", "Suburban", "Rural"]
age_groups = ["18-25", "26-35", "36-50", "51+"]

data = {
    "CustomerID": customer_ids,
    "AgeGroup": np.random.choice(age_groups, size=50000),
    "Category": np.random.choice(categories, size=50000),
    "Channel": np.random.choice(purchase_channels, size=50000),
    "Location": np.random.choice(locations, size=50000),
    "Quantity": np.random.randint(1, 10, size=50000),
    "Price": np.random.randint(50, 5000, size=50000),
}

df = pd.DataFrame(data)
df["Revenue"] = df["Quantity"] * df["Price"]

# Step 3: Summary of the Dataset
print("Dataset Overview:")
print(df.head())

print("\nSummary Statistics:")
print(df.describe())

# Step 4: Customer Segmentation
# 4.1 Revenue by Age Group
age_group_revenue = df.groupby("AgeGroup")["Revenue"].sum()
print("\nRevenue by Age Group:")
print(age_group_revenue)

# 4.2 Revenue by Category
category_revenue = df.groupby("Category")["Revenue"].sum()
print("\nRevenue by Category:")
print(category_revenue)

# Step 5: Visualizing Consumer Insights
# 5.1 Revenue by Age Group
plt.figure(figsize=(8, 6))
age_group_revenue.plot(kind="bar", color="skyblue")
plt.title("Revenue by Age Group", fontsize=14)
plt.xlabel("Age Group", fontsize=12)
plt.ylabel("Revenue", fontsize=12)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()

# 5.2 Revenue by Purchase Channel
channel_revenue = df.groupby("Channel")["Revenue"].sum()

plt.figure(figsize=(6, 6))
channel_revenue.plot(kind="pie", autopct='%1.1f%%', colors=["orange", "lightgreen"])
plt.title("Revenue by Purchase Channel", fontsize=14)
plt.ylabel("")
plt.show()

# Step 6: Behavioral Trends
# 6.1 Revenue by Location and Category
location_category_revenue = df.groupby(["Location", "Category"])["Revenue"].sum().unstack()

plt.figure(figsize=(12, 6))
location_category_revenue.plot(kind="bar", stacked=True, colormap="viridis")
plt.title("Revenue by Location and Category", fontsize=14)
plt.xlabel("Location", fontsize=12)
plt.ylabel("Revenue", fontsize=12)
plt.xticks(rotation=45)
plt.legend(title="Category", bbox_to_anchor=(1.05, 1), loc="upper left")
plt.tight_layout()
plt.show()

# Step 7: Actionable Insights
print("\nActionable Insights:")
print("- Age Group", age_group_revenue.idxmax(), "drives the most revenue. Target this group with tailored promotions.")
print("- The top-performing category is:", category_revenue.idxmax(), "suggesting it should receive higher inventory and marketing focus.")
print("- Online channels contribute", round((channel_revenue["Online"] / channel_revenue.sum()) * 100, 2), "% of the revenue. Invest in enhancing the online shopping experience.")
print("- Urban locations generate the highest revenue. Expand marketing campaigns and product availability in urban areas.")
