
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


##The Data Health Dashboard (DSBDA Pre-processing)
Where to add: After the block that finishes loading the CSVs into the database (around Page 4 of your PDF, after the conn.close() and before !pip install google-genai).
Code to insert:

# --- DSBDA ADDITION: DATA WRANGLING REPORT ---
import pandas as pd
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


2. The Analytics Summary (Descriptive Stats)
Where to add: Inside the execute_query function (around Page 8), right before the final return results_df line.
Code to insert:

        # --- DSBDA ADDITION: DESCRIPTIVE STATISTICS ---
        if not results_df.empty:
            print("\n📈 ANALYTICS SUMMARY:")
            numeric_cols = results_df.select_dtypes(include=['number']).columns
            if not numeric_cols.empty:
                # Shows Mean, Max, Min for any numbers found in the result
                display(results_df[numeric_cols].describe().loc[['mean', 'max', 'min']])


3. Automated Visualization (Plotly)
Where to add: At the very end of your notebook as a new function, or right after the text2sql function definition (around Page 9).
Code to insert:

import plotly.express as px
def visualize_results(df, user_query):
    if isinstance(df, pd.DataFrame) and not df.empty:
        cols = df.columns
        if len(cols) >= 2:
            # Simple logic: If 1st col is text and 2nd is a number, draw a chart
            try:
                fig = px.bar(df, x=cols[0], y=cols[1], title=f"Visualizing: {user_query}")
                fig.show()
            except Exception as e:
                print("Visualization skipped (Incompatible data types)")

# Update your call at the bottom like this:
# res = text2sql(genai_client, prompt, "show me order count by country")
# visualize_results(res, "order count by country")


4. Update the text2sql wrapper
Where to add: Modify your existing text2sql function (around Page 9) to include the visualizer automatically.
Change it to this:


def text2sql(genai_client, prompt, user_query):
    output = get_sql_query(genai_client, prompt, user_query)
    if output['status'] == 'success':
        results = execute_query(output['response'])
        # AUTO-VISUALIZE CALL
        visualize_results(results, user_query) 
        return results
    return output

```text
Which product has highest sales?
```

---
