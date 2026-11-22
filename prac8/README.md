# Practical 8: Decision Trees and Max Depth

## Aim
To implement a Decision Tree Classifier on the Pima Indians Diabetes dataset and study how the maximum depth affects the complexity and performance of the model.

## Objectives
- Understand how a Decision Tree Classifier works
- Separate the input features from the target variable
- Split the data into training and testing sets
- Build two decision trees with different maximum depths and compare their accuracy
- Visualize the trees and understand their structure
- Understand entropy, information gain and Gini impurity
- Identify the root node and how the tree makes decisions

## Dataset
- **File:** `diabetes.csv` (Pima Indians Diabetes dataset, included in this folder)
- **Size:** 768 rows, 9 columns
- **Features (8):** Pregnancies, Glucose, BloodPressure, SkinThickness, Insulin, BMI, DiabetesPedigreeFunction, Age
- **Target:** `Outcome` (0 = no diabetes, 1 = diabetes), so this is a binary classification problem

## Tools Used
Python, pandas, NumPy, Matplotlib, scikit-learn (Google Colab)

## Procedure

1. **Load the data** and separate `X` (all columns except `Outcome`) from `y` (`Outcome`).
2. **Split the data** 80/20 with `train_test_split(test_size=0.20, random_state=42, stratify=y)`.
   - Training set: 614 rows. Test set: 154 rows.
   - `stratify=y` keeps the proportion of diabetic and non-diabetic cases the same in both sets.
3. **Train a shallow tree:** `DecisionTreeClassifier(criterion="entropy", max_depth=4)`.
4. **Train a deep tree:** `DecisionTreeClassifier(criterion="entropy", max_depth=20)`.
5. **Compare** their accuracy and classification reports on the test set.
6. **Visualize** both trees with `plot_tree`.
7. **Study the splitting criteria** with one-level trees using entropy and Gini.
8. **Find the root node** of the shallow tree.

## Results

### Model comparison

| Model | max_depth | Test accuracy |
|---|---|---|
| Shallow tree | 4 | 0.805 |
| Deep tree | 20 | 0.701 |

**Shallow tree (depth 4)**

| Class | Precision | Recall | F1-score |
|---|---|---|---|
| 0 (no diabetes) | 0.84 | 0.87 | 0.85 |
| 1 (diabetes) | 0.74 | 0.69 | 0.71 |

**Deep tree (depth 20)**

| Class | Precision | Recall | F1-score |
|---|---|---|---|
| 0 (no diabetes) | 0.75 | 0.80 | 0.78 |
| 1 (diabetes) | 0.58 | 0.52 | 0.55 |

The deeper tree performs worse on unseen data. A tree allowed to grow to depth 20 can create a branch for almost every training example, so it **memorizes noise** in the training set instead of learning the general pattern. This is **overfitting**. The shallow tree is simpler, so it generalizes better. Limiting `max_depth` is one way to control overfitting.

### Root node
The root node of the depth-4 tree splits on **Glucose ≤ 154.5**. Glucose is therefore the single most informative feature for separating diabetic from non-diabetic cases.

### Entropy, information gain and Gini
- **Entropy** measures the uncertainty (impurity) of a node. It is 0 for a pure node and highest when the classes are evenly mixed. Entropy = -Σ pᵢ log₂ pᵢ
- **Information gain** = entropy of the parent node minus the weighted average entropy of its child nodes. The tree picks the split with the highest information gain.
- **Gini impurity** = 1 - Σ pᵢ². It is another impurity measure that ranges from 0 (pure) to 0.5 (for two evenly mixed classes), and the tree picks the split that reduces it most.

A one-level tree (`max_depth=1`) was trained with each criterion. Both chose **Glucose** as the only split, so its feature importance is 1.0 and all other features are 0. With a single split, this only shows which feature is chosen at the root. It does not show the information gain of every feature.

## Conclusion
A Decision Tree Classifier was trained to predict diabetes. The shallow tree (max_depth = 4) reached 80.5% test accuracy against 70.1% for the deep tree (max_depth = 20), showing that a more complex tree is not always better. Both entropy and Gini selected Glucose as the root feature.

## Limitations
- Accuracy comes from a single train/test split of 154 rows, so the numbers can change with a different split. Cross-validation would give a more reliable comparison.
- Only two depths were compared. Trying depths 1 to 20 and plotting train and test accuracy would show the overfitting curve clearly.
- In this dataset, zeros in `Insulin`, `SkinThickness`, `BloodPressure` and `BMI` are likely missing values and were not cleaned.
