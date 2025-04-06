# CODE

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import statsmodels.api as sm
from statsmodels.tsa.stattools import adfuller

# File path
file_path = r"C:\Users\Lenovo\Downloads\API_SP.DYN.TFRT.IN_DS2_EN_csv_v2_162\API_SP.DYN.TFRT.IN_DS2_EN_csv_v2_162.csv"

# Load dataset
df = pd.read_csv(file_path, delimiter=',', skiprows=4, on_bad_lines='skip')

# Drop unnecessary columns
df = df.drop(columns=["Country Code", "Indicator Name", "Indicator Code", "Unnamed: 68"], errors='ignore')

# Convert years to numeric format
df_long = pd.melt(df, id_vars=["Country Name"], var_name="Year", value_name="Birth Rate")
df_long["Year"] = pd.to_numeric(df_long["Year"])
df_long["Birth Rate"] = pd.to_numeric(df_long["Birth Rate"], errors='coerce')

# Drop NaN values
df_long.dropna(subset=["Birth Rate"], inplace=True)

# Select a specific country (e.g., "United States")
country = "India"
df_country = df_long[df_long["Country Name"] == country].set_index("Year")
df_country = df_country.drop(columns=["Country Name"])

```
