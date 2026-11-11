### Algorithm: FIRST_OCCURRENCE_BINARY_SEARCH

```text
FIRST_OCCURRENCE_BINARY_SEARCH(A, n, key)

    low = 0

    high = n - 1

    result = -1

    WHILE low <= high

        mid = low + (high - low) / 2

        IF A[mid].timestamp == key THEN

            result = mid

            high = mid - 1

        ELSE IF A[mid].timestamp < key THEN

            low = mid + 1

        ELSE

            high = mid - 1

        END IF

    END WHILE

    RETURN result

END
```
