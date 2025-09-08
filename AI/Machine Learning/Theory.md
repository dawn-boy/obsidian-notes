# Coefficient of Determination (R²)

## 1. What it is
- Symbol: **R²**
- Name: **Coefficient of Determination**
- Default score used in **scikit-learn regressors** (`.score()`).
- Tells you **how well your regression model explains the variability of the target variable**.

---

## 2. Formula

$$R^2 = 1 - \frac{SS_{res}}{SS_{tot}}$$

Where:
- $(SS_{res} = \sum (y_i - \hat{y}_i)^2)$ → **Residual sum of squares** (error left after fitting).
- $(SS_{tot} = \sum (y_i - \bar{y})^2)$ → **Total sum of squares** (variation in the data from the mean).

---

## 3. Interpretation
- **R² = 1** → Perfect fit (model explains all variability in data).
- **R² = 0** → Model is as good as predicting the **mean** of y.
- **R² < 0** → Model is **worse than mean prediction** (very poor fit).
- Higher R² = better model (in terms of variance explained).

---

## 4. Example intuition
Suppose target = house prices.
- If R² = 0.85 → 85% of the variance in house prices is explained by your features (income, rooms, location, etc.).
- Remaining 15% = due to factors the model didn’t capture (noise, missing features, randomness).

---

## 5. Limitations
- **Only for regression**, not classification.
- **High R² ≠ always good model**:
  - You can overfit and still get high R².
  - Doesn’t account for number of features used.
- That’s why we sometimes use **Adjusted R²** (penalizes unnecessary features).

---

## 6. Quick Example in Python

```python
from sklearn.metrics import r2_score

y_true = [3, -0.5, 2, 7]
y_pred = [2.5, 0.0, 2, 8]

print("R²:", r2_score(y_true, y_pred))
```

***
# Decision Tree, Random Forest, and Ensemble Learning — Theory
## 1. Decision Tree

### Definition
A **Decision Tree** is a supervised learning algorithm used for both **classification** and **regression**.  
It predicts outcomes by splitting data into branches based on feature values.

### Key Ideas
- Works like a **flowchart**:
  - At each node → ask a question about a feature.  
  - Depending on the answer → go down a branch.  
  - Continue until a **leaf node** (prediction) is reached.  

### Example
- Predict whether someone will buy a computer:  
  - **Q1**: Age < 30? → Yes →  
    - **Q2**: Income > 50k? → Yes → **Buy**  
    - Otherwise → **Not Buy**  
  - Age ≥ 30 → different splits.

### Pros
- Easy to **interpret & visualize**.  
- Handles **numerical and categorical data**.  
- No need for feature scaling.  

### Cons
- **Overfitting** (memorizes training data).  
- **Instability** (small changes → very different tree).  
- Usually lower accuracy than ensembles.

---

## 2. Random Forest

### Definition
A **Random Forest** is an **ensemble method** that combines many decision trees.  

- Each tree is trained on:
  - A **random sample of data** (bootstrapping).  
  - A **random subset of features** at each split.  
- Final prediction:
  - **Classification** → Majority vote.  
  - **Regression** → Average prediction.  

### Why "Random"?
- Random data subsets = **Bagging (Bootstrap Aggregating)**.  
- Random feature subsets = prevents dominant features from biasing results.  

### Benefits
- **Reduces overfitting** (better generalization).  
- **Stable & robust** against noise.  
- Strong performance with minimal tuning.  
- Can measure **feature importance**.  

### Limitations
- Less interpretable than a single tree.  
- Larger models → more computation & memory.  

---

## 3. Ensemble Learning

### Definition
**Ensemble learning** combines predictions of multiple models to achieve better performance than individual models.

### Types
1. **Bagging**  
   - Train models on random subsets of data.  
   - Combine predictions (vote/average).  
   - Example: **Random Forest**.  

2. **Boosting**  
   - Train models sequentially, each one **fixes errors** of the previous.  
   - Examples: **XGBoost, AdaBoost, Gradient Boosting**.  

3. **Stacking**  
   - Train different models (e.g., tree, logistic regression, SVM).  
   - Combine their outputs using a **meta-model**.  

### Why Use Ensembles?
- Reduce **variance** (unstable predictions).  
- Reduce **bias** (systematic error).  
- Improve **accuracy** and **generalization**.  
- Works like “wisdom of the crowd.”  

---
