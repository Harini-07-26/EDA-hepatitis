# EDA-hepatitis
#impotring libraries and dataset
from google.colab import files
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt 
uploaded = files.upload()
import io
df = pd.read_csv(io.BytesIO(uploaded['hepatitis.csv']))
df

#to display first 5 rows
df.head(5)
df
#to display last 5 rows
df.tail(5)
df

#to find the data types of the data in the csv file
df.dtypes

#dropping the irrelevent column
df = df.drop(['histology','protime'], axis=1)
df

#renaming the existing column
df = df.rename(columns={"class": "live status"})
df

#finding shape of dataset
df.shape

#finding duplicate entries
duplicate_rows_df = df[df.duplicated()]
print("number of duplicate rows: ", duplicate_rows_df.shape)

df.count()
df = df.drop_duplicates()
df
df.count()
print(df.isnull().sum())
df = df.dropna() 
df.count()
print(df.isnull().sum()) 

#box plot
sns.boxplot(x=df['age'])

Q1 = df.quantile(0.25)
Q3 = df.quantile(0.75)
IQR = Q3-Q1
print(IQR)
df = df[~((df < (Q1-1.5 * IQR)) |(df > (Q3+1.5 * IQR))).any(axis=1)]
df.shape

#plotting the data using the scatter plot
fig, ax = plt.subplots(figsize=(10,6))
ax.scatter(df['sex'], df['age'])
ax.set_xlabel('sex')
ax.set_ylabel('age')
plt.show()
