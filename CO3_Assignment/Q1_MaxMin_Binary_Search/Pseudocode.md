## Part A – Finding Maximum and Minimum

### Pseudocode


```text
MAXMIN(A, low, high):

    if low == high:
        return (A[low], A[low])

    if high == low + 1:
        if A[low] < A[high]:
            return (A[low], A[high])
        else:
            return (A[high], A[low])

    mid = floor((low + high) / 2)

    (minL, maxL) = MAXMIN(A, low, mid)
    (minR, maxR) = MAXMIN(A, mid + 1, high)

    return (min(minL, minR), max(maxL, maxR))

    return NOT-FOUND
```


## Part B – Binary Search

### Pseudocode

```text
BINARY-SEARCH(A, target):

    low = 0
    high = length(A) - 1

    while low <= high:

        mid = floor((low + high) / 2)

        if A[mid] == target:
            return mid

        else if target < A[mid]:
            high = mid - 1

        else:
            low = mid + 1

    return NOT-FOUND
```
