# Exno:1
Data Cleaning Process

## NAME : K.GOUTHAM
## REG NO: 212223110019

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
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df
```
![image](https://github.com/user-attachments/assets/4a1532b7-b0f2-4e12-8a4b-5e9c6b2182ed)

```
df.head(3)
df.tail(3)
```
![image](https://github.com/user-attachments/assets/f6fbb7ff-a98d-4a5a-ab65-14fbd4b1006a)
```
df.isnull().sum()
```
![image](https://github.com/user-attachments/assets/14cfe1db-7ea2-4df0-84a9-03257519fb9b)

```
df.dropna(how='any').shape
```
![image](https://github.com/user-attachments/assets/d48d4843-99dd-4db9-a696-75d1bae8bff9)
```
df.shape
```
![image](https://github.com/user-attachments/assets/529be02e-48ee-4029-89cf-7dc7dde4a307)
```
mn=df.TOTAL.mean()
mn
```
![image](https://github.com/user-attachments/assets/f4293443-705e-4624-b7f9-4b8eec3bb152)
```
df.TOTAL.fillna(mn,inplace=True)
df
```
![image](https://github.com/user-attachments/assets/b522e978-ab46-4d06-b957-96e3d2c7b943)

```
df.drop_duplicates(inplace=True)
df
```
![image](https://github.com/user-attachments/assets/c7773e26-fa9e-49e9-bbd8-bb1885710d71)
```
df.duplicated()
```
![image](https://github.com/user-attachments/assets/1b670939-90ee-43bd-9770-09ebf876944d)
```
df['DOB']
```
![image](https://github.com/user-attachments/assets/492d20b1-97fc-45e0-9d03-3154afa04c7e)
```
df['DOB'] = pd.to_datetime(df['DOB'], format='%Y-%m-%d',errors='coerce')
df['DOB']
```
![image](https://github.com/user-attachments/assets/bb6fa6d5-cdc6-4483-9595-4f3969f79eeb)

```
import seaborn as sns
sns.heatmap(df.isnull(),yticklabels=False,annot=True)
```
![image](https://github.com/user-attachments/assets/7f3a1ee5-1add-4b43-ac84-fe3087489fd7)
```
import pandas as pd
import seaborn as sns
import numpy as np
```
```
age = [1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af= pd.DataFrame(age)
af
```
![image](https://github.com/user-attachments/assets/817289cd-7094-4482-a966-507efd9264ab)

```
sns.boxplot(data=af)
```
![image](https://github.com/user-attachments/assets/1a24bdfd-e213-453a-b000-e15ae8f07bf8)
```
sns.scatterplot(data=af)
```
![image](https://github.com/user-attachments/assets/58087a64-a227-4d4e-b079-f54f8d6a413a)
```
q1=af.quantile(0.25)
q3=af.quantile(0.75)
iqr=q3-q1
iqr
```
![image](https://github.com/user-attachments/assets/0f93e53c-339b-46e9-a50d-d22784bb5092)
```
Q1 = np.quantile(af, 0.25)
Q3 = np.quantile(af, 0.75)
IQR = Q3 - Q1
IQR
```
![image](https://github.com/user-attachments/assets/0c1b8cb4-2cbb-4850-8ec0-04f0dcba1f0c)
```
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR
```
```
lower_bound
```
![image](https://github.com/user-attachments/assets/544b433d-d83b-4aaa-a6f8-6db8eb565e8e)

```
upper_bound
```
![image](https://github.com/user-attachments/assets/7a67d177-54d3-4f48-ba50-35a731509a41)

```
outliers = [x for x in age if x < lower_bound or x > upper_bound]
```
```
print("Q1:",Q1)
print("Q3:",Q3)
print("IQR:",IQR)
print("Lower Bound:",lower_bound)
print("Upper Bound:",upper_bound)
print("Outliers:",outliers)
```
![image](https://github.com/user-attachments/assets/c44ee4d4-81fd-4116-b523-743392668536)
```
af=af[((af >= lower_bound)&(af <= upper_bound))]
af
```
![image](https://github.com/user-attachments/assets/4ce40069-01f3-4af1-9421-0b8e37391836)
```
af.dropna()
```
![image](https://github.com/user-attachments/assets/586550a0-024b-40af-8541-70a82ed76c5d)
```
sns.boxplot(data=af)
```
![image](https://github.com/user-attachments/assets/5914a2a0-934b-4d53-a9ce-0e9b6723bf9f)
```
data = [1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
mean = np.mean(data)
std = np.std(data)
print('mean of the dataset is',mean)
print('std.deviation is',std)
```
![image](https://github.com/user-attachments/assets/ffa84e59-6d62-4b56-8afd-aa8a7e29200a)
```
threshold = 3
outlier = []
for i in data:
  z_score = (i-mean)/std
  if np.abs(z_score) > threshold:
    outlier.append(i)
print('outlier in dataset is',outlier)
```
![image](https://github.com/user-attachments/assets/4221e2c9-1f5f-4438-a68f-bfd7d6a8d4d2)
```
import pandas as pd
import numpy as np
import seaborn as sns
import pandas as pd
from scipy import stats
```
```
z=np.abs(stats.zscore(df))
print(df[z['weight']>3])
```
![image](https://github.com/user-attachments/assets/269e5292-b43d-46f3-ad5e-d905b1c95543)

# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
