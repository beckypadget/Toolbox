Matplotlib figures are confusing so here are some templates.

➡️ Remember to import `matplotlib` as `plt` first.

```python
import matplotlib.pyplot as plt
import numpy as np
```

# Line plot (single panel, single line)

```python
x = np.array([])
y = np.array([])

fig, ax = plt.subplots(figsize=(8, 5))

ax.plot(
    x, y,
    label="Dataset",
    color="steelblue",
    linestyle="-",
    linewidth=2,
    marker="o"
)

ax.set_xlabel("X-axis label")
ax.set_ylabel("Y-axis label")
ax.set_title("Line Plot Title")

ax.grid(True, linestyle="--", alpha=0.5)
ax.legend()

fig.tight_layout()
plt.show()

```

Template code produced by ChatGPT.