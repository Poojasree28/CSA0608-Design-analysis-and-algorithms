## Pseudocode

```text
CLOSEST-PAIR-DIVIDE-AND-CONQUER(points)
    sort points by x; prepare points ordered by y
    if n <= 3:
        return brute-force closest pair
    split points into left and right halves
    dLeft = CLOSEST-PAIR(left)
    dRight = CLOSEST-PAIR(right)
    d = min(dLeft, dRight)
    strip = points whose x-distance from split line is < d
    examine strip in y-order, checking only following points
        whose y-distance is < current best distance
    return the best pair found
```
