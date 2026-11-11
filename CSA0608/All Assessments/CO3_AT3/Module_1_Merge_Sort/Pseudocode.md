### Algorithm 1: MERGE_SORT

```text
MERGE_SORT(A, left, right)

    IF left < right THEN

        mid = (left + right) / 2

        MERGE_SORT(A, left, mid)

        MERGE_SORT(A, mid + 1, right)

        MERGE(A, left, mid, right)

    END IF

END
```

### Algorithm 2: MERGE

```text
MERGE(A, left, mid, right)

    Create temporary array TEMP

    i = left

    j = mid + 1

    k = 0

    WHILE i <= mid AND j <= right

        IF A[i].timestamp <= A[j].timestamp THEN

            TEMP[k] = A[i]

            i = i + 1

        ELSE

            TEMP[k] = A[j]

            j = j + 1

        END IF

        k = k + 1

    END WHILE

    Copy remaining elements from left half

    Copy remaining elements from right half

    Copy TEMP into A[left...right]

END
```
