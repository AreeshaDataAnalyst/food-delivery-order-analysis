# food-delivery-order-analysis
Python &amp; Pandas analysis of food delivery orders covering data cleaning, sales analysis, visualization, statistics, and Linear Regression.
# 🍔 Food Delivery Order Analysis

A Python-based data analysis project focused on exploring food delivery order data using **Pandas, Matplotlib, Seaborn, and Scikit-learn**.

The project covers data cleaning, sales analysis, statistical analysis, data visualization, and a basic machine learning model using Linear Regression.

---

## 📌 Project Overview

This project analyzes food delivery order data to understand:

* Order and dataset structure
* Missing values and duplicate records
* Total sales generated from orders
* Best-selling dishes
* Average ratings by category
* Distribution of dish prices
* Relationship between price and total sales
* Statistical characteristics of total sales
* Prediction of total sales using Linear Regression

The project was completed using Python and common data analysis and machine learning libraries.

---

## 🛠️ Technologies & Libraries

* **Python**
* **Pandas** — Data cleaning and analysis
* **Matplotlib** — Data visualization
* **Seaborn** — Statistical visualization
* **Scikit-learn** — Machine learning
* **Google Colab / Jupyter Notebook**

---

## 📂 Dataset

The project uses a food delivery dataset containing information related to dishes, categories, prices, quantities, ratings, and order frequency.

The dataset file used in the notebook is:

```text
Foodpanda Analysis Dataset.csv
```

---

## 🔍 Project Workflow

### 1. Data Loading & Exploration

The dataset is loaded using Pandas and basic information is explored, including:

* Dataset shape
* First five rows
* Column information
* Data types

```python
df = pd.read_csv("Foodpanda Analysis Dataset.csv")

print("Shape:", df.shape)
display(df.head())
df.info()
```

---

### 2. Data Cleaning

Missing values are identified and handled.

For numerical columns, **median imputation** is used because the median is less affected by extreme values.

For categorical columns, **mode imputation** is used because it represents the most frequently occurring category.

Duplicate rows are also removed.

```python
for col in df.select_dtypes(include="number").columns:
    df[col] = df[col].fillna(df[col].median())

for col in df.select_dtypes(include="object").columns:
    df[col] = df[col].fillna(df[col].mode()[0])

df = df.drop_duplicates()
```

---

### 3. Total Sales Calculation

A new `total_sales` column is created using:

```text
total_sales = price × quantity
```

```python
df["total_sales"] = df["price"] * df["quantity"]
```

This allows order-level sales to be analyzed.

---

### 4. Best-Selling Dishes

The project identifies the **top 3 best-selling dishes** based on total sales.

```python
top_3_dishes = (
    df.groupby("dish_name")["total_sales"]
    .sum()
    .sort_values(ascending=False)
    .head(3)
)
```

---

### 5. Category Rating Analysis

Average ratings are calculated for each food category.

```python
average_rating = df.groupby("category")["rating"].mean()
```

This helps compare customer ratings across different categories.

---

### 6. Rating Classification

A custom function is created to classify ratings into three groups:

| Rating | Label   |
| ------ | ------- |
| 4–5    | Good    |
| 3      | Average |
| 1–2    | Poor    |

```python
def rating_label(r):
    if r >= 4:
        return "Good"
    elif r == 3:
        return "Average"
    else:
        return "Poor"
```

The resulting classification is stored in a new `rating_label` column.

---

## 📊 Data Visualization

The project includes several visualizations.

### Total Sales by Category

A bar chart is used to compare total sales across food categories.

### Distribution of Dish Prices

A histogram is used to understand the distribution of dish prices.

### Price vs Total Sales

A scatter plot is used to examine the relationship between dish price and total sales.

The analysis indicates a **positive relationship between price and total sales**, where total sales generally increase as price increases.

---

## 📈 Statistical Analysis

The following statistical measures are calculated for `total_sales`:

* Mean
* Median
* Standard deviation

The analysis found that the mean total sales is higher than the median, suggesting that some higher sales values are increasing the average.

The standard deviation indicates considerable variation in total sales values.

---

## 🤖 Machine Learning

A basic **Linear Regression** model is used to predict `total_sales`.

### Features

The model uses:

* `price`
* `quantity`
* `order_frequency`

### Target

```text
total_sales
```

The dataset is divided into:

* **80% Training Data**
* **20% Testing Data**

with:

```python
random_state=42
```

### Model

```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()

model.fit(X_train, y_train)

y_pred = model.predict(X_test)
```

---

## 📏 Model Evaluation

The model is evaluated using the **R² (R-squared) score**.

The notebook reports an R² score of approximately **0.8936**.

This indicates that the selected features explain a large proportion of the variation in total sales within this dataset.

> Note: The result is specific to this dataset and train/test split and should not be interpreted as proof that the model will perform equally well on new real-world data.

---

## 💡 Key Skills Demonstrated

This project demonstrates practical beginner-level skills in:

* Data loading
* Data inspection
* Missing-value handling
* Duplicate removal
* Feature creation
* GroupBy analysis
* Sorting and aggregation
* Custom Python functions
* Data visualization
* Descriptive statistics
* Train/test splitting
* Linear Regression
* R² model evaluation

---

## 🚀 How to Run

### 1. Clone the repository

```bash
git clone https://github.com/your-username/food-delivery-order-analysis.git
```

### 2. Open the project

Open the project folder in **Jupyter Notebook, JupyterLab, or VS Code**.

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Make sure the dataset is in the same folder

```text
Foodpanda_Analysis_Dataset.csv
```

### 5. Open the notebook

```text
Food_Delivery_Order_Analysis.ipynb
```

Run the cells from top to bottom.

---

## 📦 Requirements

The main libraries required for this project are:

```text
pandas
matplotlib
seaborn
scikit-learn
jupyter
```

---

## 🎯 Project Purpose

This project was created as a practical exercise to apply Python and data analysis concepts to a food delivery dataset.

It demonstrates the complete basic workflow from **data cleaning and exploration to visualization, statistical analysis, and machine learning**.

---

## 👩‍💻 Author

**Areesha Atique**

Computational Mathematics Graduate | Data Analytics Enthusiast

Interested in:

* Data Analytics
* Business Intelligence
* Python
* SQL
* Power BI
* Data-driven Business Solutions

---

⭐ If you find this project useful, feel free to explore the notebook and analysis.
