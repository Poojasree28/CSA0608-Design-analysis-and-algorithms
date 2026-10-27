## Pseudocode

```text
BRUTE-FORCE-MATCH(text, pattern)
    comparisons = 0

    for shift = 0 to n - m
        j = 0

        while j < m
            comparisons += 1

            if text[shift + j] != pattern[j]:
                break

            j += 1

        if j == m:
            return (shift, comparisons)

    return (NOT_FOUND, comparisons)
```
