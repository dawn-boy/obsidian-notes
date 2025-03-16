```python

#to read .csv files
import pandas as pd
import numpy as np

df = pd.read_csv(fileName)

#to display the dataFrames
df.head(n)
df.tail(n)
df.info()

#concating data with existing dataFrame
newVals = pd.DataFrame(
		   {"colName":["val1",'val2']}
		   )
df = pd.concat([df,newVals],ignore_index = True) #ignore_index pads with the existing index instead of starting from 0

#to calculate the missing percentage
missingPercentage = df.isnull().mean() * 100

#to iterate through the columns
for col in df.select_dtypes(include=[np.number,object]).columns: #np.number is for numerical data and object is for categorical data
	print(df[col])

#mean,meadian,mode
df[col].mean()
df[col].median()
df[col].mode()[0]
```
## imputation
filling up the missing data in the dataset 
```python
#performing mean imputation for numerical data
for col in df.select_dtypes(include = [np.number]).columns:
	if missingPercentage[col] > 10:
		df[col].fillna(df[col].mean(),inplace = True)

#performing modal imputation for catogorical data
for col in df.select_dtypes(include = [object]).columns:
	if missingPercentage[col] > 10:
		df[col].fillna(df[col].mode()[0],inplace = True)

# KNN imputation
# non NaN values should be present before imputing
from sklearn.impute import KNNImputer
imputer = KNNImputer(n_neighbors = 2)
imputed = pd.DataFrame(
		imputer.fit_transform(
			df.select_dtypes(include = [np.number])
		) 
		columns = df.select_dtypes(include = [np.number]).columns
)
df.update(imputed)

#dropping columns with more than 10% values
df_dropped_cols = df.dropna(axis=1, thresh=len(df) * 0.9)
# axis 0 -> selects row
# axis 1 -> selects column
# thresh -> specifies the minimum value needed in the field, if this minimum value is not satisfied then the column is deleted. len(df) gives the total number of rows. len(df) * 0.9 says 90% of len(df), so we need a minimum data fill of 90% in a column for it be not deleted.
```
## dropping
```python

# dropping columns with outlies
from scipy.stats import zscore
numData = df.select_dtypes(include=[np.number])

# applying the zscore function to each field withing numData dataframe
z = numData.apply(zscore)

# df[condition] is used for filtering, here we are converting all the data to its absolute value with a condition less than 3 for all columns (axis = 1)
filteredDF = df[(np.abs(z) < 3).all(axis=1)]
print(filteredDF)

#to delete duplicate rows
df_no_dupes = df.drop_duplicates()
# if we need to delete duplicates from only half of the columns
df_no_dupes = df.drop_duplicates(
				subset = df.columns[:int(len(df.columns)*0.5)]
)
```
## preprocessing
```python
# fit transfrom
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
#[''] gives a serial type(one dimensional pd datatype)
#[['']] gives a frame type(two dimensional pd datatypek)
df['Age'] = scaler.fit_transform(df[['Age']])

# to binarize the data, if the value is above the threshold, set it to 1, else set it to 0

from sklearn.preprocessing import Binarize
binarize = Binarize(threshold = 50)
df['col'] = binarize.fit_transform(df[['col']])

# One Hot encoder
# it assigns a numerical value to each categorical value in the column

from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder(sparse_output=False)
encoded_columns = encoder.fit_transform(df[['col']])
encoded_df = pd.DataFrame(
			  encoded_columns,
			  columns=encoder.get_feature_names_out(['col'])
			  )

df = df.join(encoded_df)
```
## univariate
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

data = {
		...
}
df = pd.DataFrame(data)


# customize the plot
plt.title('col dis')
plt.xlabel("Col")
plt.ylabel("Count")
plt.show()

# Bar Plot
sns.countplot(
	x='colName',
	data=df
)
# Violin chart
sns.violinplot(
	x='Gender',
	y='Age',
	data=df
)

# Histogram
sns.histplot(
	df['Age'],
	kde=True, # gives the trend line over the blocks,
	bins=5 # number of blocks
)

# Pie chart
depts_counts = df['Departments']
plt.pie(
	dept_counts,
	labels=dept_counts.index,
	autopct = '%1.1f',
	startangle=90
)


```
