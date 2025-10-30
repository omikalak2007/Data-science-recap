## 🤖 Enhanced Data Preprocessing and Modeling Pipeline

### Data Inspection & Cleaning

1.  **Identify Feature Types** 🔍: Identify data as **numerical** and **categorical** columns. This is the foundation for all subsequent steps.
2.  **Handle Missing Data (NaNs)**:
    * **Drop** columns that have missing values (NaNs) exceeding a high threshold (e.g., **50%**).
    * **Fill** the remaining NaNs in numerical columns (e.g., with the mean/median) and categorical columns (e.g., with the mode or a placeholder like 'Missing').
3.  **Address Duplicates**: Find and remove duplicates in **rows**. Checking for duplicates in individual columns often means finding repeated values, which is normal and not an issue unless the column is a unique identifier.
4.  **Manage Skewness & Normality** 📉:
    * Calculate **skewness** for numerical features.
    * Apply a **log transformation** (or square root, box-cox, etc.) to heavily skewed features (e.g., skewness $\geq 0.5$). This helps meet the normality assumptions of linear models.
5.  **Identify Outliers (Post-Transformation)**: Find outliers in numerical features **after** log transformation (using methods like the Interquartile Range (IQR) rule or Z-scores). Transformation often normalizes the data and changes the outlier values.
6.  **Fix Outliers**: Fix the outliers in columns, typically by **capping** (winsorizing) them at a threshold (e.g., the 5th and 95th percentiles or the IQR bounds) rather than dropping the rows entirely.
7.  **Drop Unwanted Categorical Columns**: Drop categorical columns that have too many unique values (high cardinality) or are otherwise irrelevant based on feature importance or domain knowledge.
8.  **Feature Engineering (Combining/Reducing)**: **Merge columns** based on domain knowledge if the number of features is very high, or create new meaningful features from existing ones (e.g., combining 'Day' and 'Month' into a 'Season' feature).

---

### Feature Transformation (The Missing Step)

9.  **Split Data (The Essential Step)** 🛑: **Split the data** into three sets: **Training**, **Validation**, and **Test** sets. This is crucial to prevent data leakage and ensure an unbiased model evaluation later.

10. **Encode Categorical Features**: Turn the categorical features into numerical using encoding methods:
    * **One-Hot Encoding** for nominal (unordered) features.
    * **Label/Ordinal Encoding** for ordinal (ordered) features.

11. **Feature Scaling (For Linear Models)**: Apply **Standard Scaling** (Z-score normalization) or **MinMaxScaler** to all numerical columns. This is mandatory for linear models (like Linear Regression, SVM, or those with regularization like Ridge/Lasso) and K-Nearest Neighbors, as they are sensitive to the scale of features.

---

### Model Training & Evaluation

12. **Train the Model**: Train the machine learning model on the **Training set**. Use the **Validation set** for hyperparameter tuning.
13. **Calculate Model Error**: Calculate the error of the final model on the **Test set** using appropriate metrics (e.g., **Mean Squared Error (MSE)** and **Mean Absolute Error (MAE)** for regression, or accuracy/F1-score for classification). This step provides the final, unbiased performance estimate.

