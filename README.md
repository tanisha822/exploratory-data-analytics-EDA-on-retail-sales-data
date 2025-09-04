import pandas as pd

def load_data(sales_path, product_path):
    """Load sales and product datasets."""
    sales_df = pd.read_csv(sales_path, parse_dates=["order_date"])
    product_df = pd.read_csv(product_path)
    return sales_df, product_df

def clean_sales_data(sales_df):
    """Handle missing values and ensure correct datatypes."""
    sales_df = sales_df.dropna(subset=["order_id", "order_date", "customer_id"])
    sales_df["order_date"] = pd.to_datetime(sales_df["order_date"])
    return sales_df

def descriptive_stats(sales_df):
    """Return summary statistics of revenue and quantity."""
    return sales_df[["revenue", "quantity", "discount_rate"]].describe()

def add_time_features(sales_df):
    """Add year, month, day features for time series analysis."""
    sales_df["year"] = sales_df["order_date"].dt.year
    sales_df["month"] = sales_df["order_date"].dt.month
    sales_df["day"] = sales_df["order_date"].dt.day
    return sales_df

# EDA on Retail Sales Data

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from retail_utils import load_data, clean_sales_data, descriptive_stats, add_time_features

# Load Data
sales_df, prod_df = load_data("../data/dataset1_retail_sales.csv",
                              "../data/dataset2_product_catalog.csv")

# Clean Data
sales_df = clean_sales_data(sales_df)

# Merge with product info
df = sales_df.merge(prod_df, on="product_id", how="left")

# Add time features
df = add_time_features(df)

# 1. Descriptive Statistics
print("Descriptive Stats:\n", descriptive_stats(df))

# 2. Time Series Analysis
monthly_sales = df.groupby(["year", "month"])["revenue"].sum().reset_index()
monthly_sales["date"] = pd.to_datetime(monthly_sales[["year", "month"]].assign(day=1))

plt.figure(figsize=(10,5))
sns.lineplot(data=monthly_sales, x="date", y="revenue")
plt.title("Monthly Revenue Trend")
plt.show()

# 3. Customer Analysis
customer_rev = df.groupby("customer_id")["revenue"].sum().reset_index()
plt.figure(figsize=(8,5))
sns.histplot(customer_rev["revenue"], bins=30, kde=True)
plt.title("Distribution of Customer Revenue")
plt.show()

# 4. Product Analysis
top_products = df.groupby("product_name")["revenue"].sum().nlargest(10)
plt.figure(figsize=(10,5))
sns.barplot(x=top_products.values, y=top_products.index)
plt.title("Top 10 Products by Revenue")
plt.show()

# 5. Heatmap (Correlation)
plt.figure(figsize=(8,6))
sns.heatmap(df[["quantity", "revenue", "discount_rate"]].corr(), annot=True, cmap="coolwarm")
plt.title("Correlation Heatmap")
plt.show()

# Recommendations (example)
print("\nRecommendations:")
print("1. Focus marketing on top-selling products.")
print("2. Retain high-value customers with loyalty programs.")
print("3. Monitor discounting strategy impact on revenue.")
print("4. Plan inventory based on seasonal demand.")
