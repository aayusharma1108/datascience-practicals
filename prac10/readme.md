# Practical X: Principal Component Analysis (PCA) on the Wine Dataset

## Aim
To explore the Wine dataset, standardize its features and apply Principal Component Analysis (PCA) to reduce dimensionality while retaining the important information, and to visualize the separation between wine classes.

## Dataset
- **Source:** Wine dataset, loaded with `sklearn.datasets.load_wine()`
- **Size:** 178 samples, 13 numeric features (alcohol, malic acid, flavanoids, proline, etc.)
- **Classes:** 3 wine cultivars (class_0, class_1, class_2)

## Tools Used
Python, NumPy, pandas, Matplotlib, Seaborn, scikit-learn (Google Colab)

## Procedure

1. **Load the data** with `load_wine()` and convert it into a DataFrame. Add the target labels and class names.
2. **Basic statistics:** check the shape, count the samples in each class, and compute descriptive statistics (mean, standard deviation, minimum, maximum).
3. **Boxplot by class:** compare the distribution of `alcohol` across the three classes (median, spread and outliers).
4. **Scatter plot:** plot `flavanoids` against `proline`, coloured by class.
5. **Covariance matrix:** compute the covariance matrix of the raw features and visualize it as a heatmap.
6. **Standardization:** scale the features with `StandardScaler` so each has mean ≈ 0 and standard deviation ≈ 1. Verify with `describe()` and plot the covariance matrix of the scaled data.
7. **PCA:** apply `PCA(n_components=3)` to the scaled data. Print the explained variance ratio and total variance explained, then plot the three components in a 3D scatter plot coloured by class.

## Key Concepts

- **Covariance matrix:** shows how pairs of features vary together. On raw data it is dominated by features with large numeric scales (such as proline), so it is hard to compare features.
- **Standardization:** `z = (x - mean) / std`. PCA depends on variance, so unscaled features with large ranges would dominate the principal components.
- **Principal components:** new, uncorrelated axes that are linear combinations of the original features, ordered by how much variance they capture. PC1 captures the most, then PC2, and so on.
- **Explained variance ratio:** the fraction of the total variance each component captures.

## Results

| Component | Explained variance |
|---|---|
| PC1 | ≈ 36.2% |
| PC2 | ≈ 19.2% |
| PC3 | ≈ 11.1% |
| **Total (3 components)** | **≈ 66.5%** |

*(Replace with the values printed by your notebook.)*

Three components retain roughly two-thirds of the information in the original 13 features. In the 3D plot the three wine classes form fairly distinct groups, so PCA preserves the structure needed to tell the classes apart even after dropping from 13 dimensions to 3.

## Conclusion
Standardizing the features and applying PCA reduced the 13-dimensional Wine dataset to 3 components while keeping most of the variance and the class separation. This makes high-dimensional data easier to visualize and can reduce the number of features needed for later modelling.

## Limitations
- PCA is unsupervised. It maximizes variance, not class separation, so the classes separate well here but this is not guaranteed in general.
- Principal components are combinations of the original features, so they are harder to interpret than the original features.
- Only about two-thirds of the variance is retained by 3 components, so some information is lost.
