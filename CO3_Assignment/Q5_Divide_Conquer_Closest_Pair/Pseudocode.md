## Q5 – Closest Pair of Points

### Pseudocode

```text
CLOSEST-PAIR(P):

    sort P by x; also prepare y-sorted order

    return CLOSEST(Px, Py)


CLOSEST(Px, Py):

    if number of points <= 3:
        return brute_force_closest_pair(Px)

    split Px into left and right at median x

    partition Py into corresponding leftY and rightY

    dL = CLOSEST(leftX, leftY)

    dR = CLOSEST(rightX, rightY)

    delta = min(dL, dR)

    strip = points in Py with abs(x - dividing_x) < delta

    best = delta

    for each strip point in y-order:

        compare it with only the next at most 7 strip points

        update best distance

    return best
```
