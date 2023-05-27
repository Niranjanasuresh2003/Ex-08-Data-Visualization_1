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


# CODE

# loading the dataset
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("Superstore.csv")
df
# removing unnecessary data variables
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
# detecting and removing outliers in current numeric data
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
# data visualization
# line plots
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
# bar plots
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
# Histogram
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
# count plot
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
# Barplot
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
# KDE plot
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
#violin plot
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
# point plot
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
# Pie Chart
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
# HeatMap
df4=df.copy()
# encoding
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

# Heatmap
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()

# OUPUT

# Initial Dataset:

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/0a386020-2b95-41db-8d35-f002b159819b)


# Cleaned Dataset:

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/146209d1-443c-4b0a-8a9a-17c0e0334b78)

# Removing Outliers:

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/482ac29f-2e7e-4947-aa9d-afc8e2923fc7)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/be8faeed-d07a-4673-8d21-67bb934e0ede)

# Line PLot:

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/1ee8062c-508b-4199-83b1-1a677fb13b8c)


![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/0c774e06-f648-4262-809c-c358ac1c4215)


![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/d8c9f36d-e04e-45a4-b705-ba1dabba32e7)


![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/f4c7e244-b5e4-45a8-8172-17827d2ec526)


# Bar Plots:

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/34e4bd25-e9a8-4e4f-b584-b6ebb57c7c19)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/98d93161-3c6a-414f-9361-40489426a24d)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/09ca4172-9031-49dd-9b4e-c12d787ef6e9)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/2d91f839-c2e2-45da-af48-e3f8233da3b7)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/5836988a-3c5a-4765-9520-d6a324c9f7c3)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/028ff07f-27d8-4b04-a36e-c63c790f2424)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/72114122-d251-45ea-a8e6-8910ca1ff379)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/b77d4278-8fc6-48bb-aa3e-90ef2522a807)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/040e4d53-56ab-4005-9e92-10e7f71a686f)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/afd5ddd3-9c9c-4857-981d-173bde997a46)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/8d68f404-ed68-448c-a75e-3a86b7e7fb81)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/558001c0-c5b2-481c-b6ac-875db6277964)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/f8bd37b6-0832-44aa-87b4-579571fb076c)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/53ec2eb4-4d4f-4263-aaff-ddcf79dbfa89)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/bfd17c72-599f-4b0a-ae22-37652f8f71c0)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/e7fe0bdb-cdfe-4f50-8a1b-e4f464f9efa4)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/ffe8d741-f29a-4dae-a41e-eed494f6560f)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/c05a071a-6b62-468d-8ffa-dabdbab22d9b)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/4ecfd35e-5a99-4e35-85a3-7c66e18f5ba6)


# Histograms:

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/c2aa78e6-1439-4ef5-9168-9afbc456a46d)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/32a085da-247d-4348-9354-dc07f89aa620)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/6caed301-c52d-4c34-b78d-9a1dbf1b7461)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/0d9822c0-d04a-4a36-b053-f787fa77626d)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/03e84bfb-1a38-4657-80ed-fbe108428cc3)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/cb1356b0-4533-4ba9-922c-86d5af9d3ac4)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/46622d05-59f2-4699-8ae6-de93d16c90ef)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/4d877f01-2bdc-46c4-8bbc-6dce2c06bcaf)


![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/a6c2d40e-b24f-4db0-b6f7-df1bc52969b2)


# Count plots:

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/085c4b8b-8f07-45aa-9749-322cdbb7ed14)


![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/ae67cce0-6dc7-429a-b2ee-098e08468564)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/3c1bd6b4-a9ff-42be-8f3b-789e08ee5991)

# Bar Charts:

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/27006094-04db-49fe-ad19-bb7909a6de68)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/383abd05-90c2-4986-b7aa-6182a67cfe92)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/4a8e0507-d722-4abd-b1e6-9b755b65f272)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/60927df9-ab46-4ec4-af00-a61decdffdfb)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/3ab213c3-c442-4aa1-a4d1-a8b2e95220f5)

# KDE Plots:

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/10e8476b-15ff-4050-8431-1d5692a167be)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/e7fb63b6-5eb4-4aad-b96e-d0711e4e89aa)

# Violin Plot:

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/015a62eb-5c05-4e1d-808e-67da6a656dba)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/5a8efa29-0866-470b-ba1e-46a1516443c6)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/8ec9d351-ac34-4d31-9bfc-b8a097fa1f40)

# Point Plots:

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/5acc3f38-d1ca-4947-b461-ba90dc0f1476)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/01171e4e-0eaa-409b-a57f-c6b2a990ceef)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/d280dcac-0b5e-4563-9b4f-1b6ddc30ed99)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/0ee526b4-31de-4e41-b90a-15f3315a90df)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/77efb982-22bd-452e-9d4e-e27f06e978e2)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/134c4e3e-196a-4224-92f7-c20ee511b059)

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/9ddc705e-0b49-4f3f-95ce-169847e08522)


# HeatMap:

![image](https://github.com/Niranjanasuresh2003/Ex-08-Data-Visualization_1/assets/129851738/ae6f061b-c3c3-4c57-a79a-a4c4f998f061)


# RESULT:
~~~

Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file.
~~~
