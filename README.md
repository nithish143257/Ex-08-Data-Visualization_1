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
NAME: EASWAR.J
REG NO: 212221230024
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

![ds_ex8 (1)](https://user-images.githubusercontent.com/94154683/202210674-49d9caf6-67c9-4dd4-900b-206b3d09eaad.png)
![ds_ex8 (2)](https://user-images.githubusercontent.com/94154683/202210675-ca807cdc-bd30-4fbb-8162-c3814c4dccfd.png)
![ds_ex8 (3)](https://user-images.githubusercontent.com/94154683/202210679-65d8b85a-6377-4e83-b456-79070c90d5f4.png)
![ds_ex8 (4)](https://user-images.githubusercontent.com/94154683/202210684-a26f76d0-643f-4b4e-9501-2c0e9ea94bab.png)
![ds_ex8 (5)](https://user-images.githubusercontent.com/94154683/202210687-4bb48ae8-78e3-4a8e-9187-be12a6a87591.png)
## Line Plot:
![ds_ex8 (6)](https://user-images.githubusercontent.com/94154683/202210482-d467a856-2b3d-494f-8587-c0889a7b9f75.png)
![ds_ex8 (7)](https://user-images.githubusercontent.com/94154683/202210487-34640960-b6a1-4927-bf2e-4a26522693f3.png)
![ds_ex8 (8)](https://user-images.githubusercontent.com/94154683/202210496-e16a1730-8c0a-41a1-a31a-5aedb04ca626.png)
![ds_ex8 (9)](https://user-images.githubusercontent.com/94154683/202210497-0e118340-3496-4249-be28-bf695b1d2132.png)
![ds_ex8 (10)](https://user-images.githubusercontent.com/94154683/202210501-dd0fe56a-0eb5-4f4d-88d0-b41e2215ca43.png)
![ds_ex8 (11)](https://user-images.githubusercontent.com/94154683/202210506-6ca09c21-2bdc-49e7-9a64-f90636c13a0c.png)
![ds_ex8 (12)](https://user-images.githubusercontent.com/94154683/202210509-cb3b30a1-a4c5-4697-94d4-4a3b2ad6ea93.png)
## Bar Plot:
![ds_ex8 (13)](https://user-images.githubusercontent.com/94154683/202210511-2fc7104a-7fed-4c7a-be8e-8af48368834c.png)
![ds_ex8 (14)](https://user-images.githubusercontent.com/94154683/202210516-dc88657f-5697-43a1-bcff-6dde5ca8df34.png)
![ds_ex8 (15)](https://user-images.githubusercontent.com/94154683/202210520-40beb794-d1f6-4be9-910c-0a2b3909a94f.png)
![ds_ex8 (16)](https://user-images.githubusercontent.com/94154683/202210527-a397845e-53bc-4607-8f5e-1ee5dddd3ea1.png)
![ds_ex8 (17)](https://user-images.githubusercontent.com/94154683/202210532-e7ab34f9-ecac-4027-9907-98e331c29441.png)
![ds_ex8 (18)](https://user-images.githubusercontent.com/94154683/202210535-4d6eb5fc-f999-4e94-b64b-ba212cf7cd9a.png)
## Histogram:
![ds_ex8 (19)](https://user-images.githubusercontent.com/94154683/202210540-fb950f9c-a0a7-40bd-baaa-851a644c79db.png)
![ds_ex8 (20)](https://user-images.githubusercontent.com/94154683/202210544-1f7f2719-08d5-4ec5-b868-732ec45b9560.png)
![ds_ex8 (21)](https://user-images.githubusercontent.com/94154683/202210546-0131fd9a-a547-4a52-acee-40ac5aec2737.png)
![ds_ex8 (22)](https://user-images.githubusercontent.com/94154683/202210548-3391a2e0-5522-4383-a7d9-08d51ab03ba4.png)
![ds_ex8 (23)](https://user-images.githubusercontent.com/94154683/202210551-7e805f8d-36f6-4600-b596-d48697c5f115.png)
## Count plot:
![ds_ex8 (24)](https://user-images.githubusercontent.com/94154683/202210555-65d75f75-3c0a-4a51-83f7-435d383d23d5.png)
![ds_ex8 (25)](https://user-images.githubusercontent.com/94154683/202210557-f8a69a2b-235f-4d75-bdb1-9395920e0d0c.png)
![ds_ex8 (26)](https://user-images.githubusercontent.com/94154683/202210562-c8933adb-6b81-42b1-acd7-06813b53a590.png)
![ds_ex8 (27)](https://user-images.githubusercontent.com/94154683/202210566-77c241c4-3899-4173-bd99-5b1b8700da21.png)
![ds_ex8 (28)](https://user-images.githubusercontent.com/94154683/202210571-9fa989da-54d3-4c10-a6e4-eb4a0b9da22a.png)
## Box plot:
![ds_ex8 (29)](https://user-images.githubusercontent.com/94154683/202210573-fc107268-1c24-4baa-992c-b966c8dd02f3.png)
![ds_ex8 (30)](https://user-images.githubusercontent.com/94154683/202210577-eea97260-2b34-4258-9e90-f2e9ca508262.png)
![ds_ex8 (31)](https://user-images.githubusercontent.com/94154683/202210581-8a782f24-ef13-484f-904c-0eb167272816.png)
![ds_ex8 (32)](https://user-images.githubusercontent.com/94154683/202210584-ba1e0bca-2f3c-4a75-bf3f-bfc96fcb120d.png)
![ds_ex8 (33)](https://user-images.githubusercontent.com/94154683/202210590-00488078-d10d-4300-8cec-ce1420881ff2.png)
![ds_ex8 (34)](https://user-images.githubusercontent.com/94154683/202210593-fbc385ae-df6f-4884-b147-9da44def7ae4.png)
![ds_ex8 (35)](https://user-images.githubusercontent.com/94154683/202210598-795b3454-6e02-4577-973f-f888e6174be2.png)
![ds_ex8 (36)](https://user-images.githubusercontent.com/94154683/202210604-39574958-ee00-43f5-b6ee-34887b97525b.png)
## KDE Plot:
![ds_ex8 (37)](https://user-images.githubusercontent.com/94154683/202210609-fc22ffe0-8c83-469b-8e7d-a55539e0dda1.png)
![ds_ex8 (38)](https://user-images.githubusercontent.com/94154683/202210613-81f86888-3b32-4df8-ae5b-27ab29956e62.png)
![ds_ex8 (39)](https://user-images.githubusercontent.com/94154683/202210618-308adf47-f409-4c86-a67d-c509fb620ef2.png)
![ds_ex8 (40)](https://user-images.githubusercontent.com/94154683/202210621-0e051a99-864f-4c31-be03-ab7c8d026427.png)
## Violin Plot:
![ds_ex8 (41)](https://user-images.githubusercontent.com/94154683/202210625-cd219f9b-6a3d-490a-b06f-5535aeada217.png)
![ds_ex8 (42)](https://user-images.githubusercontent.com/94154683/202210629-856ce30d-e0da-44ba-98f7-660a298e8ae6.png)
![ds_ex8 (43)](https://user-images.githubusercontent.com/94154683/202210631-6ec0daa7-d7b3-4963-a5f9-8493ab1f37b7.png)
![ds_ex8 (44)](https://user-images.githubusercontent.com/94154683/202210637-bc64d244-58a1-428d-a3cd-b9abbcfe70eb.png)
## Point Plot:
![ds_ex8 (45)](https://user-images.githubusercontent.com/94154683/202210641-990f6b9f-9be2-461b-bb7f-a9761ef5aa73.png)
![ds_ex8 (46)](https://user-images.githubusercontent.com/94154683/202210647-31432917-9137-4176-8a3b-cb1e79d7140d.png)
![ds_ex8 (47)](https://user-images.githubusercontent.com/94154683/202210649-abf33193-c0ce-4b0b-876f-0b29dab48577.png)
![ds_ex8 (48)](https://user-images.githubusercontent.com/94154683/202210651-c180891d-bd7b-4839-88c8-fe8b14927852.png)
## Pie Chart:
![ds_ex8 (49)](https://user-images.githubusercontent.com/94154683/202210655-f930f19b-d085-4364-ae0e-492186ba8ea0.png)
![ds_ex8 (50)](https://user-images.githubusercontent.com/94154683/202210659-e96595ed-1850-4e07-a669-78ea72a0eb39.png)
![ds_ex8 (51)](https://user-images.githubusercontent.com/94154683/202210662-ba865792-c3e4-420a-9fcd-1fa94ab425e7.png)
![ds_ex8 (52)](https://user-images.githubusercontent.com/94154683/202210665-349c6a97-ed5c-4c39-ac10-d440d705fd7a.png)
![ds_ex8 (53)](https://user-images.githubusercontent.com/94154683/202210669-1dd1219c-1f1b-408e-b529-03c6bbd8ef70.png)

