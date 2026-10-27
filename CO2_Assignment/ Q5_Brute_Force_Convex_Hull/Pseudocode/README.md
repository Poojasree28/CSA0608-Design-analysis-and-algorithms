## Pseudocode

```text id="p9k3xa"
BRUTE-FORCE-HULL(points)
    edges = empty set

    for each unordered pair A, B
        hasPositive = false
        hasNegative = false

        for each point P other than A and B
            z = cross(A, B, P)

            if z > 0:
                hasPositive = true

            if z < 0:
                hasNegative = true

        if not (hasPositive and hasNegative):
            add candidate edge AB

    construct and order the boundary edges
    handle collinear points consistently

    return hull boundary
```

