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

