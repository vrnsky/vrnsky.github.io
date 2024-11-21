---
title: Decision trees concept
type: docs
sidebar:
  open: true
date: 2024-11-19
---


### Properties of decision tree
- Root node (parent node)
- Internal node (child node)
- Leaf node (terminal node)
- Test condition

### Example
![Decision tree example](https://raw.githubusercontent.com/vrnsky/vrnsky.github.io/refs/heads/main/content/university/data-mining-and-knowledge-discovery/img/decision-tree.png)

### Tree induction
#### Greedy strategy
Split the records based on an attribute test that optimizes certain criterion.
Nodes with **homogeneous** class distribution (low degree of impurity) are preferred.
Need a measure of node impurity.

Entropy:
- Measure homogeneity of a node
- **Maximum** when records are equally distributed among all classes implying the least information.
- **Minimum** when all records belong to one class (of target attribute), implying most information. 

### Notes
Do not use ids for data modeling and prediction.
The higher the entropy/gini/misclassification the lower the purity of a node.
Error value should be less

