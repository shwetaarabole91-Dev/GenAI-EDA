# PART 1: DATA LOADING

import json
import sqlite3
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 1. JSON Load
with open('product_data.json', 'r') as f:
    products = json.load(f)
df_products = pd.DataFrame(products)
print(df_products.head())

# 2. SQLite DB Load
conn = sqlite3.connect('sample.db')
df_sql = pd.read_sql_query("SELECT * FROM students", conn)
print(df_sql.head())

# 3. CSV Load
df_movies = pd.read_csv('tmdb_movies.csv')
print(df_movies.head())

# PART 2: DATA CLEANING
df = pd.read_csv('tmdb_movies.csv') # ya students wala csv
df_clean = df.dropna()
df_clean.to_csv('cleaned_students.csv', index=False)

# Basic Histogram
plt.figure(figsize=(8,5))
sns.histplot(df_clean['math_score'], kde=True)
plt.title('Math Score Distribution')
plt.savefig('math_score_hist.png')
plt.show()

# PART 3: ADVANCED EDA (12 Charts)

# 1. Age Distribution
sns.histplot(df_clean['age'])
plt.savefig('age_dist.png')

# 2. Gender Count
sns.countplot(x='gender', data=df_clean)
plt.savefig('gender_count.png')

# 3. Boxplot for outliers
sns.boxplot(x=df_clean['math_score'])
plt.savefig('math_box.png')

# 4. Scatter plot
sns.scatterplot(x='study_hours', y='math_score', data=df_clean)
plt.savefig('scatter_study_math.png')

# 5. Correlation Heatmap
plt.figure(figsize=(10,6))
sns.heatmap(df_clean.corr(numeric_only=True), annot=True, cmap='coolwarm')
plt.savefig('correlation_heatmap.png')
plt.show()

print("All charts created successfully!")
