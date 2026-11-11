### Algorithm 1: QUICK_SORT

```text
QUICK_SORT(A, low, high)

    IF low < high THEN

        pivot = MEDIAN_OF_THREE(
                    A[low],
                    A[mid],
                    A[high]
                )

        (lt, gt) = THREE_WAY_PARTITION(
                      A, low, high, pivot
                  )

        QUICK_SORT(A, low, lt - 1)

        QUICK_SORT(A, gt + 1, high)

    END IF

END
```

### Algorithm 2: THREE_WAY_PARTITION

```text
THREE_WAY_PARTITION(A, low, high, pivot)

    lt = low

    i = low

    gt = high

    WHILE i <= gt

        IF A[i] < pivot THEN

            SWAP A[lt] AND A[i]

            lt = lt + 1

            i = i + 1

        ELSE IF A[i] > pivot THEN

            SWAP A[i] AND A[gt]

            gt = gt - 1

        ELSE

            i = i + 1

        END IF

    END WHILE

    RETURN (lt, gt)

END
```
