# Template

## Creating NumPy Arrays

### 1D Arrays from lists

```python
import numpy as np

# Create from list
py_list = list(range(1,5))
np_array = np.array(py_list)
print(np_array)  # Output: array([1, 2, 3, 4])
```

### 2D Arrays (matrices)

```python
# Create a 2D array
rows, cols = 3, 4
list_of_list = [[j for j in range(cols)] for i in range(rows)]
np_array = np.array(list_of_list)
print(np_array)
```

### Creating arrays from scratch

```python
# Range of values
print("np.arange")
print(np.arange(1, 10, 2))  # <start,stop,step>, stop is not included in the array

# Arrays of zeros
print("np.zeros")
print(np.zeros((2, 2)))     # Array of zeros

# Arrays of ones
print("np.ones")
print(np.ones(5))           # Array of ones

# 2-D arrays
print("2-D arrays")
print(np.ones([5,2])) # 2-D array of ones 
print(np.random.random((2, 2)))  # 2-D array Random values between 0 and 1
```

## Examining numpy array structure and storage

```python
print("2-D array")
np_2d = np.ones([5,2])
print("\tshape", np_2d.shape)
print("\tndim", np_2d.ndim)
print("\tsize", np_2d.size)
```

## Type Homogeneity

```python
# Python collections like lists can contain mixed types:
mixed_list = [1, "DNA", True, 3.14]  # Different types in one list
print(type(mixed_list), type(mixed_list[0]), type(mixed_list[1]), type(mixed_list[2]), type(mixed_list[3]))

# NumPy arrays enforce type homogeneity:
# All elements converted to the same type (float64)
np_array = np.array([1, 2, 3.14, 4])
print(np_array.dtype)
```

## Key NumPy Data Types

### Integer Types

```python
# Storing chromosome positions for a set of genes
gene_positions = np.array([45123, 67845, 123456, 789012], dtype=np.int32)
print(gene_positions.dtype)

print(f"int8 range: {np.iinfo(np.int8).min} to {np.iinfo(np.int8).max}")
print(f"int16 range: {np.iinfo(np.int16).min} to {np.iinfo(np.int16).max}")
```

### String Types

```python
# Array of gene IDs
gene_ids = np.array(['BRCA1', 'TP53', 'EGFR', 'KRAS'])
print(gene_ids.dtype)

x = np.array(["1234567890", "12345678901234567890"])
print(x.dtype)

# Output
# dtype('<U20')
```

```python
np.array([1, 2, 3])            # Creates int64 array
np.array([1.0, 2.0, 3.0])      # Creates float64 array
np.array([True, False, True])  # Creates bool array
np.array(['A', 'C', 'G', 'T']) # Creates string array
```

## Array Indexing and Slicing

### 1D Array Operations

```python
# Example: String sequence converted to numerical representation
# A=0, C=1, G=2, T=3
dna_seq = np.array([0, 1, 2, 3, 0, 0, 1, 2])  # "ACGTAACG"

# Single element access through indexing
print("Original array", dna_seq)
print("First element (0th index)", dna_seq[0])    # First nucleotide (0 = A)
print("Fourth element", dna_seq[3])    # Fourth nucleotide (3 = T)
print("Last element",dna_seq[-1])   # Last nucleotide (2 = G) using negative indexing
```

### 1D Array Slicing

```python
print("Original array", dna_seq)

# Slicing * extracting subsequences
print("From second to fourth", dna_seq[1:4])  # From second to fourth nucleotide: array([1, 2, 3]) = "CGT"
print("First three nucleotides", dna_seq[:3])   # First three nucleotides: array([0, 1, 2]) = "ACG"
print("From sixth nucleotide to the end", dna_seq[5:])   # From sixth nucleotide to the end: array([0, 1, 2]) = "ACG"

# Slicing with negative indices
print("Last three nucleotides", dna_seq[-3:])  # Last three nucleotides: array([0, 1, 2]) = "ACG"

# Slicing with step
print("Every second nucleotide", dna_seq[::2])  # Every second nucleotide: array([0, 2, 0, 1]) = "AGAC"

# Reverse array
print("Every second nucleotide", dna_seq[::-1]) 
```

## NumPy Boolean Masking and Filtering

### Boolean Masking: The Concept

```python
import numpy as np

# Create a sample array
data = np.array([1, 4, 2, 5, 3])
print("Original array:", data)

# Create a boolean mask for elements greater than 3
mask = data > 3
print("Boolean mask (data > 3):", mask)
# This produces: [False, True, False, True, False]

# Apply the mask to select elements
selected_data = data[mask]
print("Selected elements:", selected_data)
# This produces: [4, 5]

## Elegant approach -  mask array has the exact same shape as data array
## Each position containing information about whether that element meets our criteria
```

### Using np.where(): Finding Positions

```python
# Create an array with a sequence
data = np.arange(0, 20, 3)  # [0, 3, 6, 9, 12, 15, 18]
print("Original array:", data)

# Find indices where elements are even
indices = np.where(data % 2 == 0)
print("Indices of even elements:", indices[0])
# This produces: [0, 2, 4, 6]

# Use these indices to get the actual values
even_elements = data[indices]
print("Even elements:", even_elements)
# This produces: [ 0,  6, 12, 18]
```

## Essential Array Operations with NumPy

```python
import numpy as np

# Create a simple 1D array
a = np.ones(6)
print("Original array:")
print(a)
print(f"Dimensions: {a.ndim}")  # Number of dimensions
print(f"Shape: {a.shape}")      # Tuple showing size in each dimension
```

```python
a = np.array(range(1,7))
# Reshape our 1D array with 6 elements into a 2D array (2 rows, 3 columns)
b = a.reshape(2, 3)
print("\nReshaped to 2x3 array:")
print(b)
print(f"Dimensions: {b.ndim}")
print(f"Shape: {b.shape}")
```

### Summary Statistics

```python
# Create a 2D array
data = np.array([[1, 2, 3],
                 [4, 5, 6]])

print("Our data:")
print(data)

# Sum of all elements
total = np.sum(data)
print(f"\nTotal sum: {total}")  # 21

# Column sums (axis=0)
col_sums = np.sum(data, axis=0)
print(f"Column sums: {col_sums}")  # [5 7 9]
## Collapse values in rows along the the column 0 and aggregate: [1, 4] = 5
## Collapse values in rows along the the column 1 and aggregate: [2, 5] = 7
## Collapse values in rows along the the column 2 and aggregate: [3, 6] = 9

# Row sums (axis=1)
row_sums = np.sum(data, axis=1)
print(f"Row sums: {row_sums}")  # [6 15]
## Collapse values in columns along the the row 0 and aggregate: [1, 2, 3] = 6
## Collapse values in columns along the the row 1 and aggregate: [4, 5, 6] = 15
```

## Vectorized Operations in NumPy: Beyond Python Loops

### The Speed Advantage: Loops vs. Vectorization

```python
import numpy as np
import time

# Create a large array for testing
size = 10000000
data = np.random.random(size)

# Method 1: Traditional Python loop
start_time = time.time()
result_loop = []
for value in data:
    result_loop.append(value * 2 + 5)
loop_time = time.time() - start_time
print(f"Python loop time: {loop_time:.4f} seconds")

# Method 2: NumPy vectorized operation
start_time = time.time()
result_vectorized = data * 2 + 5
vector_time = time.time() - start_time
print(f"NumPy vectorized time: {vector_time:.4f} seconds")

# Calculate the speedup
speedup = loop_time / vector_time
print(f"Vectorized operations are {speedup:.1f}x faster!")
```

```python
import numpy as np

# Create two arrays
a = np.array([1, 2, 3, 4, 5])
b = np.array([10, 20, 30, 40, 50])

# Element-wise operations
addition = a + b
subtraction = b - a
multiplication = a * b
division = b / a

print(f"Addition: {addition}")
print(f"Subtraction: {subtraction}")
print(f"Multiplication: {multiplication}")
print(f"Division: {division}")
```

### Basic Vectorized Operations in NumPy

```python
import numpy as np

# Create two arrays
a = np.array([1, 2, 3, 4, 5])
b = np.array([10, 20, 30, 40, 50])

# Element-wise operations
addition = a + b
subtraction = b - a
multiplication = a * b
division = b / a

print(f"Addition: {addition}")
print(f"Subtraction: {subtraction}")
print(f"Multiplication: {multiplication}")
print(f"Division: {division}")
```

### Scalar Operations

```python
# Scalar operations
a = np.array([1, 2, 3, 4, 5])

plus_10 = a + 10
times_2 = a * 2
square = a ** 2
reciprocal = 1 / a

print(f"Plus 10: {plus_10}")
print(f"Times 2: {times_2}")
print(f"Squared: {square}")
print(f"Reciprocal: {reciprocal}")
```

### Comparison Operations

```python
# Comparison operations
a = np.array([1, 2, 3, 4, 5])

greater_than_3 = a > 3
less_than_equal_to_2 = a <= 2
equal_to_3 = a == 3

print(f"a > 3: {greater_than_3}")
print(f"a <= 2: {less_than_equal_to_2}")
print(f"a == 3: {equal_to_3}")

# Using boolean masks for filtering
filtered_data = a[greater_than_3]   # [4, 5]
print(f"Values greater than 3: {filtered_data}")
```

### Aggregation Functions and Universal Functions

```python
# Aggregation functions
a = np.array([1, 2, 3, 4, 5])

sum_a = np.sum(a)                   # Sum of all elements (15)
mean_a = np.mean(a)                 # Mean of all elements (3.0)
min_a = np.min(a)                   # Minimum value (1)
max_a = np.max(a)                   # Maximum value (5)
std_a = np.std(a)                   # Standard deviation (~1.41)

print(f"Sum: {sum_a}")
print(f"Mean: {mean_a}")
print(f"Min: {min_a}")
print(f"Max: {max_a}")
print(f"Standard deviation: {std_a}")
```

## Broadcasting in NumPy

Example 1: Adding a scalar to an array

```python
# Adding a scalar to an array
a = np.array([1, 2, 3, 4, 5])
result = a + 10  # Scalar 10 is broadcast to array [10, 10, 10, 10, 10]
print(result)    # [11, 12, 13, 14, 15]
```

## Pandas vs NumPy Relationship

```python
import numpy as np
import pandas as pd

# Try to put mixed types in NumPy - notice what happens
mixed_numpy = np.array([1, 'string', 3.14])
print(f"Mixed NumPy array: {mixed_numpy}")
print(f"Mixed array dtype: {mixed_numpy.dtype}")  # Converts to common type

# Pandas Series - can handle mixed types
pandas_series = pd.Series([1, 'string', 3.14])
print("\nPandas Series with mixed types:")
print(pandas_series)

print([type(i) for i in mixed_numpy])
print([type(i) for i in pandas_series])
```

### DataFrame Data Structures

```python
# Creating a Series
s = pd.Series([10, 20, 30, 40], index=['a', 'b', 'c', 'd'])
print("Pandas Series with custom index:")
print(s)
print(f"The index: {s.index}")
print(f"The values: {s.values}")  # Notice this returns a NumPy array

# Dictionary-like access
print(f"\nValue at index 'b': {s['b']}")
print(f"Values at indices 'a' and 'c': {s[['a', 'c']]}")

# NumPy-like operations
print(f"\nAdding 5 to all values: \n{s + 5}")
print(f"Values greater than 25: \n{s > 25}")
```

### The Pandas DataFrame

```python
# Creating a DataFrame
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['New York', 'Boston', 'Chicago']
}
df = pd.DataFrame(data)
print("Pandas DataFrame:")
print(df)

# DataFrame info
print(f"\nDataFrame shape: {df.shape}")
print(f"DataFrame columns: {df.columns}")
print(f"DataFrame index: {df.index}")

# Accessing a column (returns a Series)
print("\nAccessing the Age column:")
print(df['Age'])
print(f"Type of column: {type(df['Age'])}")
```

### Creating Pandas Objects from NumPy Arrays

```python
# NumPy array to Pandas Series
numpy_data = np.array([100, 200, 300, 400])
s1 = pd.Series(numpy_data)
print("Series with default index:")
print(s1)

s2 = pd.Series(numpy_data, index=['w', 'x', 'y', 'z'])
print("\nSeries with custom index:")
print(s2)
```

## Data Import and Export in Pandas

### Reading CSV Data

```python
import pandas as pd
from urllib.request import urlopen

# Basic CSV reading

sample_data_csv_url = "https://coderefinery.github.io/NumPy-and-Pandas-fundamentals-for-handling-biological-datasets/_downloads/4c11eeffe234e7bc729008f767fe631a/sample_data.csv"

df_csv = pd.read_csv(urlopen(sample_data_csv_url))
# df_csv = pd.read_csv('test_data/sample_data.csv')


print("Basic CSV import:")
print(df_csv.head())  # Show first 3 rows

# Customizing CSV import
df_csv_custom = pd.read_csv(urlopen(sample_data_csv_url),
                           sep=',',            # Delimiter (comma is default)
                           header=0,           # Row to use as column names (0 is default)
                           index_col='ID',     # Column to set as index
                           usecols=['ID', 'Name', 'Value'],  # Only import specific columns
                           nrows=5)            # Only read first 5 rows
print("\nCustomized CSV import:")
print(df_csv_custom)
```

### Reading Excel Data

```python
# Basic Excel reading

import requests
from io import BytesIO

## Read XLSX file directly from a URL
# sample_data_xls_url = "https://coderefinery.github.io/NumPy-and-Pandas-fundamentals-for-handling-biological-datasets/_downloads/04c10398f323fcf8ff5ec474e4b22205/sample_data.xlsx"

# response = requests.get(sample_data_xls_url)
# df_excel = pd.read_excel(BytesIO(response.content))

df_excel = pd.read_excel('test_data/sample_data.xlsx')
print("Basic Excel import:")
print(df_excel.head())

# Reading specific sheet
df_excel_sheet2 = pd.read_excel('test_data/sample_data.xlsx', 
                               sheet_name='Sheet 1 - sample_data',
                               skiprows=1)     # Skip first row
print("\nReading specific Excel sheet:")
print(df_excel_sheet2.head())

# List all sheets in workbook
xl = pd.ExcelFile('test_data/sample_data.xlsx')
print(f"\nAll sheets in workbook: {xl.sheet_names}")
```

### Writing Data to Files

```python
# Create a small DataFrame to export
data = {
    'Name': ['Alex', 'Beth', 'Charlie', 'Diana'],
    'Department': ['Sales', 'HR', 'Tech', 'Finance'],
    'Salary': [55000, 60000, 75000, 70000],
    'Hire_Date': ['2020-01-15', '2019-07-10', '2021-03-22', '2018-11-05']
}
df = pd.DataFrame(data)
print("DataFrame to export:")
print(df)

# Export to CSV
df.to_csv('employees.csv', index=False)
print("\nExported to CSV (employees.csv)")

# Export to Excel
df.to_excel('employees.xlsx', sheet_name='Employees', index=False)
print("Exported to Excel (employees.xlsx)")
```

### Data Inspection Methods

```python
# Let's inspect a more interesting dataset
import numpy as np

# Create a sample dataset with different data types
np.random.seed(42)  # For reproducibility
data = {
    'Category': np.random.choice(['A', 'B', 'C', 'D'], size=1000),
    'Value': np.random.normal(100, 20, size=1000),
    'Count': np.random.randint(1, 100, size=1000),
    'Date': pd.date_range(start='2023-01-01', periods=1000),
    'Flag': np.random.choice([True, False], size=1000)
}
df = pd.DataFrame(data)

# Add some missing values
df.loc[10:20, 'Value'] = np.nan
df.loc[500:510, 'Category'] = None

# Now let's inspect
print("First 5 rows with head():")
print(df.head())

print("\nLast 3 rows with tail(3):")
print(df.tail(3))

print("\nDataFrame information with info():")
df.info()

print("\nStatistical summary with describe():")
print(df.describe())

print("\nInclude all columns in describe (even non-numeric):")
print(df.describe(include='all'))

print("\nData types of each column:")
print(df.dtypes)

print("\nShape (rows, columns):", df.shape)

print("\nValue counts for 'Category':")
print(df['Category'].value_counts())
```

## DataFrame Manipulation & Sorting

### Basic Selection

```python
import pandas as pd
import numpy as np

# Create a sample dataset
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eva'],
    'Age': [24, 30, 35, 42, 28],
    'City': ['New York', 'Boston', 'Chicago', 'Seattle', 'Miami'],
    'Salary': [65000, 72000, 85000, 92000, 70000],
    'Department': ['HR', 'Sales', 'Tech', 'Tech', 'Finance']
}
df = pd.DataFrame(data)
df.index = ['emp001', 'emp002', 'emp003', 'emp004', 'emp005']  # Custom index
print("Original DataFrame:")
print(df)

# Single column selection - two methods
print("\n1. Single column as Series:")
print(df['Age'])  # Returns a Series

print("\n2. Alternative syntax for columns without spaces:")
print(df.Age)  # Also returns a Series, but only works if column name has no spaces

# Multiple column selection
print("\n3. Selecting multiple columns:")
print(df[['Name', 'Salary']])  # Returns a DataFrame

# Row selection by index label using .loc
print("\n4. Selecting row by index label:")
print(df.loc['emp003'])  # Returns a Series representing the row

# Row selection by position using .iloc
print("\n5. Selecting row by position (third row):")
print(df.iloc[2])  # Also returns a Series

# Selecting a subset of rows
print("\n6. Selecting multiple rows by position:")
print(df.iloc[1:4])  # Row indices 1, 2, and 3 (not including 4)

# Selecting specific cells
print("\n7. Selecting specific value (cell):")
print(df.loc['emp002', 'Salary'])  # Returns the value (72000)

# Selecting a subset of rows and columns
print("\n8. Selecting subset of rows and columns:")
print(df.loc['emp001':'emp003', ['Name', 'Age', 'Salary']])
## df.iloc[0:3, [0,1,3]] == df.loc['emp001':'emp003', ['Name', 'Age', 'Salary']] 
```

### Advanced Selection with Conditions

```python
# Boolean selection - rows where Age > 30
print("\n9. Boolean selection - employees over 30:")
print(df[df['Age'] > 30])

# Multiple conditions using & (and) and | (or)
print("\n10. Multiple conditions - Tech department with salary > 80000:")
print(df[(df['Department'] == 'Tech') & (df['Salary'] > 80000)])

# Using .query() method for cleaner syntax
## .query() method allows you to use and/or
## print("\n11. Using query method - same condition:")
## print(df.query("Department == 'Tech' and Salary > 80000"))

# Row selection with .isin()
print("\n12. Using .isin() - employees in HR or Finance:")
print(df[df['Department'].isin(['HR', 'Finance'])])
```

### Adding and Removing Columns

```python

# Create a sample dataset
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eva'],
    'Age': [24, 30, 35, 42, 28],
    'City': ['New York', 'Boston', 'Chicago', 'Seattle', 'Miami'],
    'Salary': [65000, 72000, 85000, 92000, 70000],
    'Department': ['HR', 'Sales', 'Tech', 'Tech', 'Finance']
}
df = pd.DataFrame(data)
df.index = ['emp001', 'emp002', 'emp003', 'emp004', 'emp005']  # Custom index
print("Original DataFrame:")
print(df)

# 1. Adding a new column with scalar value
df['Active'] = True
print("\n1. Adding 'Active' column with same value for all rows:")
print(df)

# 2. Adding a column with a list of values
df['Performance'] = [4.5, 4.0, 3.8, 4.7, 4.2]
print("\n2. Adding 'Performance' column with different values:")
print(df)

# 3. Adding a calculated column
df['Bonus'] = df['Salary'] * df['Performance'] / 100
print("\n3. Adding calculated 'Bonus' column:")
print(df)

# 4. Adding a column with conditional values
df['Experience'] = np.where(df['Age'] > 30, 'Senior', 'Junior')
print("\n4. Adding conditional 'Experience' column:")
print(df)

# 5. Removing a single column
df_no_city = df.drop('City', axis=1)
print("\n5. Removing 'City' column:")
print(df_no_city)

# 6. Removing multiple columns
df_minimal = df.drop(['Active', 'Performance', 'Bonus'], axis=1)
print("\n6. Removing multiple columns:")
print(df_minimal)

# 7. Remove columns in-place
df.drop(['City', 'Active'], axis=1, inplace=True)
print("\n7. Removing multiple columns (inplace=True):")
print(df)
```

### Adding and Removing Rows

```python

data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eva'],
    'Age': [24, 30, 35, 42, 28],
    'City': ['New York', 'Boston', 'Chicago', 'Seattle', 'Miami'],
    'Salary': [65000, 72000, 85000, 92000, 70000],
    'Department': ['HR', 'Sales', 'Tech', 'Tech', 'Finance']
}
df = pd.DataFrame(data)
df.index = ['emp001', 'emp002', 'emp003', 'emp004', 'emp005']  # Custom index

# 1. Removing a row by index label
df_no_bob = df.drop('emp002')
print("\n1. DataFrame without Bob (emp002):")
print(df_no_bob)

# 2. Removing multiple rows
df_reduced = df.drop(['emp001', 'emp005'])
print("\n2. DataFrame without emp001 and emp005:")
print(df_reduced)

# 3. Adding a new row with .loc
# Create a copy to avoid SettingWithCopyWarning
df_new = df.copy()
df_new.loc['emp006'] = ['Frank', 38, 'Dallas', 88000, 'Sales']
print("\n3. DataFrame with new employee:")
print(df_new)

# 4. Adding a row with a Series
new_employee = pd.Series({
    'Name': 'Grace', 'Age': 27, 'City': 'Denver', 'Salary': 67000, 'Department': 'HR',
}, name='emp007')

df_newer = pd.concat([df_new, new_employee.to_frame().T])
print("\n4. DataFrame with another new employee:")
print(df_newer)
```

### Basic Sorting

```python
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eva'],
    'Age': [24, 30, 35, 42, 28],
    'City': ['New York', 'Boston', 'Chicago', 'Seattle', 'Miami'],
    'Salary': [65000, 72000, 85000, 92000, 70000],
    'Department': ['HR', 'Sales', 'Tech', 'Tech', 'Finance']
}
df = pd.DataFrame(data)
df.index = ['emp001', 'emp002', 'emp003', 'emp004', 'emp005']  # Custom index

# Continuing with our employee DataFrame
print("Original DataFrame:")
print(df)

# 1. Sorting by a single column (ascending by default)
df_by_age = df.sort_values('Age')
print("\n1. Sorted by Age (ascending):")
print(df_by_age)

# 2. Sorting by a single column (descending)
df_by_salary_desc = df.sort_values('Salary', ascending=False)
print("\n2. Sorted by Salary (descending):")
print(df_by_salary_desc)

# 3. Sorting by index
df_by_index = df.sort_index()
print("\n3. Sorted by index:")
print(df_by_index)

# 4. Sorting by multiple columns
df_multi_sort = df.sort_values(['Department', 'Salary'])
print("\n4. Sorted by Department, then by Salary within each department:")
print(df_multi_sort)

# 5. Sorting with different directions for each column
df_complex = df.sort_values(['Department', 'Salary'], 
                          ascending=[True, False])
print("\n5. Sorted by Department (asc), then by Salary (desc) within each department:")
print(df_complex)
```

## Indexing, Selection & Slicing in Pandas

### Creating a DataFrame with Meaningful Indices

```python
# Create a DataFrame with custom indices
import pandas as pd

# Create a genetic dataset
genetic_data = {
    'Gene': ['BRCA1', 'TP53', 'APOE', 'PTEN', 'BRAF', 'KRAS', 
            'BRCA2', 'EGFR', 'TNF', 'IL6'],
    'Chromosome': ['Chr17', 'Chr17', 'Chr19', 'Chr10', 'Chr7', 'Chr12', 
                  'Chr13', 'Chr7', 'Chr6', 'Chr7'],
    'Study': ['Study1', 'Study2', 'Study1', 'Study3', 'Study2', 'Study3', 
             'Study1', 'Study2', 'Study3', 'Study1'],
    'PValue': [0.0001, 0.0050, 0.0200, 0.0150, 0.0300, 0.0400, 
              0.0005, 0.0250, 0.0100, 0.0450],
    'EffectSize': [2.5, 1.8, 3.2, 2.1, 1.5, 1.2, 2.7, 1.9, 2.3, 1.1]
}

genetic_df = pd.DataFrame(genetic_data)
print("Genetic DataFrame:")
print(genetic_df)

# Set a meaningful index from an existing column
genetic_df.set_index('Gene', inplace=True)
print("DataFrame with 'Gene' as index:")
print(genetic_df)

# Reset index to return to default integer indexing
df_reset = genetic_df.reset_index()
print("\nDataFrame with default integer index:")
print(df_reset)
```

### Use Label and Position-based Indexing

```python
# Using the genetic_df with 'Gene' as the index

# 1. Label-based indexing with .loc
print("\n1.1. Label-based selection (.loc):")
print("Data for 'BRCA1':")
print(genetic_df.loc['BRCA1'])

# Select multiple rows by label
print("\n1.2. Data for 'TP53' and 'APOE':")
print(genetic_df.loc[['TP53', 'APOE']])

# Select rows and columns by label
print("\n1.3. Chromosome and PValue for 'BRAF' and 'KRAS':")
print(genetic_df.loc[['BRAF', 'KRAS'], ['Chromosome', 'PValue']])

# Slicing dataframe using labels
print("\n1.4. All the rows of Chromosome and PValue columns:")
print(genetic_df.loc[:, ['Chromosome', 'PValue']])
gene_set = ["BRCA1", "BRCA2", "TP53"]
print("\n1.5. row indices in gene_set array and column indices - Study, EffectSize:")
print(genetic_df.loc[["BRCA1","BRAF"], ["Study","EffectSize"]])

# 2. Position-based indexing with .iloc
print("\n2.1. Position-based selection (.iloc):")
print("Third row (index position 2):")
print(genetic_df.iloc[2])

# Select multiple rows by position
print("\n2.2. First and fourth rows (positions 0 and 3):")
print(genetic_df.iloc[[0, 3]])

# Slicing dataframe using indices - Select rows and columns by position
print("\n2.3. Rows 1-3, columns 0-1:")
print(genetic_df.iloc[1:4, 0:2])

# 3. Mixed indexing (direct [])
# Mixing approaches (not recommended but sometimes seen)
# print("\nFirst two rows of 'Study' column:")
# print(genetic_df['Study'][0:2])  # Chained indexing - can lead to issues
```

### Boolean Indexing

```python
# Reset example
genetic_df = pd.DataFrame(genetic_data)
genetic_df.set_index('Gene', inplace=True)
print("Original DataFrame:")
print(genetic_df)

# 1. Simple boolean mask
low_pvalue_mask = genetic_df['PValue'] < 0.01
print("\n1. Boolean mask for low P-values:")
print(low_pvalue_mask)

# Using the mask to filter rows
print("\nGenes with low P-values:")
print(genetic_df[low_pvalue_mask])

# 2. Inline boolean indexing
print("\n2. Genes on Chromosome 7:")
print(genetic_df[genetic_df['Chromosome'] == 'Chr7'])

# 3. Multiple conditions with & (and), | (or)
print("\n3a. Genes from Study1 with large effect size:")
multi_cond_and = (genetic_df['Study'] == 'Study1') & (genetic_df['EffectSize'] > 2.5)
print(genetic_df[multi_cond_and]) # print(genetic_df.loc[multi_cond_and, :])

print("\n3b. Genes with either very low P-value or large effect size:")
multi_cond_or = (genetic_df['PValue'] < 0.005) | (genetic_df['EffectSize'] > 3.0)
print(genetic_df[multi_cond_or]) # print(genetic_df.loc[multi_cond_or, :])

# 4. Using .loc with boolean masks
print("\n4.a Using .loc with boolean mask:")
chr17_genes = (genetic_df['Chromosome'] == 'Chr17')
col_list = ['Study', 'EffectSize']
print(genetic_df.loc[chr17_genes, col_list])
print("\n4.b Using .loc with boolean mask:")
print(genetic_df.loc[multi_cond_and, col_list])
```

## Summary Statistics & Aggregations in Pandas

### Basic Statistical Methods:

```python
import pandas as pd
import numpy as np

# Create a sample gene expression DataFrame
np.random.seed(42)  # For reproducibility

# Generate 15 sample genes
data = {
    'Gene_ID': [f'GENE{i:03d}' for i in range(1, 16)],
    'Expression_Level': np.random.lognormal(4, 1, 15).round(2),  # Draw random samples Log-normal distribution for expression values
    'Log2_Fold_Change': np.random.normal(0, 2, 15).round(2),  # Draw random samples from normal distribution for log2 fold changes
    'P_Value': np.random.beta(1, 10, 15).round(4),  # Draw random samples Beta distribution for p-values
    'Tissue_Type': np.random.choice(['Brain', 'Liver', 'Kidney', 'Heart', 'Lung'], 15),
    'Chromosome': np.random.choice(['chr1', 'chr2', 'chr3', 'chr4', 'chrX', 'chrY'], 15)
}

df = pd.DataFrame(data)

# Add some missing values for realism
df.loc[4, 'P_Value'] = None
df.loc[9, 'Log2_Fold_Change'] = None

# Add a column for significance based on P_Value and Log2_Fold_Change
df['Is_Significant'] = ((df['P_Value'] < 0.05) & (abs(df['Log2_Fold_Change']) > 1))

print("Sample Gene Expression DataFrame:")
print(df)

# 1. Comprehensive statistical summary
print("\n1. Comprehensive statistical summary with describe():")
print(df.describe())

# 2. Include all columns (even non-numeric)
print("\n2. Describing all columns (including non-numeric):")
print(df.describe(include='all'))

# 3. Basic statistical methods
print("\n3. Basic statistical methods:")
print(f"Mean expression level: {df['Expression_Level'].mean():.2f}")
print(f"Median log2 fold change: {df['Log2_Fold_Change'].median():.2f}")
print(f"Minimum p-value: {df['P_Value'].min():.4f}")
print(f"Number of significant genes: {df['Is_Significant'].sum()}")
print(f"Standard deviation of expression: {df['Expression_Level'].std():.2f}")

# 4. Multiple statistics at once
print("\n4. Multiple statistics for Expression Level:")
print(df['Expression_Level'].agg(['min', 'max', 'mean', 'median', 'std']))

# 5. Quantiles/percentiles
print("\n5. Expression level quartiles:")
print(df['Expression_Level'].quantile([0, 0.25, 0.5, 0.75, 1.0]))
```

### Aggregation Functions

```python

# Create a sample gene expression DataFrame
np.random.seed(42)  # For reproducibility

# Generate 15 sample genes
data = {
    'Gene_ID': [f'GENE{i:03d}' for i in range(1, 16)],
    'Expression_Level': np.random.lognormal(4, 1, 15).round(2),  # Log-normal for expression values
    'Log2_Fold_Change': np.random.normal(0, 2, 15).round(2),  # Normal distribution for log2 fold changes
    'P_Value': np.random.beta(1, 10, 15).round(4),  # Beta distribution for p-values
    'Tissue_Type': np.random.choice(['Brain', 'Liver', 'Kidney', 'Heart', 'Lung'], 15),
    'Chromosome': np.random.choice(['chr1', 'chr2', 'chr3', 'chr4', 'chrX', 'chrY'], 15)
}

df = pd.DataFrame(data)
print("Original dataframe")
print(df)

# 1. Simple custom aggregation with custom function

# Define a custom function
def get_range(x):
    """Get range"""
    return x.max() - x.min()

def range_ratio(x):
    """Calculate the ratio of max to min value"""
    return x.max() / x.min()


range_calc = df['Expression_Level'].agg(get_range)
print("\n1. Expression Level range using lambda function:")
print(f"{range_calc:.2f}")

print("\n2. Expression Level max/min ratio using custom function:")
print(f"{df['Expression_Level'].agg(range_ratio):.2f}")

# 3. Different aggregations for different columns
print("\n3. Different aggregations per column:")
mixed_aggs = df.agg({
    'Expression_Level': ['min', 'max', 'mean'],
    'Log2_Fold_Change': ['median', 'std'],
    'P_Value': ['min', 'mean'],
    'Is_Significant': 'sum'
})
print(mixed_aggs)

# 4. Genomics-specific custom aggregation
def differential_expression_score(x):
    """Calculate a custom score based on fold change magnitude and significance"""
    # Higher absolute fold change and lower p-values yield higher scores
    return x.abs().mean() * (-np.log10(df['P_Value'].dropna().mean()))

print("\n4. Custom differential expression score:")
print(f"{df['Log2_Fold_Change'].agg(differential_expression_score):.2f}")
```

### Group dataframes on columns

```python
# Create a genetic dataset
import pandas as pd
import numpy as np

genetic_data = {
    'Gene': ['BRCA1', 'TP53', 'APOE', 'PTEN', 'BRAF', 'KRAS', 
            'BRCA2', 'EGFR', 'TNF', 'IL6'],
    'Chromosome': ['Chr17', 'Chr17', 'Chr19', 'Chr10', 'Chr7', 'Chr12', 
                  'Chr13', 'Chr7', 'Chr6', 'Chr7'],
    'Study': ['Study1', 'Study2', 'Study1', 'Study3', 'Study2', 'Study3', 
             'Study1', 'Study2', 'Study3', 'Study1'],
    'PValue': [0.0001, 0.0050, 0.0200, 0.0150, 0.0300, 0.0400, 
              0.0005, 0.0250, 0.0100, 0.0450],
    'EffectSize': [2.5, 1.8, 3.2, 2.1, 1.5, 1.2, 2.7, 1.9, 2.3, 1.1]
}

genetic_df = pd.DataFrame(genetic_data)
print("Genetic DataFrame:")
print(genetic_df)

# Group by Chromosome
chromosome_groups = genetic_df.groupby('Chromosome')

# View the groups
print("Available groups:")
print(list(chromosome_groups.groups.keys()))

# Access a specific group
print("\nGenes on Chr17:")
print(chromosome_groups.get_group('Chr17'))
```

### Aggregations - The Core of GroupBy

```python
# Calculate mean effect size and p-value for each chromosome
chromosome_stats = genetic_df.groupby('Chromosome').agg({
    'PValue': 'mean',
    'EffectSize': 'mean'
})

print("Mean statistics by chromosome:")
print(chromosome_stats)
```
