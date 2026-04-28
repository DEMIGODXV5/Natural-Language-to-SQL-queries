
# Natural Language to SQL Query Generator

This project converts natural language English queries into SQL queries using Gemini API and executes them on an ecommerce SQLite database.

## Tech Stack
- Python
- SQLite
- Gemini API
- Pandas
- Google Colab/Jupyter

## Features
- NL → SQL conversion
- Query execution
- JSON structured output
- Ecommerce dataset support

- always check for Gemini API key..
- used google colab to build this , hence the api key was hiddent in the google colab secrets. while using this on local sys do-
- # Natural Language to SQL using Gemini API

This project converts natural language queries into SQL queries using Google's Gemini API. It uses three CSV files:

- `customers.csv`
- `products.csv`
- `orders.csv`

The system reads these datasets, generates SQL queries from user input, and returns query results.

---

## Requirements

Make sure you have installed:

- Python
- Anaconda
- Jupyter Notebook
- Git
- Gemini API Key

---

## Step 1: Clone Repository

Open Anaconda Prompt/Terminal and run:

```bash
git clone https://github.com/your-username/your-repository-name.git
```

Go to project folder:

```bash
cd your-repository-name
```

---

## Step 2: Create Conda Environment

```bash
conda create -n nl_sql_env python=3.10
```

Activate environment:

```bash
conda activate nl_sql_env
```

---

## Step 3: Install Required Libraries

Install dependencies:

```bash
pip install pandas google-generativeai jupyter
```

OR if you have `requirements.txt`:

```bash
pip install -r requirements.txt
```

---

## Step 4: Add Gemini API Key

Open your notebook/python file and add:

```python
import google.generativeai as genai

genai.configure(api_key="YOUR_GEMINI_API_KEY")
```

Get API key from :contentReference[oaicite:0]{index=0}

---

## Step 5: Run Jupyter Notebook

Start Jupyter Notebook:

```bash
jupyter notebook
```

Open:

```bash
nl_to_sql.ipynb
```

Run all cells.

---

## Project Files

```bash
customers.csv
products.csv
orders.csv
nl_to_sql.ipynb
```

---

## Example Query

```text
Show all customers from Pune
```
# DSBDA Enhancements Added to Text-to-SQL E-commerce Project

This project has been enhanced with additional **Data Science and Big Data Analytics (DSBDA)** functionalities to improve preprocessing, analytical insights, and automated visualization.

---

## 1. Data Health Dashboard (Pre-processing)

### Where to Add
Insert this code block after loading CSV files into the SQLite database:

- After `conn.close()`
- Before `!pip install google-genai`

### Purpose
This module performs dataset quality checks on all database tables by identifying:

- Total records
- Missing values
- Duplicate records

### Code

```python
# --- DSBDA ADDITION: DATA WRANGLING REPORT ---
import pandas as pd
import sqlite3

def show_data_health():
    tables = ['customers', 'products', 'orders']
    conn = sqlite3.connect('ecommerce.db')

    print("📊 DATASET HEALTH REPORT (DSBDA Unit 2)")

    for t in tables:
        df = pd.read_sql(f"SELECT * FROM {t}", conn)

        print(f"\nTable: {t.upper()}")
        print(f"- Total Records: {len(df)}")
        print(f"- Missing Values: {df.isnull().sum().sum()}")
        print(f"- Duplicates: {df.duplicated().sum()}")

    conn.close()

show_data_health()
```

---

# 2. Analytics Summary (Descriptive Statistics)

### Where to Add
Insert this inside the `execute_query()` function right before:

```python
return results_df
```

### Purpose
Automatically generates descriptive statistics for numerical query outputs.

### Features
- Mean
- Maximum
- Minimum

### Code

```python
# --- DSBDA ADDITION: DESCRIPTIVE STATISTICS ---
if not results_df.empty:
    print("\n📈 ANALYTICS SUMMARY:")

    numeric_cols = results_df.select_dtypes(include=['number']).columns

    if not numeric_cols.empty:
        display(
            results_df[numeric_cols]
            .describe()
            .loc[['mean', 'max', 'min']]
        )
```

---

# 3. Automated Data Visualization (Plotly)

### Where to Add
Add this function at the end of your notebook or after the `text2sql()` function definition.

### Purpose
Automatically creates visualizations for query results.

### Features
- Detects compatible columns
- Creates bar charts automatically
- Handles incompatible datasets gracefully

### Code

```python
import plotly.express as px

def visualize_results(df, user_query):
    if isinstance(df, pd.DataFrame) and not df.empty:
        cols = df.columns

        if len(cols) >= 2:
            try:
                fig = px.bar(
                    df,
                    x=cols[0],
                    y=cols[1],
                    title=f"Visualizing: {user_query}"
                )
                fig.show()

            except Exception as e:
                print("Visualization skipped (Incompatible data types)")
```

---

# 4. Update the `text2sql()` Wrapper

### Where to Add
Modify your existing `text2sql()` function.

### Purpose
Automatically integrates SQL execution with visualization.

### Updated Code

```python
def text2sql(genai_client, prompt, user_query):
    output = get_sql_query(genai_client, prompt, user_query)

    if output['status'] == 'success':
        results = execute_query(output['response'])

        # AUTO VISUALIZATION
        visualize_results(results, user_query)

        return results

    return output
```

---

# Final Workflow

The complete workflow now follows:

1. Load CSV datasets into SQLite database  
2. Run Data Health Dashboard  
3. Convert natural language to SQL query  
4. Execute SQL query  
5. Generate descriptive analytics summary  
6. Automatically visualize results  

---

# Tech Stack

- Python  
- Pandas  
- SQLite  
- Google Gemini API  
- Plotly  
- Jupyter Notebook  

---

# Benefits of These Enhancements

✅ Better data preprocessing  
✅ Automatic data quality checks  
✅ Built-in descriptive analytics  
✅ Automated visual insights  
✅ Improved project alignment with DSBDA concepts  


