# Practical 4: Understanding Data with Graphs

## Aim
To understand and analyse data using statistical techniques and graphical representations with Python libraries.

## Objectives
- Explore the Teaching Ratings dataset
- Identify duplicate observations
- Compare mean age and standard deviation before and after removing duplicate observations
- Calculate average teaching evaluation scores by course division
- Visualize the relationship between age and teaching evaluation
- Analyse data by gender and tenure using scatter plots

## Dataset
- **Source:** https://vincentarelbundock.github.io/Rdatasets/csv/AER/TeachingRatings.csv (from the `AER` R package)
- **Size:** 463 course evaluations, 13 columns
- **Unique instructors:** 94 (instructors appear in several rows because they teach multiple courses)

## Tools Used
Python, pandas, NumPy, Matplotlib, Seaborn (Google Colab)

## Procedure and Findings

### 1. Duplicate observations
Rows were grouped by the `prof` column. The 463 rows belong to only 94 instructors, so most instructors appear more than once, once per course they teach.

### 2. Mean and standard deviation of age

| Dataset | Mean age | Std. dev. |
|---|---|---|
| All 463 observations | 48.37 | 9.80 |
| 94 unique instructors | 47.55 | 10.26 |

Using all rows gives more weight to instructors who teach more courses. Using one row per instructor describes the actual faculty, so it is the better choice when the question is about instructors rather than courses.

### 3. Evaluation score by course division

| Division | Mean evaluation |
|---|---|
| Lower | 4.09 |
| Upper | 3.95 |

Instructors teaching lower-division courses receive slightly higher evaluations. The difference is about 0.13 points, so it is a modest gap and not a strong effect.

### 4. Age vs. evaluation score
The scatter plot shows no clear trend. High and low scores appear at every age, so age does not appear to be a major factor in teaching evaluations.

### 5. Effect of gender
Colouring the points by gender shows the same picture. Both male and female instructors have widely varying scores across ages, with no strong age trend in either group.

### 6. Effect of tenure
Adding tenure status (marker style) does not change the conclusion. Scores vary considerably across ages for each gender and tenure combination, and no clear relationship between age and evaluation appears.

## Conclusion
The Teaching Ratings dataset was analysed with pandas, NumPy, Matplotlib and Seaborn. Duplicate instructor rows were identified, and the age statistics were compared with and without them. Lower-division courses had slightly higher average evaluations. The scatter plots showed only a weak association between evaluation scores and age, gender, and tenure status. Graphs are an effective way to explore and interpret data before any formal testing.

## Limitations
These are descriptive plots, so they show associations, not cause and effect. No statistical tests were run, so the division difference may not be statistically significant.
