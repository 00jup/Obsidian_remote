
```python
class Coord:
    def __init__(self, *values):
        self.values = tuple(values)

    def __repr__(self):
        return str(self.values)

    def __add__(self, coord):
        new_values = list(self.values)
        for i in range(len(self.values)):
            print(f"{new_values[i]} += {coord.values[i]}")
            new_values[i] += coord.values[i]
        new_coord = Coord(*new_values)

        return new_coord


x = Coord(1, 2)
y = Coord(3, 4)
print(x+y)

```
