# CO-2 ASSIGNMENT

## Assignment Title

Brute-Force and Exhaustive-Search Techniques – Selection Sort, Bubble Sort, Insertion Sort, Sequential Search, Brute-Force String Matching, Closest Pair, Convex Hull and Exhaustive Search.

## Student and Course Details

| Field | Details |
|---|---|
| Course Outcome | CO2 |
| Assignment | CO2 Assignment |
| Faculty | Dr. F. Mary Harin Fernandez |
| Student Name | Pooja Sree M |
| Register Number | 192521403 |
| Course Code | CSA0608 |
| Course Name | Design and Analysis of Algorithm |

---

# Q1 — Sorting Under Different Data Conditions

## Problem Description

Sort e-commerce order priority scores using Selection Sort, Bubble Sort and Insertion Sort. The incoming data can be random, nearly sorted, sorted or highly disordered.

## Algorithm Design

### Selection Sort

1. Divide the array into sorted and unsorted portions.
2. Find the minimum element in the unsorted portion.
3. Swap it with the first element of the unsorted portion.
4. Repeat until all elements are sorted.
5. Count comparisons and swaps to measure performance.

### Bubble Sort

1. Compare adjacent elements in the array.
2. Swap them if they are in the wrong order.
3. Continue each pass until the largest unsorted element reaches its correct position.
4. Stop early if a complete pass performs no swaps.
5. Record comparisons and swaps.

### Insertion Sort

1. Treat the first element as the sorted portion.
2. Select the next element as the key.
3. Shift larger elements to the right until the correct position is found.
4. Insert the key into that position.
5. Repeat until the array is sorted.
6. Record comparisons and movements.

## Design Decision

Test all three algorithms using sorted, reverse-sorted and duplicate-containing datasets. Compare their operation counts and recommend Insertion Sort when approximately 95% of the orders are already sorted and small batches are added.

## Predictions Before Testing

| Algorithm | Prediction | Reason |
|---|---|---|
| Selection Sort | Similar comparison count for every arrangement: n(n−1)/2 | It searches the remaining unsorted portion for the minimum on every pass. |
| Bubble Sort | Fast on sorted/nearly sorted inputs with early termination | It stops after a pass with no swaps, but may perform many adjacent swaps. |
| Insertion Sort | Very fast on nearly sorted inputs | Its work is proportional to the number of inversions. |

## Designed Test Datasets

| Condition | Example Dataset | Purpose |
|---|---|---|
| Already Sorted | `[1, 2, 3, 4, 5, 6]` | Tests early termination and best-case behaviour. |
| Reverse Sorted | `[6, 5, 4, 3, 2, 1]` | Creates many inversions and exposes shifts/swaps. |
| Random Order | `[4, 1, 6, 2, 5, 3]` | Evaluates performance on randomly arranged elements. |
| Nearly Sorted | `[1, 2, 4, 3, 5, 6]` | Tests performance when only a few elements are out of order. |
| Duplicate Values | `[3, 1, 3, 2, 1, 4]` | Checks whether repeated values are handled correctly. |

## Pseudocode

### Selection Sort

```text
SELECTION-SORT(A)
  for i = 0 to n-2
    minIndex = i
    for j = i+1 to n-1
      comparisons += 1
      if A[j] < A[minIndex]
        minIndex = j
    if minIndex != i
      swap A[i], A[minIndex]
      swaps += 1
```

### Bubble Sort

```text
BUBBLE-SORT(A)
  for end = n-1 down to 1
    swapped = false
    for j = 0 to end-1
      comparisons += 1
      if A[j] > A[j+1]
        swap A[j], A[j+1]
        swaps += 1
        swapped = true
    if swapped == false
      break
```

### Insertion Sort

```text
INSERTION-SORT(A)
  for i = 1 to n-1
    key = A[i]
    j = i-1
    while j >= 0
      comparisons += 1
      if A[j] > key
        A[j+1] = A[j]
        moves += 1
        j -= 1
      else
        break
    A[j+1] = key
    moves += 1
```

## Complexity Analysis

| Algorithm | Best Case | Average Case | Worst Case | Auxiliary Space |
|---|---|---|---|---|
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) |
| Bubble Sort (with early termination) | O(n) | O(n²) | O(n²) | O(1) |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) |

## Experimental Evidence

The following values illustrate operation counts for selected input sizes. Actual results depend on the input arrangement and implementation.

| Input Size (n) | Selection Comparisons | Bubble Comparisons | Insertion Comparisons |
|---|---:|---:|---:|
| 10 | 45 | 45 | 29 |
| 50 | 1225 | 1170 | 644 |
| 100 | 4950 | 4884 | 2813 |
| 200 | 19900 | 19522 | 9244 |

## Source Code

```python
import random
import turtle

def selection_sort(a):
    c = 0
    for i in range(len(a) - 1):
        m = i
        for j in range(i + 1, len(a)):
            c += 1
            if a[j] < a[m]:
                m = j
        a[i], a[m] = a[m], a[i]
    return c

def bubble_sort(a):
    c = 0
    for end in range(len(a) - 1, 0, -1):
        changed = False
        for j in range(end):
            c += 1
            if a[j] > a[j + 1]:
                a[j], a[j + 1] = a[j + 1], a[j]
                changed = True
        if not changed:
            break
    return c

def insertion_sort(a):
    c = 0
    for i in range(1, len(a)):
        key = a[i]
        j = i - 1
        while j >= 0:
            c += 1
            if a[j] > key:
                a[j + 1] = a[j]
                j -= 1
            else:
                break
        a[j + 1] = key
    return c

sizes = [10, 50, 100, 200]
sel, bub, ins = [], [], []

random.seed(42)

for n in sizes:
    data = [random.randint(1, 10000) for _ in range(n)]
    sel.append(selection_sort(data.copy()))
    bub.append(bubble_sort(data.copy()))
    ins.append(insertion_sort(data.copy()))

print("Input sizes:", sizes)
print("Selection:", sel)
print("Bubble:", bub)
print("Insertion:", ins)

# Draw graph using turtle
screen = turtle.Screen()
screen.title("Sorting Algorithm Comparisons")
screen.setup(1000, 650)
screen.bgcolor("white")

pen = turtle.Turtle()
pen.speed(0)
pen.hideturtle()
pen.width(3)

left, bottom = -400, -230
graph_width, graph_height = 800, 430
max_value = max(sel + bub + ins) * 1.1

# Draw axes
pen.penup()
pen.goto(left, bottom)
pen.pendown()
pen.goto(left, bottom + graph_height)
pen.goto(left, bottom)
pen.goto(left + graph_width, bottom)

# Axis labels
pen.penup()
pen.goto(0, -290)
pen.write("Input size n", align="center",
          font=("Arial", 14, "normal"))

pen.goto(-450, 230)
pen.write("Comparisons", align="center",
          font=("Arial", 12, "normal"))

# X-axis labels
for n in sizes:
    x = left + (n / 200) * graph_width
    pen.penup()
    pen.goto(x, bottom - 25)
    pen.write(str(n), align="center",
              font=("Arial", 10, "normal"))

# Y-axis labels and grid
for k in range(5):
    value = max_value * k / 4
    y = bottom + graph_height * k / 4
    pen.penup()
    pen.goto(left - 12, y - 5)
    pen.write(str(int(value)), align="right",
              font=("Arial", 9, "normal"))
    pen.goto(left, y)
    pen.pendown()
    pen.goto(left + graph_width, y)
    pen.penup()

def draw_line(values, color, name):
    pen.color(color)
    pen.width(3)
    for i, n in enumerate(sizes):
        x = left + (n / 200) * graph_width
        y = bottom + (values[i] / max_value) * graph_height
        if i == 0:
            pen.penup()
            pen.goto(x, y)
            pen.pendown()
        else:
            pen.goto(x, y)
        pen.dot(9)

# Draw three sorting lines
draw_line(sel, "blue", "Selection")
draw_line(bub, "orange", "Bubble")
draw_line(ins, "green", "Insertion")

# Graph title
pen.penup()
pen.goto(0, 270)
pen.color("black")
pen.write("Q1: Comparisons on random data",
          align="center",
          font=("Arial", 18, "normal"))

# Legend
for i, (color, name) in enumerate([
    ("blue", "Selection"),
    ("orange", "Bubble"),
    ("green", "Insertion")
]):
    pen.goto(260, 240 - i * 25)
    pen.color(color)
    pen.pendown()
    pen.forward(25)
    pen.penup()
    pen.forward(8)
    pen.color("black")
    pen.write(name, font=("Arial", 11, "normal"))

turtle.done()
```



## Observation and Design Decision

Selection Sort performs a predictable number of comparisons regardless of input order. Bubble Sort with early termination is useful for already-sorted data but can perform many swaps on reverse-sorted data. Insertion Sort is suitable for small batches added to an already-sorted list.

Therefore, Insertion Sort is recommended for maintaining order when approximately 95% of the data is already sorted.

---

# Q2 — Sequential Search

## Problem Description

Consider a frequently changing list of aircraft maintenance tools. Each record contains a Tool ID, Technician ID, Issue Time and Work Bay.

The objective is to search for a particular Tool ID and measure the number of comparisons required to find it.

## Algorithm Design

1. Accept the list of tool records and the target Tool ID.
2. Initialize the comparison counter to zero.
3. Start searching from the first record.
4. Compare each record's Tool ID with the target.
5. Increment the comparison counter after each comparison.
6. If a match is found, return the corresponding technician and tool details.
7. If the target is not found, continue until the list ends.
8. If the entire list is checked, return `NOT FOUND`.
9. Repeat the experiment with successful and unsuccessful searches.
10. Compare operation counts for different list sizes.

## Pseudocode

```text
SEQUENTIAL-SEARCH(records, targetToolID)
  comparisons = 0

  for i = 0 to length(records)-1
    comparisons += 1
    if records[i].ToolID == targetToolID
      return (records[i], comparisons)

  return (NOT_FOUND, comparisons)
```

## Test Results

| List Size | Successful: First | Successful: Middle | Successful: Last | Unsuccessful |
|---|---:|---:|---:|---:|
| 10 | 1 | 5 | 10 | 10 |
| 100 | 1 | 50 | 100 | 100 |
| 1000 | 1 | 500 | 1000 | 1000 |

## Complexity Analysis

- Best Case: O(1)
- Average Case: O(n)
- Worst Case: O(n)
- Auxiliary Space: O(1)

## Python Implementation

```python
def sequential_search(records, target):
    comparisons = 0

    for record in records:
        comparisons += 1

        if record['tool_id'] == target:
            return record, comparisons

    return None, comparisons


if __name__ == '__main__':
    tools = [
        {
            'tool_id': f'T-{i:03}',
            'technician': f'TECH-{i % 4 + 1}',
            'issue_time': '10:00',
            'work_bay': f'BAY-{i % 3 + 1}'
        }
        for i in range(101, 111)
    ]

    targets = ['T-101', 'T-105', 'T-110', 'T-999']

    for target in targets:
        record, count = sequential_search(tools, target)

        print(
            target,
            'FOUND' if record else 'NOT_FOUND',
            'comparisons =', count
        )
```

## Engineering Decision

Sequential Search is appropriate for small, frequently changing lists and infrequent lookups. For larger lists across multiple facilities, an indexed lookup structure or database index is more appropriate.

---

# Q3 — Brute-Force String Matching

## Problem Description

Search security logs for a known event signature. The algorithm tries every possible alignment of a pattern in the text and compares characters from left to right.

## Algorithm Design

1. Accept the log text and pattern.
2. Calculate the lengths of the text and pattern.
3. Align the pattern with the beginning of the text.
4. Compare corresponding characters from left to right.
5. Count every character comparison.
6. If a mismatch occurs, shift the pattern one position to the right.
7. If every character matches, return the starting position.
8. Continue until all possible alignments have been examined.
9. If no match is found, return `NOT FOUND`.
10. Compare actual and predicted character comparison counts.

## Pseudocode

```text
BRUTE-FORCE-MATCH(text, pattern)
  comparisons = 0

  for shift = 0 to n-m
    j = 0

    while j < m
      comparisons += 1

      if text[shift+j] != pattern[j]
        break

      j += 1

    if j == m
      return (shift, comparisons)

  return (NOT_FOUND, comparisons)
```

## Test Cases

| Case | Text | Pattern | Expected Result |
|---|---|---|---|
| Early Match | `security-alert` | `sec` | Match at index 0 |
| Repeated Prefix | `AAAAAAAAAAAB` | `AAAAB` | Match near the end |
| Not Found | `AAAAAAAAAA` | `AAAB` | No match |

## Complexity Analysis

Let `n` be the text length and `m` be the pattern length.

- Best Case: O(m)
- Average Case: O(nm)
- Worst Case: O(nm)
- Auxiliary Space: O(1)

## Python Implementation

```python
def brute_force_match(text, pattern):
    comparisons = 0

    for shift in range(len(text) - len(pattern) + 1):
        j = 0

        while j < len(pattern):
            comparisons += 1

            if text[shift + j] != pattern[j]:
                break

            j += 1

        if j == len(pattern):
            return shift, comparisons

    return -1, comparisons


tests = [
    ('security-alert', 'sec'),
    ('AAAAAAAAAAAB', 'AAAAB'),
    ('AAAAAAAAAA', 'AAAB')
]

for text, pattern in tests:
    index, count = brute_force_match(text, pattern)

    print(
        repr(text),
        repr(pattern),
        'index =', index,
        'comparisons =', count
    )
```

## Observation

The number of character comparisons depends on text length, pattern length, repeated prefixes, mismatch position and match position.

---

# Q4 — Brute-Force Closest Pair

## Problem Description

Given `n` drone coordinates `(x, y)`, examine every unique pair and find the pair with the minimum Euclidean distance.

## Algorithm Design

1. Accept the coordinates of all drones.
2. Initialize the minimum distance to infinity.
3. Generate every unique pair of drones.
4. Avoid duplicate comparisons by considering only pairs where the second index is greater than the first.
5. Calculate the Euclidean distance:

   `d = √((x₂ − x₁)² + (y₂ − y₁)²)`

6. Count each pair examined and each distance calculation.
7. Compare the calculated distance with the current minimum.
8. If it is smaller, update the minimum distance and closest pair.
9. Repeat until all unique pairs have been checked.
10. Display the closest pair, minimum distance and total calculations.

## Pseudocode

```text
CLOSEST-PAIR(points)
  bestDistance = infinity
  bestPair = NONE
  pairCount = 0

  for i = 0 to n-2
    for j = i+1 to n-1
      pairCount += 1

      d = sqrt(
        (x[i]-x[j])^2 + (y[i]-y[j])^2
      )

      if d < bestDistance
        bestDistance = d
        bestPair = (i,j)

  return bestPair, bestDistance, pairCount
```

## Experimental Growth

| Number of Points | Unique Pairs | Distance Calculations |
|---|---:|---:|
| 10 | 45 | 45 |
| 100 | 4950 | 4950 |
| 1000 | 499500 | 499500 |

## Complexity Analysis

- Time Complexity: O(n²)
- Auxiliary Space: O(1), excluding the input.

The algorithm becomes inefficient for large datasets because it examines every possible pair.

## Python Implementation

```python
from math import hypot, inf


def closest_pair(points):
    best_distance = inf
    best_pair = None
    pair_count = 0

    for i in range(len(points) - 1):
        for j in range(i + 1, len(points)):
            pair_count += 1

            d = hypot(
                points[i][0] - points[j][0],
                points[i][1] - points[j][1]
            )

            if d < best_distance:
                best_distance = d
                best_pair = (points[i], points[j])

    return best_pair, best_distance, pair_count


points = [
    (0, 0),
    (5, 5),
    (2, 2),
    (9, 1),
    (2, 3)
]

pair, distance, count = closest_pair(points)

print("Closest pair:", pair)
print("Minimum distance:", round(distance, 2))
print("Pairs checked:", count)
```

## Observation

Brute-force closest pair is suitable for small datasets. For larger datasets, a divide-and-conquer algorithm can reduce unnecessary distance calculations.

---

# Q5 — Brute-Force Convex Hull

## Problem Description

Monitoring stations are represented as points in a plane. The convex hull is the smallest convex boundary containing all stations.

## Algorithm Design

1. Accept the coordinates of all monitoring stations.
2. Select every possible pair of distinct points as a candidate boundary edge.
3. Examine every remaining point.
4. Calculate the orientation using the cross-product expression:

   `C = (xB − xA)(yP − yA) − (yB − yA)(xP − xA)`

5. Determine whether each point lies on the positive side, negative side or directly on the line.
6. If points exist on both sides of the line, reject the candidate edge.
7. Otherwise, retain the pair as a supporting-line candidate.
8. Handle collinear points and remove duplicate candidate edges.
9. Arrange accepted boundary edges in order.
10. Visualize and validate the convex hull.

## Pseudocode

```text
BRUTE-FORCE-HULL(points)
  edges = empty set

  for each unordered pair A, B
    hasPositive = false
    hasNegative = false

    for each point P other than A and B
      z = cross(A, B, P)

      if z > 0
        hasPositive = true

      if z < 0
        hasNegative = true

    if not (hasPositive and hasNegative)
      add candidate edge AB

  construct and order the boundary edges
  handle collinear points consistently

  return hull boundary
```

## Test Configurations

| Test | Point Set | Purpose |
|---|---|---|
| Interior Points | `[(0,0),(4,0),(4,4),(0,4),(2,2),(1,2)]` | Tests whether interior points are excluded. |
| Collinear Edge Points | `[(0,0),(2,0),(4,0),(4,3),(0,3),(2,1)]` | Tests collinearity handling. |

## Complexity Analysis

- Time Complexity: O(n³)
- Auxiliary Space: O(n²) in the worst case for candidate-edge storage.

A production implementation must handle collinear points, duplicate edges and boundary ordering correctly.

## Python Implementation

```python
def cross(a, b, p):
    return (
        (b[0] - a[0]) * (p[1] - a[1])
        - (b[1] - a[1]) * (p[0] - a[0])
    )


def brute_force_hull_edges(points):
    edges = []
    n = len(points)

    for i in range(n):
        for j in range(i + 1, n):
            positive = False
            negative = False

            for k in range(n):
                if k == i or k == j:
                    continue

                z = cross(points[i], points[j], points[k])

                if z > 0:
                    positive = True
                elif z < 0:
                    negative = True

                if positive and negative:
                    break

            if not (positive and negative):
                edges.append((points[i], points[j]))

    return edges


points = [
    (0, 0),
    (4, 0),
    (4, 4),
    (0, 4),
    (2, 2),
    (1, 2)
]

edges = brute_force_hull_edges(points)

print("Supporting-line candidate edges:")

for edge in edges:
    print(edge)
```

## Observation

The supporting-line test identifies potential convex hull edges. Collinear points can create multiple candidate pairs on the same boundary line, so the final hull requires deduplication and consistent ordering.

---

# Q6 — Exhaustive Search and Combinatorial Growth

## Problem Description

Choose packages for a humanitarian airlift. Each package has a weight and humanitarian value. Total weight must not exceed payload capacity, and total value must be maximized.

## Algorithm Design

1. Accept the packages, weights, values and payload capacity.
2. Represent each possible package combination as a subset.
3. Generate every possible subset, including the empty subset.
4. Calculate the total weight and total value of each subset.
5. Reject subsets exceeding the payload capacity.
6. Compare each feasible subset with the best value found so far.
7. Update the best subset when a better value is found.
8. Continue until every subset has been examined.
9. Return the package combination with the highest feasible value.
10. Compare the number of subsets examined with `2ⁿ`.

## Pseudocode

```text
EXHAUSTIVE-PACKING(packages, capacity)
  bestValue = -infinity
  bestSubset = empty

  for mask = 0 to 2^n - 1
    weight = 0
    value = 0
    subset = empty

    for i = 0 to n-1
      if bit i of mask is 1
        add package i to subset
        weight += packages[i].weight
        value += packages[i].value

    if weight <= capacity and value > bestValue
      bestValue = value
      bestSubset = subset

  return bestSubset, bestValue
```

## Test Dataset

| Package | Weight | Value |
|---|---:|---:|
| P1 | 2 | 6 |
| P2 | 3 | 8 |
| P3 | 4 | 9 |
| P4 | 5 | 10 |

**Capacity = 7**

There are `2⁴ = 16` subsets. The optimal selection is P2 + P3, with total weight 7 and total value 17.

## Growth Analysis

| Number of Packages | Subsets Examined | Upper Bound on Subset-Item Checks |
|---|---:|---:|
| 4 | 16 | 64 |
| 10 | 1024 | 10240 |
| 15 | 32768 | 491520 |
| 20 | 1048576 | 20971520 |

## Complexity Analysis

- Time Complexity: O(n × 2ⁿ)
- Auxiliary Space: O(n)

The number of subsets doubles whenever one additional package is added.

## Python Implementation

```python
def exhaustive_packing(packages, capacity):
    n = len(packages)

    best_value = -1
    best_weight = 0
    best_mask = 0

    for mask in range(1 << n):
        weight = 0
        value = 0

        for i, (w, v) in enumerate(packages):
            if mask & (1 << i):
                weight += w
                value += v

        if weight <= capacity and value > best_value:
            best_value = value
            best_weight = weight
            best_mask = mask

    chosen = [
        i for i in range(n)
        if best_mask & (1 << i)
    ]

    return chosen, best_weight, best_value


packages = [
    (2, 6),
    (3, 8),
    (4, 9),
    (5, 10)
]

capacity = 7

chosen, weight, value = exhaustive_packing(
    packages,
    capacity
)

print("Chosen package indices:", chosen)
print("Total weight:", weight)
print("Total value:", value)
print("Capacity:", capacity)
```

## Observation

Exhaustive search guarantees an optimal solution when every subset is evaluated. However, exponential growth makes it unsuitable for sufficiently large datasets. Dynamic programming and branch-and-bound are possible alternatives.

---

# Q7 — Day-4 Design Challenge: Diagnose, Redesign and Validate

## Problem Description

The selected limitation is Brute-Force Closest Pair. It is a significant bottleneck because it examines every pair, resulting in Θ(n²) distance calculations.

## A. Diagnose the Computational Bottleneck

- For n points, the number of distance calculations is `n(n−1)/2`.
- At n = 100, there are 4,950 pairs.
- At n = 1,000, there are 499,500 pairs.
- At n = 10,000, there are 49,995,000 pairs.
- The algorithm evaluates candidate pairs without exploiting spatial order or distance bounds.

## B. Define the Design Objective

Reduce distance calculations substantially compared with `n(n−1)/2` while returning the same minimum distance.

The target time complexity is O(n log n) for a standard divide-and-conquer closest-pair algorithm.

## C. Revised Computational Strategy

Use the divide-and-conquer closest-pair algorithm.

1. Sort the points by x-coordinate.
2. Divide the points into left and right halves.
3. Solve each half recursively.
4. Select the smaller of the two minimum distances.
5. Construct a vertical strip around the dividing line.
6. Examine nearby points in y-coordinate order.
7. Return the closest pair.

## Pseudocode

```text
CLOSEST-PAIR-DIVIDE-AND-CONQUER(points)
  sort points by x
  prepare points ordered by y

  if n <= 3
    return brute-force closest pair

  split points into left and right halves

  dLeft = CLOSEST-PAIR(left)
  dRight = CLOSEST-PAIR(right)

  d = min(dLeft, dRight)

  strip = points whose x-distance from split line is < d

  examine strip in y-order
  check only following points whose y-distance
  is less than the current best distance

  return the best pair
```

## D. Prediction Before Implementing

The redesigned strategy should return the same minimum distance while performing fewer distance calculations as the number of points increases.

## E. Python Implementation

```python
from math import hypot, inf


def divide_closest(points):
    points = sorted(points, key=lambda p: (p[0], p[1]))

    if len(points) <= 3:
        best = inf
        pair = None
        count = 0

        for i in range(len(points)):
            for j in range(i + 1, len(points)):
                count += 1

                d = hypot(
                    points[i][0] - points[j][0],
                    points[i][1] - points[j][1]
                )

                if d < best:
                    best, pair = d, (points[i], points[j])

        return pair, best, count

    mid = len(points) // 2
    mid_x = points[mid][0]

    lp, ld, lc = divide_closest(points[:mid])
    rp, rd, rc = divide_closest(points[mid:])

    if ld <= rd:
        best, pair = ld, lp
    else:
        best, pair = rd, rp

    count = lc + rc

    strip = sorted(
        [
            p for p in points
            if abs(p[0] - mid_x) < best
        ],
        key=lambda p: p[1]
    )

    for i in range(len(strip)):
        j = i + 1

        while (
            j < len(strip)
            and strip[j][1] - strip[i][1] < best
        ):
            count += 1

            d = hypot(
                strip[i][0] - strip[j][0],
                strip[i][1] - strip[j][1]
            )

            if d < best:
                best, pair = d, (strip[i], strip[j])

            j += 1

    return pair, best, count


points = [
    (0, 0),
    (5, 5),
    (2, 2),
    (9, 1),
    (2, 3)
]

pair, distance, comparisons = divide_closest(points)

print("Points:", points)
print("Closest pair:", pair)
print("Minimum distance:", round(distance, 2))
print("Distance comparisons:", comparisons)
```

## F. Defend the Final Design

### Evaluation

The divide-and-conquer method is intended to reduce the number of distance calculations compared with brute force.

### Measured Improvement

Record the actual results obtained by running both algorithms on identical datasets.

| Number of Points | Brute-Force Distance Calculations | Divide-and-Conquer Calculations |
|---|---:|---:|
| 10 | 45 | Record actual result |
| 100 | 4950 | Record actual result |
| 1000 | 499500 | Record actual result |

### Trade-Offs

The redesigned method requires sorting, additional memory and a more complex implementation. The dividing line, strip comparisons and equal-distance cases must be handled correctly.

### When Is Brute Force Still Suitable?

Brute force remains useful for very small datasets because it is simple to implement, easy to understand and straightforward to verify.

### Final Conclusion

The redesign aims to reduce unnecessary distance calculations while preserving the minimum distance. Validate both algorithms on identical datasets before claiming measured improvements.

---

# Overall Recommendations

1. Use Insertion Sort for maintaining a mostly sorted list when small batches are added.
2. Use Sequential Search for small lists and consider indexed lookups for larger systems.
3. Use brute-force string matching as a simple baseline, but consider advanced matching methods for large logs.
4. Use brute-force closest pair only for small point sets; consider divide-and-conquer for larger sets.
5. Use the supporting-line principle for the convex hull and explicitly handle collinear points and edge ordering.
6. Use exhaustive search when the number of subsets is small enough to evaluate within the required time limit.
7. Validate redesigned algorithms using identical test cases and compare operation counts, not just elapsed time.
