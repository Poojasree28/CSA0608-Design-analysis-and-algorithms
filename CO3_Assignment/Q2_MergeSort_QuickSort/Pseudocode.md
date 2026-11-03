## Q2 – Merge Sort and Quick Sort

### Part A – Merge Sort

#### Pseudocode

```text
MERGE-SORT(A):

    if length(A) <= 1:
        return A

    split A into left and right halves

    left_sorted = MERGE-SORT(left)

    right_sorted = MERGE-SORT(right)

    return MERGE(left_sorted, right_sorted)


MERGE(L, R):

    create empty result

    compare the first unused item of L and R

    append the smaller item; advance that input

    append all remaining items

    return result
```

### Part B – Quick Sort

#### Pseudocode

```text
QUICK-SORT(A, low, high):

    if low < high:

        p = PARTITION(A, low, high)  // last element is pivot

        QUICK-SORT(A, low, p - 1)

        QUICK-SORT(A, p + 1, high)


PARTITION(A, low, high):

    pivot = A[high]

    i = low - 1

    for j from low to high - 1:

        if A[j] <= pivot:

            i = i + 1

            swap A[i], A[j]

    swap A[i + 1], A[high]

    return i + 1
```
