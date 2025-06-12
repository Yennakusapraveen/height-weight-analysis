# height-weight-analysis
Beginner-level data analysis on height and weight using Python &amp; Google Colab
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# For inline plotting in Colab
%matplotlib inline

print("All libraries loaded!")
from google.colab import files
uploaded = files.upload()
# Load the file (if the file has a different name, adjust it accordingly)
df = pd.read_csv("sales_data.csv")

# Display the first few rows
df.head()
df.info()
df.describe()
print(df.columns)
# Remove any unwanted quotes or spaces from column names
df.columns = df.columns.str.strip().str.replace('"', '')
print(df.columns)
# Check for missing data
print(df.isnull().sum())

# Remove rows with missing values (if any exist)
df = df.dropna()
plt.figure(figsize=(8,4))
sns.histplot(df['Height(Inches)'], kde=True, color='skyblue')
plt.title("Distribution of Heights (Inches)")
plt.xlabel("Height (Inches)")
plt.show()
plt.figure(figsize=(8,6))
sns.scatterplot(x='Height(Inches)', y='Weight(Pounds)', data=df, color='green')
plt.title("Scatter Plot: Height vs. Weight")
plt.xlabel("Height (Inches)")
plt.ylabel("Weight (Pounds)")
plt.show()
# Calculate the correlation between Height and Weight
correlation = df['Height(Inches)'].corr(df['Weight(Pounds)'])
print(f"Correlation between Height and Weight: {correlation:.2f}")
plt.figure(figsize=(8,6))
sns.regplot(x='Height(Inches)', y='Weight(Pounds)', data=df, scatter_kws={"color":"blue"}, line_kws={"color":"red"})
plt.title("Height vs Weight with Regression Line")
plt.xlabel("Height (Inches)")
plt.ylabel("Weight (Pounds)")
plt.show()

