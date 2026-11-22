# Practical 9: K-Nearest Neighbors (KNN)

## Aim
To implement the K-Nearest Neighbors (KNN) classification algorithm on the Iris dataset and study how different values of K affect classification performance.

## Objectives
- Understand how the KNN algorithm works
- Perform exploratory data analysis (EDA) on the Iris dataset
- Separate the features from the target and split the data into training and testing sets
- Apply feature scaling with `StandardScaler`
- Train a KNN classifier and predict flower species
- Evaluate the model with a confusion matrix, accuracy and a classification report
- Compare error rates for different K values and identify the best K
- Visualize actual and predicted classes using PCA

## Dataset
- **Source:** Iris dataset, loaded with `sklearn.datasets.load_iris`
- **Size:** 150 samples, 4 features, 3 classes (50 samples each)
- **Features:** sepal length, sepal width, petal length, petal width (all in cm)
- **Classes:** setosa, versicolor, virginica

## Tools Used
Python, pandas, NumPy, Matplotlib, Seaborn, scikit-learn (Google Colab)

## How KNN Works
KNN is a distance-based algorithm. To classify a new sample, it finds the **K closest training samples** and predicts the **majority class** among them. It has no training phase beyond storing the data. Because it relies on distances, features must be on a similar scale.

## Procedure

### Step 1: EDA
`head()`, `describe()` and `groupby("species").mean()` were used to inspect the data. The class means show that petal length and petal width separate the species clearly:

| Species | Petal length | Petal width |
|---|---|---|
| setosa | 1.46 | 0.25 |
| versicolor | 4.26 | 1.33 |
| virginica | 5.55 | 2.03 |

### Step 2: Split and scale
- 80/20 split with `train_test_split(test_size=0.2, random_state=42, stratify=y)`: 120 training samples and 30 test samples.
- `StandardScaler` was fitted on the training data only and then applied to the test data. This avoids **data leakage** from the test set into training.

### Step 3: Train with K = 5
`KNeighborsClassifier(n_neighbors=5)` was trained and used to predict the test set.

### Step 4: Evaluation (K = 5)
**Accuracy = 0.9333 (28 of 30 correct).**

Confusion matrix (rows = actual, columns = predicted), reconstructed from the classification report:

| | setosa | versicolor | virginica |
|---|---|---|---|
| **setosa** | 10 | 0 | 0 |
| **versicolor** | 0 | 10 | 0 |
| **virginica** | 0 | 2 | 8 |

Classification report:

| Class | Precision | Recall | F1-score | Support |
|---|---|---|---|---|
| setosa | 1.00 | 1.00 | 1.00 | 10 |
| versicolor | 0.83 | 1.00 | 0.91 | 10 |
| virginica | 1.00 | 0.80 | 0.89 | 10 |

- **Precision:** of the samples predicted as a class, how many truly belong to it
- **Recall:** of the samples that truly belong to a class, how many were found
- **F1-score:** harmonic mean of precision and recall
- **Support:** number of actual test samples in each class

The only mistakes were two virginica flowers predicted as versicolor. These two classes overlap in feature space, while setosa is clearly separable.

### Step 5: Error rate for K = 1 to 20
Error rate = 1 - accuracy.

| K | Error rate |
|---|---|
| 1 | 0.0333 |
| 2 to 6 | 0.0667 |
| 7 | 0.0333 |
| 8 | 0.0667 |
| 9 to 20 | 0.0333 |

### Step 6: Best K
`np.argmin` returns the first minimum, so **K = 1** was selected with an error rate of 0.0333 (accuracy 0.9667). Every K from 9 to 20 gives exactly the same error rate.

### Step 7: PCA visualization
PCA projects the 4 features into 2 dimensions so that actual and predicted classes can be plotted side by side, with misclassified samples marked by crosses. PCA is used only for display and does not change the predictions.

## Conclusion
KNN classified the Iris test set with 93.3% accuracy at K = 5 and 96.7% at the best K. The only confusion was between versicolor and virginica. Scaling the features, splitting with stratification and fitting the scaler on training data only are important steps for a fair evaluation.

## Limitations and Notes
- **The test set has only 30 samples**, so one misclassified sample changes the error rate by 3.3 percentage points. The difference between K = 1 (0.033) and K = 5 (0.067) is a single sample, which is not strong evidence that K = 1 is better.
- **K was chosen using the test set**, so the "best accuracy" of 96.7% is slightly optimistic. A fairer approach is cross-validation, which tunes K on the training data and keeps the test set for the final check.
- **K = 1 is sensitive to noise** because a single outlier can decide the prediction. K values from 9 to 20 give the same error and are more stable, so a larger K such as 9 to 15 is a safer practical choice.
- Results come from one random split (`random_state=42`) and can change with a different split.
