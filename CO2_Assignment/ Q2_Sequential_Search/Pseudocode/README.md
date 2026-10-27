## Pseudocode

```text
SEQUENTIAL-SEARCH(records, targetToolID)
    comparisons = 0

    for i = 0 to length(records) - 1
        comparisons += 1

        if records[i].ToolID == targetToolID
            return (records[i], comparisons)

    return (NOT_FOUND, comparisons)
```

