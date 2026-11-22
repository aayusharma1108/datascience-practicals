# Practical 1: Revisiting Pandas and NumPy

## Aim
To revise the basic concepts of Pandas and NumPy and perform numerical and matrix operations using Python.

## Objectives
- Understand the Pandas and NumPy libraries
- Create and manipulate a Pandas DataFrame
- Convert a DataFrame into a NumPy array
- Understand the shape, size, and dimensions of an array
- Perform basic arithmetic and matrix operations

## Tools Used
Python, pandas, NumPy (Google Colab)

## Procedure

### Step 1: Import libraries
- `pandas` (as `pd`) creates and manages DataFrames.
- `numpy` (as `np`) handles numerical and matrix operations such as addition, multiplication, transpose, and inverse.

### Step 2: Create a dataset and DataFrame
A dictionary holds the names of 6 students and their marks in three subjects (Stats, Physics, AI). `pd.DataFrame(data)` converts it into a table of 6 rows and 4 columns.

| Name | Stats | Physics | AI |
|---|---|---|---|
| Mahi | 85 | 76 | 91 |
| Shikha | 78 | 82 | 85 |
| Pallavi | 92 | 89 | 80 |
| Akshita | 67 | 71 | 73 |
| Tushar | 74 | 65 | 79 |
| Anshul | 88 | 90 | 95 |

### Step 3: Convert the DataFrame to a NumPy array
The numeric columns were selected and converted with `to_numpy()`:
```python
marks_arr = df[["Stats", "Physics", "AI"]].to_numpy()
```

### Step 4: Shape, size and dimensions

| Attribute | Meaning | Output |
|---|---|---|
| `marks_arr.shape` | rows and columns | (6, 3) |
| `marks_arr.size` | total elements | 18 |
| `marks_arr.ndim` | number of dimensions | 2 |

### Step 5: Arithmetic and matrix operations
A second 6×3 array (`additional_arr`) was created, and these operations were performed:

| Operation | Code | Notes |
|---|---|---|
| Addition | `marks_arr + additional_arr` | element-wise, result is 6×3 |
| Subtraction | `marks_arr - additional_arr` | element-wise, result is 6×3 |
| Multiplication | `marks_arr * additional_arr` | element-wise (not matrix multiplication) |
| Transpose | `marks_arr.T` | rows and columns swapped, result is 3×6 |
| Matrix product | `np.dot(marks_arr, additional_arr.T)` | (6×3) · (3×6) = 6×6 |
| Inverse | `np.linalg.inv(matrix_product)` | see the note below |

## Observation on the matrix inverse
The 6×6 matrix product came from multiplying a 6×3 matrix by a 3×6 matrix, so its rank is at most 3. A 6×6 matrix with rank 3 is **singular** and has no true inverse. NumPy still returned numbers, but they are extremely large (around 10¹²), which is a sign of floating-point error rather than a valid inverse. To invert a matrix correctly, it must be square and have full rank, for example a 3×3 matrix:
```python
small = marks_arr.T @ additional_arr      # (3x6) @ (6x3) = 3x3
print(np.linalg.matrix_rank(small))       # 3 means invertible
print(np.linalg.inv(small))
```

## Conclusion
In this practical, we revised the basics of Pandas and NumPy. We created a DataFrame, converted it into a NumPy array, and explored its shape, size, and dimensions. We performed addition, subtraction, element-wise multiplication, transpose, and matrix multiplication. We also saw that a matrix inverse exists only for square, full-rank matrices, and that the 6×6 product here was singular, so its computed "inverse" was not meaningful.
