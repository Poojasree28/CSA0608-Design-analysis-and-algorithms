## Q6 – Median of Medians

### Introduction

Selection finds the k-th smallest element without fully sorting the array. Median of Medians guarantees a sufficiently good pivot by grouping elements into small groups, finding each group's median, and recursively selecting the median of those medians.

### Grouping and Pivot Selection

- Divide the input into groups of five (the final group may contain fewer elements).
- Sort each small group and take its median.
- Recursively select the median of the group medians as the pivot.
- Partition the full array around the pivot.
- Recurse only into the side containing the requested rank; return the pivot if its rank is k.

### Worst-Case Guarantee and Recurrence

The pivot construction guarantees that a constant fraction of elements is discarded in the worst case. A standard upper-bound recurrence is:

```text
T(n) ≤ T(⌈n/5⌉) + T(7n/10 + O(1)) + O(n)
```

This solves to:

```text
T(n) = O(n)
```

Thus, deterministic Median of Medians has worst-case linear selection time.

### Comparison with QuickSelect

| Selection Method | Pivot Choice | Expected / Worst-Case Time | Comment |
|---|---|---|---|
| QuickSelect (random pivot) | Random element | Expected O(n); worst O(n²) | Usually simple and fast; randomisation reduces risk but does not eliminate a bad run. |
| Deterministic poor pivot | First/last element under adversarial order | Can be O(n²) | Repeatedly leaves nearly all elements on one side. |
| Median of Medians | Median of group medians | Worst-case O(n) | More work per pivot, but guarantees progress. |

Pivot quality is central because it determines how much of the array is discarded after each partition. A balanced pivot reduces the remaining problem substantially; a poor pivot can leave almost the entire input for the next recursive call.

### Experiment Design

Test random, sorted, reverse-sorted, and adversarial arrays at:

- n = 100
- n = 500
- n = 1,000
- n = 5,000
- n = 10,000

Compare selected values against `sorted(A)[k-1]`. Instrument partition sizes, comparisons and recursion depth.

Demonstrate deterministic first-element QuickSelect on sorted data, randomized QuickSelect on repeated seeds, and Median of Medians. Randomisation reduces the likelihood of repeated poor partitions but cannot provide a deterministic worst-case guarantee.
