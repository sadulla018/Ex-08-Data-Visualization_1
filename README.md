# Ex-08-Data-Visualization-

## AIM
To Perform Data Visualization on a complex dataset and save the data to a file. 

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
### STEP 1
Read the given Data
### STEP 2
Clean the Data Set using Data Cleaning Process
### STEP 3
Apply Feature generation and selection techniques to all the features of the data set
### STEP 4
Apply data visualization techniques to identify the patterns of the data.


# CODE:

```
NAME: SK.Sadulla
REG NO: 212220040151
```
```
#loading the dataset
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("Superstore.csv")
df

#removing unnecessary data variables
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df

df.isnull().sum()

#detecting and removing outliers in current numeric data
plt.figure(figsize=(12,10))
plt.title("Data with outliers")
df.boxplot()
plt.show()

plt.figure(figsize=(12,10))
cols = ['Sales','Quantity','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()

#data visualization
#line plots
import seaborn as sns
sns.lineplot(x="Sub-Category",y="Sales",data=df,marker='o')
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.lineplot(x="Category",y="Profit",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Categories vs Profit")
plt.show()

sns.lineplot(x="Region",y="Sales",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Region area vs Sales")
plt.show()

sns.lineplot(x="Category",y="Discount",data=df,marker='o')
plt.title("Categories vs Discount")
plt.show()

sns.lineplot(x="Sub-Category",y="Quantity",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Sub Categories vs Quantity")
plt.show()

#bar plots
sns.barplot(x="Sub-Category",y="Sales",data=df)
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Profit",data=df)
plt.title("Categories vs Profit")
plt.show()

sns.barplot(x="Sub-Category",y="Quantity",data=df)
plt.title("Sub Categories vs Quantity")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Discount",data=df)
plt.title("Categories vs Discount")
plt.show()

plt.figure(figsize=(12,7))
sns.barplot(x="State",y="Sales",data=df)
plt.title("States vs Sales")
plt.xticks(rotation = 90)
plt.show()

plt.figure(figsize=(25,8))
sns.barplot(x="State",y="Sales",hue="Region",data=df)
plt.title("State vs Sales based on Region")
plt.xticks(rotation = 90)
plt.show()

#Histogram
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()

#count plot
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')

#Barplot 
sns.boxplot(x="Sub-Category",y="Discount",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot( x="Profit", y="Category",data=df)
plt.xticks(rotation = 90)
plt.show()
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Profit",data=df)
sns.boxplot(x="Region",y="Sales",data=df)
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Quantity",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Discount",data=df)
plt.figure(figsize=(15,7))
sns.boxplot(x="State",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()

#KDE plot
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')

#violin plot
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)

#point plot
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])

#Pie Chart
df.groupby(['Category']).sum().plot(kind='pie', y='Discount',figsize=(6,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Sub-Category']).sum().plot(kind='pie', y='Sales',figsize=(10,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Region']).sum().plot(kind='pie', y='Profit',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Ship Mode']).sum().plot(kind='pie', y='Quantity',figsize=(8,11),pctdistance=1.7,labeldistance=1.2)

df1=df.groupby(by=["Category"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)  
plt.figure(figsize=(8,8))
colors = sns.color_palette('pastel')
plt.pie(df1["Profit"],colors = colors,labels=labels, autopct = '%0.0f%%')
plt.show()

df1=df.groupby(by=["Ship Mode"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)
colors=sns.color_palette("bright")
plt.pie(df1["Sales"],labels=labels,autopct="%0.0f%%")
plt.show()

#HeatMap
df4=df.copy()

#encoding
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])

#scaling
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])

#Heatmap
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
```
# OUPUT

## Initial Dataset:
![image](https://user-images.githubusercontent.com/113021631/205608170-0d7ca6e4-8fc9-458c-a878-0a35e858bc90.png)

## Cleaned Dataset:
![image](https://user-images.githubusercontent.com/113021631/205608357-bcafc54b-8731-4196-8e13-ca383c23a9bf.png)


## Removing Outliers:
![image](https://user-images.githubusercontent.com/113021631/205608611-bd978ed4-eb7a-4739-b6f1-41b7e2da1957.png)
![image](https://user-images.githubusercontent.com/113021631/205608730-15c897bc-eb40-43f0-9b61-6d74f2f25952.png)


## Line PLot:
![image](https://user-images.githubusercontent.com/113021631/205609116-2de98db3-c077-4338-a95d-a0d97f0daf97.png)
![image](https://user-images.githubusercontent.com/113021631/205609233-a3fcedc4-39cf-423f-8275-22a42202a01d.png)
![image](https://user-images.githubusercontent.com/113021631/205609351-1946981e-4c9e-41a3-97c3-57a2fac92573.png)

## Bar Plots:
![image](https://user-images.githubusercontent.com/113021631/205609534-5b597c3f-7307-483a-a396-b8ef75c79c96.png)
![image](https://user-images.githubusercontent.com/113021631/205609645-9ee6144a-28e7-4599-89bf-2abf796d8478.png)
![image](https://user-images.githubusercontent.com/113021631/205609836-10d8135b-71ff-4adf-84eb-f4c40b2b56b9.png)
![image](https://user-images.githubusercontent.com/113021631/205609956-d9ff5afe-ab08-4b2a-b5f7-5c4de5d096c2.png)


## Histograms:
![image](https://user-images.githubusercontent.com/113021631/205610129-e5fadfaf-9be9-4a3f-b449-4c85271db081.png)
![image](https://user-images.githubusercontent.com/113021631/205610234-ccdf5e8f-7a74-4fa6-a1ce-5ddb38634e11.png)
![image](https://user-images.githubusercontent.com/113021631/205610398-2ec38172-cd11-4837-95b1-31b9e8a74649.png)

## Count plots:
![image](https://user-images.githubusercontent.com/113021631/205610538-545a730c-1438-4007-ba27-fa83d9e97826.png)
![image](https://user-images.githubusercontent.com/113021631/205610693-9c32f419-70fa-459e-ad89-b63a50326d1d.png)
![image](https://user-images.githubusercontent.com/113021631/205610913-f96592b7-f904-4857-b01f-438284134ecc.png)


## Bar Charts:
![image](https://user-images.githubusercontent.com/113021631/205611003-dd04ab94-9a89-4fcf-ba19-c9f084ebc692.png)
![image](https://user-images.githubusercontent.com/113021631/205611099-5e7f8185-4708-4c51-b3c7-62d4bd35fcdf.png)
![image](https://user-images.githubusercontent.com/113021631/205611208-476b87ec-ace5-48c5-9579-ce69ba23bcf5.png)
![image](https://user-images.githubusercontent.com/113021631/205611316-964884a3-d3f9-4d72-b800-b90bfe39d738.png)
![image](https://user-images.githubusercontent.com/113021631/205611453-86905b47-88bb-48ab-b1e7-de68a5088818.png)
![image](https://user-images.githubusercontent.com/113021631/205611607-8fc83225-2917-496c-927c-a044440374af.png)

## KDE Plots:
![image](https://user-images.githubusercontent.com/113021631/205611764-fe9fbd7d-1c24-4afb-8db0-33132ca1bbe0.png)
![image](https://user-images.githubusercontent.com/113021631/205611857-24e6b010-c61d-428e-a49e-3626813091a0.png)

## Violin Plot:
![image](https://user-images.githubusercontent.com/113021631/205611978-61b6bad5-674f-4c71-8795-30af2e887da1.png)
![image](https://user-images.githubusercontent.com/113021631/205612047-63b8a597-1132-4388-a779-2560b31575d5.png)


## Point Plots:


## Pie Charts:
![image](https://user-images.githubusercontent.com/113021631/205612295-afb1799a-c57e-43f5-83bd-4ab03d05d098.png)
![image](https://user-images.githubusercontent.com/113021631/205612375-8d2596e4-8bb9-4e9e-9cac-b2fa0767096c.png)
![image](https://user-images.githubusercontent.com/113021631/205612515-f03566dc-aa92-493e-8465-60f2fb2c435d.png)
![image](https://user-images.githubusercontent.com/113021631/205612661-7af18df7-7196-4357-8f97-75614207f42a.png)
![image](https://user-images.githubusercontent.com/113021631/205612740-129aaf65-b7fc-4340-ba2b-d5f2d0a324f3.png)


## HeatMap:
![image](https://user-images.githubusercontent.com/113021631/205612186-c0285876-a95b-4fd8-9b39-bb5dd3cb8e27.png)

# Result:
Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file
