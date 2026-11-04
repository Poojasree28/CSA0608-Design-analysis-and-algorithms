## Counting Inversions

### Pseudocode

```text
COUNT-INVERSIONS(A):

    if length(A) <= 1:
        return (A, 0)

    mid = floor(length(A)/2)

    (Lsorted, leftCount) = COUNT-INVERSIONS(A[0:mid])

    (Rsorted, rightCount) = COUNT-INVERSIONS(A[mid:])

    (merged, crossCount) = MERGE-COUNT(Lsorted, Rsorted)

    return (merged, leftCount + rightCount + crossCount)


MERGE-COUNT(L, R):

    i = 0
    j = 0
    count = 0
    output = []

    while i < length(L) and j < length(R):

        if L[i] <= R[j]:
            append L[i]
            i = i + 1

        else:
            append R[j]

            count = count + (length(L) - i)

            j = j + 1

    append remaining elements of L and R

    return (output, count)
```
