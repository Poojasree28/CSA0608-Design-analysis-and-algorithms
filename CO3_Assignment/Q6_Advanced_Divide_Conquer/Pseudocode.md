## Part A – Median of Medians

### Pseudocode

```text
SELECT(A, k):

    if length(A) <= 5:
        sort A
        return A[k-1]

    divide A into groups of at most 5

    medians = median of each sorted group

    pivot = SELECT(medians, ceil(length(medians)/2))

    partition A into L (< pivot), E (= pivot), G (> pivot)

    if k <= length(L):
        return SELECT(L, k)

    if k <= length(L) + length(E):
        return pivot

    return SELECT(G, k - length(L) - length(E))
```

## Part B – Meet-in-the-Middle Subset Sum

### Pseudocode

```text
SUBSET-SUM-MITM(A, target):

    split A into L and R

    leftSums = all subset sums of L

    rightSums = all subset sums of R

    store rightSums in a hash set

    for x in leftSums:

        if target - x is in rightSums:
            return TRUE

    return FALSE
```
