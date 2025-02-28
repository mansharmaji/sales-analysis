# sales-analysis
Sales analysis of a Store for Data analysis 
# Detail Python code for Sales Analysis.

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
csv_file_path = "/mnt/data/AusApparelSales/AusApparalSales4thQrt2020.csv"
df = pd.read_csv(csv_file_path)

# Convert 'Sales' column to numeric in case of any formatting issues
df['Sales'] = pd.to_numeric(df['Sales'], errors='coerce')

# -------------------------------
# 1️⃣ State-Wise Sales Analysis
# -------------------------------
state_sales = df.groupby("State")["Sales"].sum().reset_index()
state_sales = state_sales.sort_values(by="Sales", ascending=False)

# Identify top and low performing states
top_states = state_sales.head(3)
low_states = state_sales.tail(3)

# Plot state-wise sales
plt.figure(figsize=(10, 5))
sns.barplot(data=state_sales, x="State", y="Sales", palette="viridis")
plt.title("Total Sales by State (Q4 2020)")
plt.xticks(rotation=45)
plt.show()

# -------------------------------
# 2️⃣ Sales Breakdown by Customer Group
# -------------------------------
group_sales = df.groupby("Group")["Sales"].sum().reset_index().sort_values(by="Sales", ascending=False)

# Plot sales by customer group
plt.figure(figsize=(8, 5))
sns.barplot(data=group_sales, x="Group", y="Sales", palette="magma")
plt.title("Sales by Customer Group")
plt.show()

# -------------------------------
# 3️⃣ Sales Trend Analysis by Time of Day
# -------------------------------
time_sales = df.groupby("Time")["Sales"].sum().reset_index().sort_values(by="Sales", ascending=False)

# Plot sales by time of day
plt.figure(figsize=(8, 5))
sns.barplot(data=time_sales, x="Time", y="Sales", palette="coolwarm")
plt.title("Sales Distribution by Time of Day")
plt.show()

# -------------------------------
# Summary of Insights
# -------------------------------
print("\n🔹 Top Revenue States:")
print(top_states)
print("\n🔹 Low Revenue States:")
print(low_states)
print("\n🔹 Sales Breakdown by Customer Group:")
print(group_sales)
print("\n🔹 Sales Trend by Time of Day:")
print(time_sales)

