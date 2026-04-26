# Natural-Language-to-SQL-queries
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

```text
Which product has highest sales?
```

---
