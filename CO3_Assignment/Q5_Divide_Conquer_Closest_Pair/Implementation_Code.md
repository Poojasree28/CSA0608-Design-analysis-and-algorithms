## Q5 – Closest Pair of Points

### Python Code

```python
from math import hypot


def closest_pair_dc(points):

    px = sorted(points)

    py = sorted(points, key=lambda p: p[1])

    def brute(P):

        best = float("inf")

        for i in range(len(P)):

            for j in range(i + 1, len(P)):

                best = min(best, hypot(P[i][0] - P[j][0],
                                       P[i][1] - P[j][1]))

        return best

    def solve(X, Y):

        n = len(X)

        if n <= 3:
            return brute(X)

        mid = n // 2

        leftX, rightX = X[:mid], X[mid:]

        split_x = X[mid][0]

        left_set = set(leftX)

        leftY = [p for p in Y if p in left_set]

        rightY = [p for p in Y if p not in left_set]

        d = min(solve(leftX, leftY), solve(rightX, rightY))

        strip = [p for p in Y if abs(p[0] - split_x) < d]

        best = d

        for i in range(len(strip)):

            for j in range(i + 1, min(i + 8, len(strip))):

                best = min(best, hypot(strip[i][0] - strip[j][0],
                                       strip[i][1] - strip[j][1]))

        return best

    if len(points) < 2:
        return float("inf")

    return solve(px, py)


def closest_pair_bruteforce(points):

    best = float("inf")

    for i in range(len(points)):

        for j in range(i + 1, len(points)):

            best = min(best, hypot(points[i][0] - points[j][0],
                                   points[i][1] - points[j][1]))

    return best


# Getting input from the user

n = int(input("Enter the number of points: "))

if n < 2:

    print("Please enter at least 2 points.")

else:

    pts = []

    for i in range(n):

        x, y = map(float, input(f"Enter coordinates of point {i + 1} (x y): ").split())

        pts.append((x, y))

    dc_result = closest_pair_dc(pts)

    brute_result = closest_pair_bruteforce(pts)

    print("Closest Pair Distance using Divide and Conquer:", dc_result)

    print("Closest Pair Distance using Brute Force:", brute_result)

    print("Both results are equal:", abs(dc_result - brute_result) < 1e-9)
```


```
