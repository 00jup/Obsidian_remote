```python
def is_prime(num):
    for divider in range(2, num):
        if num % divider == 0:
            return False
    return True
```

이거임


```python
def is_prime(num):
    for divider in range(2, num):
        if num % divider == 0:
            return False
	    return True
```

이거 아님....