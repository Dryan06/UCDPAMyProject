# UCDPAMyProject
# loading importing libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
import scipy as sp
import os
import warnings
warnings.filterwarnings("ignore")
df= pd.read_csv('https://raw.githubusercontent.com/Dryan06/UCDPA-DermotRyan/main/Netflix.csv')
df.head()
df.info()
# finding total number of null values
df.isnull().sum()
# finding total number of null values
df.isnull().sum()
# droppig director
df=df.drop(["director"],axis=1)
# filling all Nan values as unknown in date_added column 
df.date_added.fillna("unknown",inplace= True)
df["release_year"].value_counts()
# making another column year and extracting year from date_added
df["year"]= df.date_added.apply(lambda x: str(x).split(",")[-1])
df["year"].value_counts()
# replaying unknows in year columns with 2019 as it has appeared most 
df["year"]= df.year.apply(lambda x: str(x).replace("unknown","2019"))
# removing extra space
df["year"]= df.year.apply(lambda x: str(x).replace(" ",""))
df.year.value_counts()
df.country.value_counts() #displaying the most occurred country
# filling null values of country with most occuring country
df.country.fillna("United_states",inplace= True)
df.rating.value_counts() 
# filling null values of rating with most occuring rating
df.rating.fillna("TV-MA",inplace= True)
df.isnull().sum()
# showing TOP 10 country wise content
x=df.country.value_counts().head(10) #for top 10
plt.figure(figsize=(10,10))
ax=sns.barplot(x.values,x.index)
ax.set_xlabel("Number of Content")
ax.set_ylabel("Number of Country")
# Showing number of contents under Movie or Tv series tag
plt.figure(figsize=(10,10))
x=df.type.value_counts()
ax=sns.barplot(x.index,x.values)
ax.set_xlabel("type")
ax.set_ylabel("count")
# showing piechat of the above data 
plt.figure(figsize=(10,10))
plt.pie(x.values,labels=["Movies","TV Shows"],autopct="%1.1f%%")
plt.show()
# Netflix content releases over the years
x= df.release_year.value_counts()
plt.figure(figsize=(16,6))
plt.xlabel("Year")
sns.lineplot(x=x.index ,y= x.values)
# Showing  no. of contents in different ratings 
x=df.rating.value_counts()
plt.figure(figsize=(16,10))
plt.xlabel("Rating")
plt.ylabel("Count")
sns.barplot(x=x.index ,y= x.values)
# Pie chart of the same above data 
plt.figure(figsize=(10,10))
plt.pie(x.values,labels=x.index,autopct="%1.1f%%")
plt.show()
# Number of content added on Netflix over the years
x= df.year.value_counts()
plt.figure(figsize=(16,6))
plt.xlabel("Year")
sns.lineplot(x=x.index ,y= x.values)
# Bar chart of the same above data 
x= df.year.value_counts()
plt.figure(figsize=(16,6))
plt.xlabel("Year")
sns.barplot(x=x.index ,y= x.values)
# Showing pie chart of the same 
x= df.year.value_counts()
plt.figure(figsize=(10,10))
plt.xlabel("Year")
plt.pie(x.values,labels=x.index ,autopct="%1.1f%%")
plt.show()
