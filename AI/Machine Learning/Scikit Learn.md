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
y_preds = clf.predict(X_test) # returns the prediction
y_preds = clf.predict_proba(X_test) # returns the probability of the predictions
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
***
# Handling missing values
to confirm missing values
```python
df.isna().sum()
```

to drop samples with no targets
```python
df.dropna(subset=['target'], inplace=True)
```
## Using `scikit-learn`'s `SimpleImputer`
```python
# creating simpleImputer for each type of column
categ_imputer = SimpleImputer(strategy='constant', fill_value='missing')
door_imputer = SimpleImputer(strategy='constant', fill_value=4)
num_imputer = SimpleImputer(strategy='mean')

# define the necessary columns
categ_columns=['Make', 'Colour']
door_columns=["Doors"]
num_columns=['Odometer']

# Define the ColumnTransformer
from sklearn.compose import ColumnTransformer
imputers = ColumnTransformer([
	("categ_imputer", categ_imputer, categ_columns),
	("door_imputer", door_imputer, door_columns),
	("num_imputer", num_imputer, num_columns)
])

# Apply the Transformation
filled_X = imputers.fit_transform(X)
```
***
# Choosing the Right Estimator
![[Scikit Learn-1756181811378.png]]

1. Terminology
	- Estimator = ML model/algorithm 
	- Classifier (clf) = estimator for classification
	- Regressor = estimator for regression

2. Problem Types
	- Classification: predicts a class/label
	- Regression: predicts a quantity

## ==Note==
==If you have **Structured data** -> Use ensemble methods==
==If you have **un-structured data** -> Use deep learning and transfer learning methods==

## The Common flow
```python
# Imports
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import Ridge

# set the seed
np.random.seed(42)

# prepare the dataset
X = housing_df.drop("target", axis=1)
y = housing_df['target']

# split into training and testing dataset
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Instantiate and fit the model
model = Ridge()
model.fit(X_train, y_train)

# score it
model.score(X_test, y_test)
```

***
# **Classification Model Evaluation Metrics**
## Model Evaluation: Score vs Cross-Validation
## 1. `.score()` Method
- Every estimator in **scikit-learn** has a `.score()` method.
- **Default metrics**:
  - Regression → Coefficient of Determination (R²).
  - Classification → Mean Accuracy.

`.score()` is useful for a quick check, but not always reliable.
## 2. Why Go Beyond `.score()`?
- `.score()` only evaluates on **one train/test split**.
- Risk: “lucky split” → test data might make the model look better than it really is.
- Solution: **Cross-validation**, which tests the model on multiple splits.
## 3. Cross-Validation
### What it is
- Cross-validation = split data into **K folds** (subsets).
- For each fold:
  1. Use fold as **test set**.
  2. Train model on the remaining folds.
  3. Record the score.
- Repeat K times → gives **K different scores**.

### Example: 5-Fold CV
- Split data into 5 subsets.
- Train & evaluate 5 different models.
- Each data point gets to be in **test set exactly once**.

## 4. `cross_val_score` in scikit-learn
```python
from sklearn.model_selection import cross_val_score
scores = cross_val_score(clf, X, y, cv=5)
print(scores)        # array of 5 scores
print(scores.mean()) # average score
```

***
# ROC & AUC
# Model Evaluation: Accuracy vs ROC-AUC

## Why not just Accuracy?
- Accuracy doesn’t always reflect how good a classifier is, especially on **imbalanced datasets**.  
- Example: if 95% of patients don’t have heart disease, a dumb model predicting *“always 0”* gets 95% accuracy — but is useless.

- **ROC curve (Receiver Operating Characteristic):** plots  
  - **True Positive Rate (TPR)** = Recall = Sensitivity = `TP / (TP + FN)`  
  vs  
  - **False Positive Rate (FPR)** = `FP / (FP + TN)`  
- **AUC (Area Under Curve):** scalar summary of the ROC curve.  
  - Closer to **1.0 → great model**  
  - ~0.5 → random guessing  

---
## Confusion Matrix Terms
- **TP (True Positive):** Model says "1", truth is "1"  
- **FP (False Positive):** Model says "1", truth is "0"  
- **TN (True Negative):** Model says "0", truth is "0"  
- **FN (False Negative):** Model says "0", truth is "1"  

---
## Scikit-learn Example

```python
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import roc_curve, auc
import matplotlib.pyplot as plt

# Train/test split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Train model
clf = RandomForestClassifier()
clf.fit(X_train, y_train)

# Predict probabilities (only positive class column = [:, 1])
y_probs = clf.predict_proba(X_test)[:, 1]

# ROC values
fpr, tpr, thresholds = roc_curve(y_test, y_probs)
roc_auc = auc(fpr, tpr)

# Plot
plt.plot(fpr, tpr, label=f"ROC curve (AUC = {roc_auc:.2f})")
plt.plot([0,1], [0,1], "k--")  # random guessing line
plt.xlabel("False Positive Rate")
plt.ylabel("True Positive Rate")
plt.title("ROC Curve")
plt.legend()
plt.show()
```

# ROC Curve and AUC Notes

## 1. ROC Curve Basics
- **ROC** stands for **Receiver Operating Characteristic**.
- It plots the **True Positive Rate (TPR)** against the **False Positive Rate (FPR)** at different thresholds.
- Provides a visual way to evaluate a classification model’s performance.

### Key terms:
- **TPR (Recall / Sensitivity)** = TP / (TP + FN)  
- **FPR** = FP / (FP + TN)
## 2. Creating an ROC Curve Plot
We typically use `matplotlib` to plot ROC curves.

```python
import matplotlib.pyplot as plt

def plot_roc_curve(fpr, tpr):
    """Plots an ROC curve given FPR and TPR of a model."""
    plt.plot(fpr, tpr, color="orange", label="ROC Curve")
    plt.plot([0, 1], [0, 1], color="darkblue", linestyle="--", label="Guessing")
    plt.xlabel("False Positive Rate (FPR)")
    plt.ylabel("True Positive Rate (TPR)")
    plt.title("Receiver Operating Characteristic (ROC)")
    plt.legend()
    plt.show()
```

## 3. AUC (Area under the curve)
- AUC measures the area under the ROC curve
- value ranges:
	- 1.0 -> Perfect model
	- 0.5 -> Random guessing
	- <0.5 -> worse than random

```python
from sklearn.metrics import roc_curve, roc_auc_score

fpr, tpr, thresholds = roc_curve(y_test, y_probs)
plot_roc_curve(fpr, tpr)

auc_score = roc_auc_score(y_test, y_probs)
print("AUC Score:", auc_score)
```

# Confusion Matrix
## 1. What is a Confusion Matrix?
- A **confusion matrix** is a quick way to compare a model’s **predicted labels** vs. the **actual labels**.
- Shows where the model is getting things right and where it’s **getting confused**.
- Structure:
  - Rows → **Actual labels**
  - Columns → **Predicted labels**
## 2. Creating a Confusion Matrix
Using **scikit-learn**:

```python
from sklearn.metrics import confusion_matrix

y_preds = model.predict(X_test)
cm = confusion_matrix(y_test, y_preds)
print(cm)
```

The Output would look something like
```python
[[TN, FP],
 [FN, TP]]
```
where,
- **TN (True Negatives)** → Correctly predicted 0s
- **TP (True Positives)** → Correctly predicted 1s
- **FP (False Positives)** → Predicted 1 when actual = 0
- **FN (False Negatives)** → Predicted 0 when actual = 1

## 3. Visualization 
```python
# From estimatore
from sklearn.metrics import ConfusionMatrixDisplay
ConfusionMatrixDisplay.from_estimator(clf, X_test, y_test)

# From Predictions
ConfusionMatrixDisplay.from_predictions(y_test, y_pred)

```
- it lets us see where our model struggles
	- Too many false positives? Model is over-predicting positives
	- Too many false negatives? Model is missing real positives
- Forms the basis for metrics like:
	- **Accuracy** = (TP + TN) / Total
	- **Precision** = TP / (TP + FP)
	- **Recall** = TP / (TP + FN)
	- **F1 Score** = Harmonic mean of Precision & Recall

# Notes: Classification Report (Scikit-learn)
- A **classification report** is a **summary of multiple evaluation metrics** for a classification model.  
- Helps when accuracy alone is misleading (e.g., in imbalanced datasets).
### In Code
```python
from sklearn.metrics import classification_report

y_pred = clf.predict(X_test)
print(classification_report(y_test, y_pred))
```

### Components of the Report
For each class (e.g., `0 = No disease`, `1 = Disease`), you get:
1. **Precision**
    - Proportion of predicted positives that were actually positive.
    - `Precision = TP / (TP + FP)`
    - High precision = few false positives.
2. **Recall (Sensitivity / True Positive Rate)**
    - Proportion of actual positives correctly identified.
    - `Recall = TP / (TP + FN)`
    - High recall = few false negatives.
3. **F1 Score**
    - Harmonic mean of precision & recall.
    - Balances the two metrics.
    - `F1 = 2 * (Precision * Recall) / (Precision + Recall)`
4. **Support**
    - Number of samples in each class.
    - Shows how many examples each metric was calculated on.
### Aggregated Metrics
- **Accuracy**: `(TP + TN) / Total` (overall correct predictions).
- **Macro Average**: Average of precision/recall/F1 across classes, **ignores class imbalance**.
- **Weighted Average**: Average of precision/recall/F1 weighted by support, **accounts for class imbalance**.

### Why Not Just Accuracy?
- **Accuracy can be misleading in imbalanced datasets.**  
    Example:
    - 10,000 samples, only **1 positive case**.
    - Model predicts **all 0**.
    - Accuracy = **99.99%**, but recall for class `1` = **0** (missed all positives).
    - Precision for class `1` = **0** too.
    - Report reveals the **failure** that accuracy hides.

***
# Regression model Evaluation Techniques
When evaluating regression models, we measure how well a model predicts continuous target values. Scikit-learn provides a variety of metrics for this purpose. Some of the most commonly used regression metrics include:

- **Max Error**  
- **Mean Absolute Error (MAE)**  
- **Mean Squared Error (MSE)**  
- **Mean Squared Log Error (MSLE)**  
- **R² Score (Coefficient of Determination)**  
***
### 1. R² Score (Coefficient of Determination)

The R² score measures the proportion of variance in the dependent variable that can be predicted from the independent variables.  

It compares your model predictions to the mean of the targets. Values can range from minus infinity (a very poor model predicting wild things) to 1 (a very accurate model). If the model only predicts the mean of your targets, its R<sup>2</sup> value would be 0.

- Perfect prediction → **R² = 1.0**  
- Predicting only the mean → **R² = 0.0**  
- Poor predictions can even result in **negative R²** values  

```python
from sklearn.metrics import r2_score
import numpy as np

# Assume y_test is the true target values
y_test_mean = np.full_like(y_test, y_test.mean())

# R² score if model predicts just the mean
r2_zero = r2_score(y_test, y_test_mean)
print("R² when predicting the mean:", r2_zero)

# R² score for perfect prediction
r2_perfect = r2_score(y_test, y_test)
print("R² for perfect prediction:", r2_perfect)
```
### 2. Mean Absolute Error (MAE)
MAE is the average of absolute differences between predictions and actual values. It gives us an idea of how wrong the predictions are in average.
$$abs(\ mean(\ predition - actual\ values)\ )$$
- Lower MAE → Better model performance
- Easy to interpret in the same units as the target variable

### 3. Mean Squared Error (MSE)

The **MSE** measures the average of squared differences between predicted and actual values:
- It amplifies the outliers in prediction and actual values
$$square(\ (mean(prediction - actual\ value))\ )$$
- Penalizes larger errors more than MAE
- Widely used in regression tasks

***
# Why Use Cross-Validation (CV)?
## Problem with Single Train/Test Split
- If you just split data once into train/test:
    - Model might look **good** (if test set was easy)
    - Model might look **bad** (if test set was hard)
    - Performance estimate is **unstable & biased**
## Cross-Validation Idea
- **Split dataset multiple times** into train/test folds.
- Train & evaluate the model on each split.
- Average results across folds → **more reliable estimate** of model’s performance.

```python
from sklearn.model_selection import cross_val_score
from sklearn.ensemble import RandomForestClassifier

# model
clf = RandomForestClassifier()

# 5-fold CV with accuracy
scores = cross_val_score(clf, X, y, cv=5, scoring="accuracy")

print("Fold scores:", scores)
print("Mean CV score:", scores.mean())

```

***
# Improving the Model

## 1. Baseline
- **First predictions** = *baseline predictions*  
- **First model** = *baseline model*  
- Always compare improvements against your baseline.  

---

## 2. From a Data Perspective
- **More data** → more examples, more patterns to learn.  
- **Better data** → richer features per sample (more informative columns, fewer errors/noise).  

Think: quantity vs. quality.

---

## 3. From a Model Perspective
- **Better model?**  
  - Start simple (fast, easy to interpret).  
  - Move to more complex (ensembles, boosting, deep models).  
- **Improve the current model?**  
  - Keep the same algorithm, but tune its **hyperparameters**.

---

## 4. Parameters vs. Hyperparameters
- **Parameters** → learned by the model from the data (e.g., tree splits, regression coefficients).  
- **Hyperparameters** → chosen/set by you before training (e.g., `n_estimators` in RandomForest, learning rate in boosting).  

Note: Scikit-learn docs list them as "parameters" because they’re function arguments, but conceptually they are **hyperparameters**.

---

## 5. Why Hyperparameter Tuning?
Analogy: cooking  
- Data = ingredients  
- Model = oven  
- Hyperparameters = oven settings (temperature, time)  
- Baseline = roast chicken at 180°C for 1 hour  
- Tuning = try 200°C instead → better dish  

---

## 6. Ways to Tune Hyperparameters
1. **Manual search** → adjust by hand, guided by intuition.  
2. **RandomizedSearchCV** → try random combos of hyperparameters.  
3. **GridSearchCV** → exhaustively try all specified combinations.  

---
## Tuning Hyperparameters
## Why a Validation Set?
- Previously: **Train** → model learns patterns, **Test** → model evaluated.  
- Now: add a **Validation set**.  
  - Train set (e.g., 70%) → model learns.  
  - Validation set (e.g., 10–15%) → tune hyperparameters.  
  - Test set (e.g., 10–15%) → final evaluation.  

**Analogy**:  
- Train set = studying course materials.  
- Validation set = practice exam (find weaknesses, adjust strategy).  
- Test set = final exam.

---
## Parameters to Adjust (RandomForest example)
Common hyperparameters to try:  
- `n_estimators` (number of trees).  
- `max_depth` (depth of trees).  
- `max_features` (features considered for each split).  
- `min_samples_split` (min samples to split a node).  
- `min_samples_leaf` (min samples per leaf node).

---

## Process
1. **Baseline model**  
   - Instantiate model with default hyperparameters.  
   - Train on training set.  
   - Evaluate on validation set.  

2. **Adjust hyperparameters manually**  
   - Example: increase `n_estimators` from 10 → 100.  
   - Train and evaluate again on validation set.  
   - Compare results (accuracy, precision, recall, f1).  

3. **Iterate**  
   - Try changing other parameters (e.g., `max_depth = 10`).  
   - Record metrics for each configuration.  

---
1. Manual Tuning hyperparameters by hand
2. Using RandomizedSearchCV
3. Using GridSearchCV

## Using RandomizedSearchCV
```python
# 5.2 Hyperparameter tuning with RandomizedSearchCV

from sklearn.model_selection import RandomizedSearchCV, train_test_split
from sklearn.ensemble import RandomForestClassifier

# Define the hyperparameter grid
param_grid = {
    'n_estimators': [10, 100, 500, 1000, 1200],
    'max_depth': [None, 5, 10],
    'min_samples_split': [2, 4, 6],
    'min_samples_leaf': [1, 2, 4],
    'max_features': ['auto', 'sqrt', 'log2']
}

# Split data into X (features) and y (target)
X = heart_disease_shuffled.drop(columns='Target')
y = heart_disease_shuffled['Target']

# Train-test split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Instantiate Random Forest Classifier
clf = RandomForestClassifier(random_state=42)

# Set up RandomizedSearchCV
rs_clf = RandomizedSearchCV(
    estimator=clf,
    param_distributions=param_grid,
    n_iter=10,          # number of parameter combinations to try
    cv=5,               # 5-fold cross-validation
    verbose=2,
    random_state=42,
    n_jobs=-1           # use all cores
)

# Fit RandomizedSearchCV on training data
rs_clf.fit(X_train, y_train)

# Best hyperparameters found
print("Best Hyperparameters:", rs_clf.best_params_)

# Make predictions on test set using best hyperparameters
y_pred = rs_clf.predict(X_test)

# Evaluate predictions
rs_matrix = evaluate(y_test, y_pred)  # use the evaluation function you created earlier
print(rs_matrix)
```
## Using GridSearchCV
```python
# 5.3 Hyperparameter tuning with GridSearchCV

from sklearn.model_selection import GridSearchCV, train_test_split
from sklearn.ensemble import RandomForestClassifier

# Refined hyperparameter grid (based on RandomizedSearchCV best params)
grid2 = {
    'n_estimators': [200, 500],
    'max_depth': [None],
    'min_samples_split': [6],
    'min_samples_leaf': [1, 2],
    'max_features': ['auto', 'sqrt']
}

# Split data into X (features) and y (target)
X = heart_disease_shuffled.drop(columns='Target')
y = heart_disease_shuffled['Target']

# Train-test split (same as before for consistency)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Instantiate Random Forest Classifier
clf = RandomForestClassifier(random_state=42)

# Set up GridSearchCV
gs_clf = GridSearchCV(
    estimator=clf,
    param_grid=grid2,
    cv=5,               # 5-fold cross-validation
    verbose=2,
    n_jobs=-1           # use all cores
)

# Fit GridSearchCV on training data
gs_clf.fit(X_train, y_train)

# Best hyperparameters found
print("Best Hyperparameters:", gs_clf.best_params_)

# Make predictions on test set using best hyperparameters
y_pred = gs_clf.predict(X_test)

# Evaluate predictions
gs_matrix = evaluate(y_test, y_pred)  # use the evaluation function you created earlier
print(gs_matrix)

# Optional: Compare metrics of all models
import pandas as pd
import matplotlib.pyplot as plt

compare_metrics = pd.DataFrame({
    'Baseline': baseline_metrics,
    'CLF2': clf2_metrics,
    'Random Search': rs_matrix,
    'Grid Search': gs_matrix
})

compare_metrics.plot.bar(figsize=(10,6))
plt.show()

```
## The Recommended workflow
- **Manual tuning:** Start with a few educated guesses.
- **RandomizedSearchCV:** Explore a large hyperparameter space quickly.
- **GridSearchCV:** Refine search around the best parameters found by RandomizedSearchCV for fine-tuning.

***
# Saving The Model
# 6. Saving and Loading Trained Machine Learning Models

Once we have a trained model that we’re happy with, we might want to save it to share with colleagues, deploy in an application, or simply avoid retraining. There are two common ways to do this in Python:

1. **Pickle module**
2. **Joblib module** (better for large models)

---

## **1. Saving a Model with Pickle**

```python
import pickle

# Let's say clf is your trained model (e.g., GridSearchCV + RandomForestClassifier)
filename = "random_forest_model1.pkl"

# Open a file in write-binary mode and save the model
with open(filename, 'wb') as file:
    pickle.dump(clf, file)
```

## Loading the saved model

```python
# Load the model from the file
with open("random_forest_model1.pkl", 'rb') as file:
    loaded_model = pickle.load(file)
```

## Using loaded model for predictions
```python
# Assuming X_test and y_test are available
y_preds = loaded_model.predict(X_test)

# Evaluate predictions (use your evaluation function)
metrics = evaluate_preds(y_test, y_preds)
print(metrics)
```

***
# Saving and Loading Models with Joblib
## **1. Saving a Model with Joblib**

```python
from joblib import dump, load

# Save the trained model
dump(clf, "random_forest_model1.joblib")
```

## 2. Loading the joblib model

```python
# Load the saved model
loaded_joblib_model = load("random_forest_model1.joblib")
```

## 3. Making predictions with loaded model

```python
# Make predictions on the test set
joblib_y_preds = loaded_joblib_model.predict(X_test)

# Evaluate predictions
joblib_metrics = evaluate_preds(y_test, joblib_y_preds)
print(joblib_metrics)

```

## **4. When to Use Joblib vs Pickle**
- **Pickle**: Works for general Python objects and smaller models.
- **Joblib**: Recommended for **large models** or models containing large NumPy arrays (like scikit-learn estimators) because it's more efficient.

***
# Pipeline
pipe lining combines different steps
```python
categorical_features = ["make", "color"]
numeric_features = ["odometer"]
door_feature = ["doors"]  # optional, can be numeric

categorical_transformer = Pipeline(steps=[
    ("imputer", SimpleImputer(strategy="constant", fill_value="missing")),
    ("onehot", OneHotEncoder(handle_unknown="ignore"))
])

door_transformer = Pipeline(steps=[
    ("imputer", SimpleImputer(strategy="constant", fill_value=4))
])

numeric_transformer = Pipeline(steps=[
    ("imputer", SimpleImputer(strategy="mean"))
])

from sklearn.compose import ColumnTransformer

preprocessor = ColumnTransformer(
    transformers=[
        ("cat", categorical_transformer, categorical_features),
        ("door", door_transformer, door_feature),
        ("num", numeric_transformer, numeric_features)
    ]
)

model = Pipeline(steps=[
    ("preprocessor", preprocessor),
    ("regressor", RandomForestRegressor())
])

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

model.fit(X_train, y_train)
y_pred = model.predict(X_test)

```