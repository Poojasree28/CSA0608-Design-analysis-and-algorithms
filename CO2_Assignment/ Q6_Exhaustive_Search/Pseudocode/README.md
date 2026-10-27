## Pseudocode

```text id="pck472"
EXHAUSTIVE-PACKING(packages, capacity)
    bestValue = -infinity
    bestSubset = empty

    for mask = 0 to 2^n - 1
        weight = 0
        value = 0
        subset = empty

        for i = 0 to n-1
            if bit i of mask is 1
                add package i to subset
                weight += packages[i].weight
                value += packages[i].value

        if weight <= capacity and value > bestValue
            bestValue = value
            bestSubset = subset

    return bestSubset, bestValue
```

