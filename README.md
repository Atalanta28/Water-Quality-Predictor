# Water-Quality-Predictor
Here's a detailed explanation of the water quality analysis code:

### 1. Data Loading and Initial Exploration
- **Libraries Import**: The code imports essential Python libraries for data analysis (pandas, numpy), visualization (matplotlib, seaborn), and machine learning (scikit-learn).
- **Data Loading**: Loads water quality data from a CSV file with semicolon delimiters.
- **Initial Exploration**:
  - Checks dataset shape (rows × columns)
  - Displays first 5 rows
  - Shows data types of each column
  - Identifies missing values

### 2. Data Preprocessing
- **Date Conversion**: Converts the date column to datetime format for time series analysis.
- **Feature Engineering**:
  - Extracts year, month, and day from dates
  - Handles missing values by filling with median
  - Removes duplicate rows
- **Outlier Treatment**: Uses Interquartile Range (IQR) method to remove outliers from numerical water quality parameters.

### 3. Data Visualization
- **Time Series Plots**: Shows trends of each water quality parameter (NH4, BSK5, etc.) across different locations over time.
- **Correlation Matrix**: Heatmap showing relationships between different water quality parameters.
- **Box Plots**: Identifies distribution and outliers for each water quality parameter.

### 4. Time Series Analysis
- **Seasonal Decomposition**: For a specific location (id=1) and parameter (O2), it decomposes the time series into:
  - Trend component
  - Seasonal component
  - Residual component
- **Note**: This section had a bug (fixed in previous solutions) where it didn't check for sufficient data points before decomposition.

### 5. Machine Learning Modeling
- **Data Preparation**:
  - Splits data into features (X) and target (y=O2 levels)
  - Creates train/test splits (80/20)
  - Scales features using StandardScaler
  - Applies PCA for dimensionality reduction (keeping 95% variance)
  
- **Model Evaluation**:
  - Tests three regression models:
    1. Linear Regression (baseline)
    2. Random Forest (ensemble method)
    3. Support Vector Regression (SVR)
  - Evaluates using RMSE and R² metrics
  - Shows feature importance for tree-based models

- **Hyperparameter Tuning**:
  - Uses GridSearchCV to find optimal parameters for Random Forest
  - Evaluates combinations of:
    - Number of trees (n_estimators)
    - Tree depth (max_depth)
    - Split criteria (min_samples_split/leaf)

- **Result Visualization**:
  - Actual vs Predicted values plot
  - Residuals analysis plot

### 6. Time Series Forecasting
- **Train/Test Split**: For location 1's O2 data, splits into 80% train and 20% test chronologically.
- **Window Creation**: Creates sliding windows of 3 time steps (look_back=3) to predict the next value.
- **Model Training**: Uses Random Forest on the time series windows.
- **Evaluation**: Calculates and displays RMSE for both training and test sets.
- **Visualization**: Shows actual vs predicted values over time.

### Key Components and Their Purposes:

1. **Data Quality Checks**:
   - Missing value handling
   - Outlier detection/removal
   - Duplicate removal

2. **Exploratory Analysis**:
   - Visual trends over time
   - Parameter distributions
   - Correlation between parameters

3. **Model Development**:
   - Multiple algorithm comparison
   - Dimensionality reduction
   - Hyperparameter optimization

4. **Time Series Specific**:
   - Seasonal pattern analysis
   - Time-based forecasting
   - Sequential train/test splitting

### Scientific Approach:
The code follows a complete data science workflow:
1. Data understanding → 2. Preparation → 3. Exploration → 4. Modeling → 5. Evaluation

It handles both:
- Traditional regression (predicting O2 from other parameters)
- Time series forecasting (predicting future O2 levels)

The visualizations help interpret both the data patterns and model performance, while the statistical metrics provide quantitative performance measures.
