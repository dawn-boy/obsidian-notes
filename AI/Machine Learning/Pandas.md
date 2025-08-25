Its used for data analysis and manipulation. It helps us organize, clean, filter and analyze data efficiently
## Series
A one-dimensional labeled array.
### Example
```python
s = pd.Series([10, 20, 30])
```
### Output
```python
0    10
1    20
2    30
dtype: int64
```
## Dataframe
![[Pandas-1754824486018.png]]
A Two-dimensional table made up of multiple series 
### Example
```python
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['Delhi', 'Mumbai', 'Bangalore']
}
df = pd.DataFrame(data)
```
### Output
```python
     Name  Age      City
0   Alice   25     Delhi
1     Bob   30    Mumbai
2  Charlie  35  Bangalore
```
## Importing/Exporting data
```python
# Import
pd.read_csv(Path)

# Export
df.to_csv(Path, index=False) 
# pandas automatically exports a index column, set it to false if not needed
```
***
# Operations on DataFrame
## There are two types of data
### Attributes (Returns info)
```python
df.dtypes 
df.columns
df.index
```
### Function (Perform actions)
```python
df.describe() #describes about the dataframe
df.info()
df.mean(numeric_only=True)j
df.sum()
df.head()
```
## Selecting and viewing 
```python
car_sales['Make'] #just gives back the Make col
car_sales[car_sales['Make'] == 'BMW'] # with a condition
```
## Data Manipulation
### Missing values
```python
car_sales_missing['Price'].fillna(value, inplace=True)
car_sales_missing.dropna()
```
### String operations 
```python
# Replace
car_sales['Price'] = car_sales['Price'].str.replace('[\$\,\.]', '').astype(int)
```
***
# Creating and Modifying columns
- Creating new columns
- Fill or calculate values in columns
- handling operation between columns
- drop unwanted columns
## 1. Creating new columns
```
df['new_col'] = <Series | List | Scaler | Computation>
```
## from a series
```python
name = pd.Series(['Jurassic', 'Avengers', 'Park'])
df['Name'] = name
```
- if there's a length mismatch, then `NaN` values are filled.
## from a python list
```python
name = [7.4,5,7,2,5,6,7]
df['Name'] = name
```
- if there's a length mismatch, then there's a `ValueError`
## from another column
```python
df['Price'] = (df['gas'] * 2.3) / df['fuel']
```
- performs row-level operation on the column
## from a single value
```python
df['number of wheels'] = 4
```

## 2. Filling missing values in new columns
```python
df['Seats'].fillna(5, inplace=True)
```

## 3. Dropping columns
```python
df = df.drop('ColName', axis=1)

# or inplace
df.drop('ColName', axis=1, inplace=True)
```
- `axis=1` for columns
***
# Sampling, Resetting index, and Applying functions
- Shuffle a DataFrame using `.sample()`
- Reset a DataFrame using `.reset_index()`
- Apply functions to DataFrame Columns using `.apply()`

## 1. Shuffling a DataFrame 
- Shuffling is useful for 
	- breaking potential order bias in your data
	- creating a train/test split more fairly
```python
# fraction, gives the whole 100% of the data
car_sales = car_sales.sample(frac=1)

# gives the 75% of the data in random order
car_sales = car_sales.sample(frac=0.75)
```

## 2. Resetting indexes 
- shuffling keeps the original index
```python
car_sales.reset_index(drop=True, inplace=True)
```

## 3. Applying functions to Columns 
```python
car_sales['Odometer KM'] = car_sales['Odometer KM'].apply(lambda x: x/1.6)
```

***
## To generate a date range
```python
pd.date_range('1/1/2000', periods=1000)
```
## To count the number of occurrence
```python
df['Doors'].count_values()
```
***
# Handling Missing values
Detect missing values
```python
df.isna().sum()
```

To Fill missing data
```python
# Fill categorical
df['col'].fillna('Missing', inplace=True)

# Fill numerical
df['col'].fillna(df['col'].mean(), inplace=True)

# Fill with most common value
df['col'].fillna(df['col'].mode()[0], inplace=True)
```
# Remove missing values
```python
df.dropna(subset=['Price'], inplace=True)
```