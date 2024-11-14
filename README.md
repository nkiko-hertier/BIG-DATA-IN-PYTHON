# Big Data and Python Example

## What is Big Data?

Big Data refers to datasets that are so large and complex that traditional data-processing software and methods are inadequate to handle them. These datasets are characterized by the following 3Vs:

- **Volume**: Refers to the vast amount of data generated every second. Examples include social media posts, transaction records, sensors data, etc.
- **Velocity**: Refers to the speed at which data is generated, collected, and processed. For example, real-time data processing from stock markets or IoT devices.
- **Variety**: Refers to the different types of data, such as structured data (like tables or CSV files), unstructured data (like videos, images, or text), and semi-structured data (like logs or JSON files).

With the exponential growth of data, efficient data handling and processing techniques like distributed computing and parallel processing are used to process Big Data.

In this example, we work with a small CSV string (representing structured data) and perform basic operations like summing values and calculating averages. Although small, the concept can scale to handle much larger datasets, which is common in Big Data applications.

## Code Explanation

This project consists of two Python files:

1. **`main.py`** - The main script that demonstrates how to work with CSV data, perform calculations, and print results.
2. **`csv_utils.py`** - A utility script that defines a function to convert CSV string data into a list of dictionaries.

### `main.py`

```python
from csv_utils import csv_string_to_dict
```

- **Line 1**: Import the `csv_string_to_dict` function from the `csv_utils.py` file. This function is used to convert a CSV-formatted string into a list of dictionaries, where each dictionary represents a row of data.

```python
csv_string = """customer_id,product_id,quantity,price,date
1,101,2,20,2023-06-01
2,102,1,30,2023-06-01
1,103,3,15,2023-06-02
3,101,2,20,2023-06-02
2,104,1,50,2023-06-03"""
```

- **Line 2-7**: This is a multi-line string representing a sample CSV file. Each line contains data about customer purchases, including:
  - `customer_id`: The ID of the customer.
  - `product_id`: The ID of the purchased product.
  - `quantity`: The number of items purchased.
  - `price`: The price of a single unit of the product.
  - `date`: The date the purchase was made.

```python
data = csv_string_to_dict(csv_string)
```

- **Line 9**: Call the `csv_string_to_dict` function, passing the `csv_string` as an argument. This converts the CSV string into a list of dictionaries, where each dictionary contains keys like `customer_id`, `product_id`, `quantity`, `price`, and `date`.

```python
total_sum = sum(item['price'] * item['quantity'] for item in data)
```

- **Line 11**: Calculate the total sum of money spent across all purchases. For each item in the `data` list (which is a dictionary representing each purchase), it multiplies the `price` and `quantity` values to calculate the total for that purchase. The `sum()` function adds these individual totals together to get the overall total.

```python
average = sum((item['price'] * item['quantity']) / len(data) for item in data)
```

- **Line 13**: Calculate the average amount spent per purchase. It first multiplies `price` and `quantity` to calculate the total amount for each purchase, then divides this total by the total number of rows (`len(data)`). The sum of these averages is computed for the entire dataset.

```python
print(total_sum)
```

- **Line 15**: Prints the `total_sum` value, which is the total money spent across all purchases in the dataset.

### `csv_utils.py`

```python
import csv
from io import StringIO
```

- **Line 1-2**: Import the `csv` module, which is used for reading and writing CSV files, and the `StringIO` module, which allows you to treat a string as a file-like object. `StringIO` is necessary to simulate reading from a file, as we're working with a string instead of an actual file.

```python
def csv_string_to_dict(csv_string):
```

- **Line 4**: Define a function `csv_string_to_dict` that takes a CSV-formatted string (`csv_string`) as input and returns a list of dictionaries.

```python
    csv_data = StringIO(csv_string)
```

- **Line 6**: Create a `StringIO` object from the `csv_string`. This turns the string into an in-memory file-like object, which can be passed to the `csv.DictReader` function for reading.

```python
    reader = csv.DictReader(csv_data)
```

- **Line 8**: Initialize a `csv.DictReader` object, which reads the CSV data as dictionaries. Each row will be parsed into a dictionary where the column headers become keys and the values are the corresponding data in that row.

```python
    result = []
```

- **Line 10**: Initialize an empty list `result`, which will be used to store the dictionaries created from each row in the CSV data.

```python
    for row in reader:
```

- **Line 12**: Loop over each row in the CSV data. `reader` will yield each row as a dictionary with keys like `customer_id`, `product_id`, `quantity`, `price`, and `date`.

```python
        row['price'] = int(row['price'])
        row['quantity'] = int(row['quantity'])
```

- **Line 13-14**: Convert the values of `price` and `quantity` from strings (since CSV data is text) to integers. This allows for mathematical operations to be performed on these values later.

```python
        result.append(row)
```

- **Line 16**: Append the dictionary `row` to the `result` list.

```python
    return result
```

- **Line 18**: Return the `result` list, which now contains dictionaries representing each row of the CSV data, with `price` and `quantity` as integers.

---

## Main.py
```python
from csv_utils import csv_string_to_dict
# Example CSV string
csv_string = """customer_id,product_id,quantity,price,date
1,101,2,20,2023-06-01
2,102,1,30,2023-06-01
1,103,3,15,2023-06-02
3,101,2,20,2023-06-02
2,104,1,50,2023-06-03"""

# Convert the CSV string to a list of dictionaries
data = csv_string_to_dict(csv_string)
# total
total_sum = sum(item['price'] * item['quantity'] for item in data)
 
# average
average= sum((item['price'] * item['quantity'])/len(data) for item in data)

# Print the result
print(total_sum)
```

## csv_utils.py
```python
import csv
from io import StringIO

def csv_string_to_dict(csv_string):
    # Use StringIO to simulate a file-like object from the CSV string
    csv_data = StringIO(csv_string)
    
    # Initialize the CSV reader
    reader = csv.DictReader(csv_data)
    
    # Create a list to store the result
    result = []
    
    # Loop over the rows of the CSV file
    for row in reader:
        # Convert price and quantity to integers
        row['price'] = int(row['price'])
        row['quantity'] = int(row['quantity'])
        
        # Append the row to the result
        result.append(row)
    
    return result

```
## Summary

This example demonstrates how to process a CSV-formatted string using Python. The `csv_utils.py` file provides a utility to convert the CSV string into a list of dictionaries, and the `main.py` file performs calculations like summing total purchases and calculating the average. The core concept of this code can be scaled to handle larger datasets, which is a common requirement in Big Data applications.



