## Pseudocode

```text id="cpa891"
CLOSEST-PAIR(points)
    bestDistance = infinity
    bestPair = NONE
    pairCount = 0

    for i = 0 to n-2
        for j = i+1 to n-1
            pairCount += 1
            d = sqrt((x[i]-x[j])^2 + (y[i]-y[j])^2)

            if d < bestDistance:
                bestDistance = d
                bestPair = (i, j)

    return bestPair, bestDistance, pairCount
```

