# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output

```
REG NO : 212224230290
DATE   : 13-03-2025
```

```
import pandas as pd
neo=pd.read_csv("SAMPLEIDS.csv")
neo
```
![Screenshot 2025-03-13 102644](https://github.com/user-attachments/assets/775dcbeb-2d7a-49cd-b781-8a0de6313153)

```
neo.isnull().sum()
```
![Screenshot 2025-03-13 102814](https://github.com/user-attachments/assets/9f71c943-c80d-4370-a6e7-31ef652751eb)

```
neo.isnull().any()
```
![Screenshot 2025-03-13 102859](https://github.com/user-attachments/assets/213e0475-083e-426f-b4bd-df3e20447ef3)

```
neo.dropna()
```
![Screenshot 2025-03-13 103131](https://github.com/user-attachments/assets/4c1da22b-e348-4998-ba96-4208f264c389)

```
neo.fillna(0)
```
![Screenshot 2025-03-13 103235](https://github.com/user-attachments/assets/3d5227ee-7215-424b-a4a2-72fd45ca0730)

```
neo.fillna(method = 'ffill')
```
![Screenshot 2025-03-13 103321](https://github.com/user-attachments/assets/6832bbc5-8290-4a61-9df4-e3b0d62101a2)

```
neo.fillna(method = 'bfill')
```
![Screenshot 2025-03-13 103419](https://github.com/user-attachments/assets/d18444e4-8d08-47c6-b1a0-e4e80a12a8d3)

```
neo_dropped = neo.dropna()
neo_dropped
```
![Screenshot 2025-03-13 103501](https://github.com/user-attachments/assets/2d587cf0-d3f3-48f7-a4dc-b2002ae59d0a)

```
neo.fillna({'GENDER':'MALE','NAME':'SRI','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![Screenshot 2025-03-13 103600](https://github.com/user-attachments/assets/ca8d6ee6-ff88-426d-b2a4-59f56736f683)

```
neo=pd.read_csv('iris.csv')
neo
```
![Screenshot 2025-03-13 103652](https://github.com/user-attachments/assets/a94bbf41-f658-48c3-8000-9f9d7ebf6384)

```
neo.describe()
```
![Screenshot 2025-03-13 103725](https://github.com/user-attachments/assets/a93cce39-7c8b-43f5-9548-fb63aa1c53cf)

```
import seaborn as sns
sns.boxplot(x='sepal_width',data=neo)
```
![Screenshot 2025-03-13 103810](https://github.com/user-attachments/assets/b4f0f21b-54ac-452d-96e0-4f08d27e20c2)

```
q1=neo.sepal_width.quantile(0.25)
q3=neo.sepal_width.quantile(0.75)
iqr=q3-q1
print(iqr)
```
![Screenshot 2025-03-13 103845](https://github.com/user-attachments/assets/52744d60-6c3a-43a0-b2e7-6fa9be197718)

```
rid=neo[((neo.sepal_width<(q1-1.5*iqr))|(neo.sepal_width>(q3+1.5*iqr)))]
rid['sepal_width']
```
![Screenshot 2025-03-13 103922](https://github.com/user-attachments/assets/3b391cce-4d9f-46ea-8c3b-fa4ddeaf8d29)

```
rid=neo[~((neo.sepal_width<(q1-1.5*iqr))|(neo.sepal_width>(q3+1.5*iqr)))]
rid['sepal_width']
```
![Screenshot 2025-03-13 104008](https://github.com/user-attachments/assets/435daa4a-7120-41f2-89cf-dae81a62c0c3)

```
sns.boxplot(x='sepal_width',data=rid)
```
![Screenshot 2025-03-13 104055](https://github.com/user-attachments/assets/39298241-7a9b-4494-b353-c5e3de15f16e)

```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats

dataset=pd.read_csv("heights.csv")
dataset
```
![Screenshot 2025-03-13 104233](https://github.com/user-attachments/assets/cbd1cd85-72ac-4db3-bf7b-fab2f2a24812)

```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)

iqr = q3-q1
iqr
```
![Screenshot 2025-03-13 104435](https://github.com/user-attachments/assets/4527872c-1b45-4129-9284-50e2e92ebd7e)

```
low = q1 - 1.5*iqr
low
```
![Screenshot 2025-03-13 104523](https://github.com/user-attachments/assets/badd559f-d0e4-460e-aba9-bd2f1b0f40c3)

```
high = q3 + 1.5*iqr
high
```
![Screenshot 2025-03-13 104606](https://github.com/user-attachments/assets/909ed37a-69ab-4fba-9a58-48d7d84ed542)

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![Screenshot 2025-03-13 104650](https://github.com/user-attachments/assets/40d790e5-758b-480f-b839-4c53d755290c)

```
z = np.abs(stats.zscore(df['height']))
z
```
![Screenshot 2025-03-13 104728](https://github.com/user-attachments/assets/8010f0b4-4f56-4a3e-9f97-f2948ee36b71)

```
df1 = df[z<3]
df1
```
![Screenshot 2025-03-13 104814](https://github.com/user-attachments/assets/d08baa51-7b5c-4ccc-8d0f-22a5bea61d6e)


# Result
          Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
