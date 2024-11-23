---
title: Decision trees practice
type: docs
sidebar:
  open: true
prev: decision-trees-concept
math: true
---

### What to measure?
- Entropy - measures the uncertainty of randomness in our data
- Gini index measures the probability of incorrect classification
- Both are used to evaluate how well a split separates classes


### Practice
In our sample dataset we have - 3 setosa samples, 3 versicolor samples, 4 virginica samples

To calculate entropy:

$$
-\sum(p * \log_2(p))
$$
where $p$ is probability of each class. So for each class
- setosa: $-(\frac{3}{10} * log_2(\frac{3}{10}))$
- versicolor: $-(\frac{3}{10} * log_2(\frac{3}{10}))$
- virginica: $-(\frac{4}{10} * log_2(\frac{4}{10}))$

Then sum calculated values to get final entropy.

To calculate Gini:
Formula is: $1 - \sum(p^2)$, where $p$ probability of each class. For each class
- setosa: $(\frac{3}{10})^2$
- versicolor: $(\frac{3}{10})^2$
- virginica: $(\frac{4}{10})^2$

Then subtract sum from 1 to get final gini index

```python {filename="decision-trees-practice.py"}
import pandas as pd
from math import log2


data = {
    'species': [
        'setosa', 'setosa', 'setosa',
        'versicolor', 'versicolor', 'versioclor',
        'virginica', 'virginica', 'virginica', 'virginica'

    ]
}

df = pd.DataFrame(data)

class_counts = df['species'].value_counts()
total_samples = len(df)
probabilities = class_counts / total_samples

print("Dataset Distribution")
print(class_counts)
print("\nProbabilities")
print(probabilities)

entropy = -sum(p * log2(p) for p in probabilities)
print(f"\nEntropy = {entropy:.4f}")

gini = 1 - sum(p ** 2 for p in probabilities)
print(f"\nGini = {gini:.4f}")

```

The output of code above:
```text
Dataset Distribution
species
virginica     4
setosa        3
versicolor    2
versioclor    1
Name: count, dtype: int64

Probabilities
species
virginica     0.4
setosa        0.3
versicolor    0.2
versioclor    0.1
Name: count, dtype: float64

Entropy = 1.8464

Gini = 0.7000
```