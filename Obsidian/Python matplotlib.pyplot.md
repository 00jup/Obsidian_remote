

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.random.random((100, 2))

fig, ax = plt.subplots()
color = ['r' if value > 0.5 else 'b' for value in x[:, 0]]

ax.scatter(x[:, 0], x[:, 1], s=5, c=color)

ax.set_title("1_assignment")
ax.set_xlim([0, 1])
ax.set_ylim([0, 1])
ax.set_xticks([0, 0.5, 1])
ax.set_yticks([0, 0.5, 1])
plt.show()


이 코드에서 점 200개 찍히지?
```


점 200개가 아니라 100개가 찍힌다는 거임!!