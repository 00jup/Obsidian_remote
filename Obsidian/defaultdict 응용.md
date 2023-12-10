## defaultdict 응용 1 function
```python
from collections import defaultdict

# Define a function that will be used as the default factory
def my_func():
    return 'Default Value'

# Create a defaultdict with the custom default factory
dd = defaultdict(my_func)

# Access a key that doesn't exist
print(dd['non_existent_key'])
```

## defaultdict 응용 2 lambda
```python
from collections import defaultdict

# Function to return a defaultdict with float as default factory
def nested_dd():
    return defaultdict(float)

# Create a nested defaultdict for sales data
sales = defaultdict(lambda: defaultdict(nested_dd))

# Add values to the nested defaultdict
sales[2022]['January']['Electronics'] = 12000.50
sales[2022]['January']['Books'] = 3500.25
sales[2022]['February']['Electronics'] = 10500.75
sales[2023]['March']['Books'] = 5000.00

print(sales)
```




[출처](https://likegeeks.com/python-defaultdict/)
