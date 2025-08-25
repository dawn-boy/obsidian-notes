# Using Classification
## 1. Get the Data Ready
```python
import pandas as pd

heart_disease = pd.read_csv("data/heart-disease.csv")
X = heart_disease.drop("target", axis=1)  # features
y = heart_disease["target"]               # labels
```
## 2. Choose the Model & Hyperparameters
```python
from sklearn.ensemble import RandomForestClassifier

clf = RandomForestClassifier(n_estimators=100)  # default = 100
```
## 3. Fit the Model
```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
clf.fit(X_train, y_train)
```
## 4. Make Predictions
```python
y_preds = clf.predict(X_test)
```
## 5. Evaluate the Model
```python
clf.score(X_train, y_train)  # training accuracy
clf.score(X_test, y_test)    # test accuracy

from sklearn.metrics import classification_report, confusion_matrix, accuracy_score

print(classification_report(y_test, y_preds))
print(confusion_matrix(y_test, y_preds))
print(accuracy_score(y_test, y_preds))
```
## 6. Improve the Model
```python
for i in range(10, 110, 10):
    clf = RandomForestClassifier(n_estimators=i, random_state=42)
    clf.fit(X_train, y_train)
    print(f"{i} trees → Test Accuracy: {clf.score(X_test, y_test):.2f}")
```
## 7. Save & Load Model
```python
import pickle

# Save
with open("random_forest_model.pkl", "wb") as f:
    pickle.dump(clf, f)

# Load
with open("random_forest_model.pkl", "rb") as f:
    loaded_model = pickle.load(f)

loaded_model.score(X_test, y_test)
```

***
# Using Regression
## Reading the data
```python
df = pd.read_csv('car-sales.csv')
```
![[Scikit Learn-1756013880844.png]]
## Splitting the dataset to `Features` and `Labels`
```python
X = df.drop('Price', axis=1)
y = df['Price']
```
## Pre-processing the categorical features
```python
from sklearn.preprocessing import OneHotEncoder
from sklearn.compose import ColumnTransformer

categorical_features = ['Make', 'Colour', 'Doors']
one_hot = OneHotEncoder()

transformer = ColumnTransformer(
			[('one_hot', one_hot, categorical_features)],
			remainder='passthrough')

transformed_X = transformer.fit_transform(X)
feature_names = transformer.get_feature_names_out()

transformed_df = pd.DataFrame(transformed_X, columns=feature_names)
```
***
# Feature Scaling
## What is Feature Scaling
- Its the process of putting all numerical features on a similar scale
- Without scaling, the model may give more importance to the features with larger numeric values
## Two types of feature scaling
1. Normalization (Min-Max Scaling)
- Re-scales values to a range of **[0,1]**
$$X_{norm} = \frac{X- X_{min}}{X_{max} - X_{min}}$$
- Use when features need to be bounded. **Often used in neural networks**
```python
from sklearn.preprogramming import MinMaxScaler

scaler = MinMaxScaler()
X_scaled = scaler.fit_transform(X)
```

2. Standardization (Z-score Scaling)
- Transforms features to have
	- Mean = 0
	- Standard deviation = 1
$$X_{std} = \frac{X-\mu}{\sigma}$$
		where $\mu$ = mean, $\sigma$ = standard deviation
```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```
- Use when features have different distributions and we want to center and scale them. Often used in **linear regression, logistic regression, SVM, PCA, K-means**