

# CO-3 ASSIGNMENT

**Course Outcome:** CO3 – Design Divide and Conquer algorithms for Merge Sort, Quick Sort, Binary Search and Matrix Multiplication

**CO3 Coverage:** DIVIDE AND CONQUER: Introduction- Finding the maximum and minimum-Merge sort-Quick sort-Binary Search-Strassen’s Matrix Multiplication-Karatsuba Algorithm for Multiplication-Closest Pair of Points-Median of Medians-Meet In Middle Technique- Advantages, and Disadvantages of Divide and Conquer.

| Details | Information |
|---|---|
| Course Outcome | CO3 |
| Assignment | Assignment tool |
| Faculty | Dr. F. Mary Harin Fernandez |
| Student Name | Pooja Sree M |
| Register Number | 192521403 |
| Course Code | CSA0608 |
| Course Name | Design and Analysis of Algorithm |

## 1. Introduction to Divide and Conquer

Divide and Conquer is an algorithm design technique that solves a problem by dividing it into smaller subproblems of the same or related type, solving those subproblems recursively, and combining their results. A correct design identifies a base case, a decomposition rule, the information returned by each recursive call, and a combine operation.

Divide and Conquer is one of the most important and widely used techniques in algorithm design. It is a problem-solving approach that helps solve complex problems by breaking them into smaller and simpler subproblems. Instead of solving the entire problem at once, the technique divides the main problem into manageable parts, solves each part independently, and combines the results to obtain the final solution.

The main idea behind Divide and Conquer is to reduce the complexity of a problem and make the solution more efficient. It mainly follows three important steps: Divide, Conquer, and Combine.

1. **Divide:** The original problem is divided into two or more smaller subproblems of the same type.
2. **Conquer:** Each subproblem is solved independently, usually using recursion. If a subproblem is small enough, it is solved directly.
3. **Combine:** The solutions obtained from the smaller subproblems are combined to produce the final result.

This technique is commonly used in computer science because it can reduce the time required to solve large problems. Many efficient algorithms are developed using this approach. It is especially useful when a problem can be divided into independent parts and the results can be combined easily.

Divide and Conquer also helps programmers understand the structure of a problem clearly. By solving smaller parts separately, the algorithm becomes easier to design, implement, test, and analyse. Recursion plays an important role in this technique because the same process is repeatedly applied to smaller versions of the original problem.

Different algorithms based on the Divide and Conquer technique are studied and implemented. These include finding Maximum and Minimum elements, Binary Search, Merge Sort, Quick Sort, Karatsuba Multiplication, Strassen's Matrix Multiplication, Closest Pair of Points, Median of Medians, and Meet-in-the-Middle techniques.

Performance analysis is also an important part of this assignment. The algorithms are evaluated based on their execution time, number of operations, and efficiency for different datasets. Tables and graphs can be used to represent the experimental results and compare the performance of different approaches.

### 1.1 General design pattern

```text
D AND C(problem):
    if problem is small enough:
        return solve_directly(problem)
    divide problem into smaller subproblems
    solve each subproblem recursively
    combine the returned results
    return combined result
```

### 1.2 Recurrence and complexity

A common recurrence is T(n) = aT(n/b) + f(n), where a is the number of recursive subproblems, n/b is the approximate size of each subproblem, and f(n) is the work for dividing and combining. The recurrence is solved using a recursion tree, substitution, or the Master Theorem when its conditions apply.

- **Advantages:** often reduces a large search space, supports clear recursive structure, can expose parallelism, and may improve asymptotic time.
- **Disadvantages:** recursive calls add stack and function-call overhead; combining results can be expensive; extra memory may be required; unbalanced decomposition can remove the expected benefit.
- **Good candidates** have manageable base cases, substantially smaller subproblems, and an efficient combine step.

---

## Q1 – Decomposition and Elimination in Ordered Data

### Part A – Finding Maximum and Minimum

**Goal:** find both the largest and smallest elements of an array using a Divide-and-Conquer/tournament strategy. Each recursive call returns a pair (minimum, maximum).

#### Algorithm design and decomposition

- **Base case:** for one element, that element is both minimum and maximum. For two elements, compare them once and return them in the correct order.
- **Divide:** split the array into left and right halves.
- **Conquer:** recursively find the minimum and maximum in each half.
- **Combine:** compare the two local minima once and the two local maxima once.

**Decomposition example for A = [8, 3, 11, 5]:**

```text
    [8, 3, 11, 5]
       /           \
    [8, 3]        [11, 5]
    /   \          /   \
  [8]   [3]      [11]  [5]
    \   /          \   /
(min=3,max=8)  (min=5,max=11)
          \       /
     (min=3,max=11)
```

#### Pseudocode

```text
MAXMIN(A, low, high):
    if low == high:
        return (A[low], A[low])
    if high == low + 1:
        if A[low] < A[high]:
            return (A[low], A[high])
        else:
            return (A[high], A[low])

    mid = floor((low + high) / 2)
    (minL, maxL) = MAXMIN(A, low, mid)
    (minR, maxR) = MAXMIN(A, mid + 1, high)
    return (min(minL, minR), max(maxL, maxR))
```

#### Python implementation with comparison counting

```python
def maxmin_dc(a):

    comparisons = 0

    def solve(lo, hi):

        nonlocal comparisons

        if lo == hi:
            return a[lo], a[lo]

        if hi == lo + 1:
            comparisons += 1
            return (a[lo], a[hi]) if a[lo] < a[hi] else (a[hi], a[lo])

        mid = (lo + hi) // 2

        mn1, mx1 = solve(lo, mid)
        mn2, mx2 = solve(mid + 1, hi)

        comparisons += 2

        return min(mn1, mn2), max(mx1, mx2)

    result = solve(0, len(a) - 1)

    return result[0], result[1], comparisons


# Getting input from the user
n = int(input("Enter the number of elements: "))

if n <= 0:
    print("Please enter a valid number of elements.")
else:
    data = list(map(int, input("Enter the elements: ").split()))

    if len(data) != n:
        print("Please enter exactly", n, "elements.")
    else:
        minimum, maximum, comparisons = maxmin_dc(data)

        print("Minimum element:", minimum)
        print("Maximum element:", maximum)
        print("Number of comparisons:", comparisons)
```

**OUTPUT:**


<img width="1035" height="459" alt="image" src="https://github.com/user-attachments/assets/c448de05-b996-4010-84d3-aa5b7ed7cf76" />


#### Recurrence and mathematical analysis

For n = 1, T(1) = 0. For n = 2, one comparison is used. For even n, the recurrence for the comparison count is C(n) = 2C(n/2) + 2. For n a power of two, this gives C(n) = 3n/2 − 2. Thus the running time is Θ(n), and the tournament method uses fewer comparisons than independently scanning for the minimum and maximum.

| Method | Maximum comparisons (n elements) | Time |
|---|---:|---|
| Independent min and max scans | 2n − 2 | Θ(n) |
| Pairwise / tournament method (even n) | 3n/2 − 2 | Θ(n) |

For n = 8, independent scans use up to 14 comparisons, while the divide-and-conquer tournament count is 10. For odd or non-power-of-two input sizes, exact counts depend on how the split and base cases are handled.

#### Experimental dataset and results

| Input size | Example dataset pattern | Expected D&C comparisons (power-of-two n) | Independent scans upper bound |
|---:|---|---:|---:|
| 8 | [8,3,11,5,2,14,7,6] | 10 | 14 |
| 16 | Increasing integers 1…16 | 22 | 30 |
| 32 | Increasing integers 1…32 | 46 | 62 |
| 64 | Increasing integers 1…64 | 94 | 126 |

**Observation:** the comparison count grows linearly. The exact D&C count is deterministic for a fixed recursive split and base-case policy; it does not depend on whether the data is increasing, decreasing, or random.

### Part B – Binary Search

Binary Search finds a target in a sorted array. It compares the target with the middle element and discards the half in which the target cannot occur.

#### Decision rule, elimination logic and termination

- If target equals the middle value, return its index.
- If target is smaller, continue only in the left half; every value in the right half is at least the middle value and therefore cannot be the target.
- If target is larger, continue only in the right half; every value in the left half is at most the middle value and therefore cannot be the target.
- Terminate successfully when the middle value matches, or unsuccessfully when low > high.

#### Pseudocode

```text
BINARY-SEARCH(A, target):
    low = 0
    high = length(A) - 1
    while low <= high:
        mid = floor((low + high) / 2)
        if A[mid] == target:
            return mid
        else if target < A[mid]:
            high = mid - 1
        else:
            low = mid + 1
    return NOT-FOUND
```

#### Python implementation with comparison count

```python
def binary_search(a, target):

    low, high, comparisons = 0, len(a) - 1, 0

    while low <= high:

        mid = (low + high) // 2

        comparisons += 1

        if a[mid] == target:
            return mid, comparisons

        comparisons += 1

        if target < a[mid]:
            high = mid - 1
        else:
            low = mid + 1

    return -1, comparisons


# Getting input from the user
n = int(input("Enter the number of elements: "))

if n <= 0:
    print("Please enter a valid number of elements.")
else:
    values = list(map(int, input("Enter the sorted elements: ").split()))

    if len(values) != n:
        print("Please enter exactly", n, "elements.")
    elif values != sorted(values):
        print("Please enter elements in sorted order.")
    else:
        target = int(input("Enter the element to search: "))

        index, comparisons = binary_search(values, target)

        if index != -1:
            print("Element found at index:", index)
        else:
            print("Element not found.")

        print("Number of comparisons:", comparisons)
```

**OUTPUT:**


<img width="1035" height="616" alt="image" src="https://github.com/user-attachments/assets/e20350f7-71f5-4459-a921-f4ddb6f68aba" />


The code counts one equality test and, when needed, one ordering test per loop. State the counting convention when comparing results. The number of iterations is O(log n); best case is O(1), and worst/average case is O(log n).

For successful and unsuccessful experiments, use sorted arrays of sizes 16, 32, 64, 128, 256 and 512. Test targets at the first, middle and last positions, plus values below, between and above the array values. Record index or NOT-FOUND and the comparison counter.

| n | Approximate worst-case iterations | Growth description |
|---:|---:|---|
| 16 | 5 | logarithmic |
| 32 | 6 | logarithmic |



### Q1 – Conclusion

The Max-Min algorithm and Binary Search demonstrate the effective application of the Divide and Conquer technique in searching and selection problems. The Max-Min algorithm divides the given array into smaller subarrays and independently identifies the minimum and maximum elements. The results from these subarrays are then combined to obtain the overall minimum and maximum values. This method reduces unnecessary comparisons and improves the efficiency of finding extreme elements.

Binary Search works by repeatedly dividing a sorted array into two halves and comparing the target value with the middle element. Based on the comparison, the search continues only in the required half, reducing the search space at every step. The Max-Min algorithm has a time complexity of Θ(n), while Binary Search achieves Θ(log n) time complexity. The implementation and analysis of these algorithms provide a clear understanding of recursion, problem decomposition, comparison reduction, and efficient searching techniques.

---

## Q2 – The Quality of Decomposition in Sorting

### Merge Sort

Merge Sort divides the array into two approximately equal halves, recursively sorts each half, and merges the two sorted halves. Its decomposition is balanced regardless of the original order of the input.

#### Pseudocode

```text
MERGE-SORT(A):
    if length(A) <= 1:
        return A
    split A into left and right halves
    left_sorted = MERGE-SORT(left)
    right_sorted = MERGE-SORT(right)
    return MERGE(left_sorted, right_sorted)

MERGE(L, R):
    create empty result
    compare the first unused item of L and R
    append the smaller item; advance that input
    append all remaining items
    return result
```

#### Python implementation

```python
def merge_sort(a):

    if len(a) <= 1:
        return a[:]

    mid = len(a) // 2

    left = merge_sort(a[:mid])
    right = merge_sort(a[mid:])

    i = j = 0
    out = []

    while i < len(left) and j < len(right):

        if left[i] <= right[j]:
            out.append(left[i])
            i += 1
        else:
            out.append(right[j])
            j += 1

    return out + left[i:] + right[j:]


# Getting input from the user
n = int(input("Enter the number of elements: "))

if n <= 0:
    print("Please enter a valid number of elements.")
else:
    data = list(map(int, input("Enter the elements: ").split()))

    if len(data) != n:
        print("Please enter exactly", n, "elements.")
    else:
        sorted_data = merge_sort(data)

        print("Original array:", data)
        print("Sorted array:", sorted_data)
```

**OUTPUT:**


<img width="1035" height="444" alt="image" src="https://github.com/user-attachments/assets/ac17d3a7-3c6d-479f-9e9b-134f64ec9aea" />


#### Recurrence and complexity

T(n) = 2T(n/2) + Θ(n), because two halves are sorted recursively and merging takes linear time. By the Master Theorem, T(n) = Θ(n log n). Auxiliary space is Θ(n) for the merge buffer in this implementation.

### Quick Sort

Quick Sort selects a pivot, partitions the array into values smaller than or equal to the pivot and values greater than the pivot, and recursively sorts the partitions. This report uses the last element as the pivot so the experiment is reproducible.

#### Pseudocode

```text
QUICK-SORT(A, low, high):
    if low < high:
        p = PARTITION(A, low, high)  // last element is pivot
        QUICK-SORT(A, low, p - 1)
        QUICK-SORT(A, p + 1, high)

PARTITION(A, low, high):
    pivot = A[high]
    i = low - 1
    for j from low to high - 1:
        if A[j] <= pivot:
            i = i + 1
            swap A[i], A[j]
    swap A[i + 1], A[high]
    return i + 1
```

#### Python implementation with partition metrics

```python
def quick_sort_metrics(a):

    a = a[:]

    partitions, max_depth = [], 0

    def sort(lo, hi, depth):

        nonlocal max_depth

        max_depth = max(max_depth, depth)

        if lo < hi:

            pivot = a[hi]

            i = lo - 1

            for j in range(lo, hi):

                if a[j] <= pivot:
                    i += 1
                    a[i], a[j] = a[j], a[i]

            p = i + 1

            a[p], a[hi] = a[hi], a[p]

            partitions.append((p - lo, hi - p))

            sort(lo, p - 1, depth + 1)
            sort(p + 1, hi, depth + 1)

    sort(0, len(a) - 1, 1)

    return a, partitions, max_depth


# Getting input from the user
n = int(input("Enter the number of elements: "))

if n <= 0:
    print("Please enter a valid number of elements.")
else:
    data = list(map(int, input("Enter the elements: ").split()))

    if len(data) != n:
        print("Please enter exactly", n, "elements.")
    else:
        sorted_data, partitions, max_depth = quick_sort_metrics(data)

        print("Original array:", data)
        print("Sorted array:", sorted_data)
        print("Partition sizes:", partitions)
        print("Maximum recursion depth:", max_depth)
```

**OUTPUT:**


<img width="1035" height="353" alt="image" src="https://github.com/user-attachments/assets/5e0c54aa-21e7-4a1d-a2f1-4c29b99fdd99" />


#### Recurrence and complexity

Best/balanced case:

T(n) = 2T(n/2) + Θ(n) = Θ(n log n).

Worst case:

T(n) = T(n−1) + Θ(n) = Θ(n²), for example when the chosen pivot repeatedly becomes the smallest or largest element.

Average expected time with a suitably randomized pivot is Θ(n log n), while worst-case stack depth can be Θ(n).

#### Balanced and unbalanced experiment design

| Scenario | Suggested input (last-element pivot) | Expected partition behaviour | Expected recursion depth |
|---|---|---|---|
| Balanced-like | A shuffled permutation; repeat with fixed random seeds | Partitions near equal sizes on average | O(log n) typical |
| Severely unbalanced | Already sorted ascending or descending data | One side has 0 elements and other has n−1 for this pivot rule | O(n) |

Record each partition as (left_size, right_size), maximum recursion depth, elapsed time, and correctness. Repeat for n = 100, 500, 1,000, 2,000 and 4,000. A last-element pivot on sorted ascending input produces the worst-case pattern; a randomized or median-of-three pivot can reduce the likelihood of this pattern.

#### Merge Sort versus Quick Sort

| Feature | Merge Sort | Quick Sort |
|---|---|---|
| Decomposition | Always splits by position into near-equal halves | Depends on pivot and input values |
| Recurrence | 2T(n/2)+Θ(n) | T(k)+T(n−k−1)+Θ(n) |
| Worst-case time | Θ(n log n) | Θ(n²) |
| Typical time | Θ(n log n) | Θ(n log n) |
| Extra memory | Θ(n) for this array implementation | Usually in-place partition; recursion stack |
| Predictability | Predictable recursion-tree height | Partition quality varies |

#### Joint design question

Before choosing a sorting component when input characteristics are unknown, we would want to know the expected input size, whether data is already or nearly sorted, the distribution and frequency of duplicates, whether stable ordering is required, available memory, worst-case latency requirements, and whether inputs may be adversarial.

Merge Sort is a strong choice when predictable O(n log n) worst-case time and stability are important. Quick Sort can be attractive when in-place sorting and strong average performance are priorities, especially with randomized pivot selection or an introspective fallback.

### Q2 – Conclusion

Merge Sort and Quick Sort demonstrate how the Divide and Conquer strategy can be used to arrange data efficiently. Merge Sort recursively divides the input array into smaller subarrays until each subarray contains a single element. These subarrays are then merged in sorted order to produce the final result. It provides consistent performance with a time complexity of Θ(n log n) in the best, average, and worst cases.

Quick Sort selects a pivot element and partitions the array into smaller and larger elements. The same process is recursively applied to the partitions until the complete array becomes sorted. Its performance depends on the selection of the pivot and the balance of the partitions. Balanced partitions provide an average time complexity of Θ(n log n), whereas highly unbalanced partitions can result in a worst-case complexity of Θ(n²).

Merge Sort requires additional memory for merging, while Quick Sort mainly performs partitioning within the original array. The implementation and comparison of both algorithms help us understand their working principles, advantages, limitations, and performance under different input conditions.

---

## Q3 – Breaking the Quadratic Barrier: Karatsuba Multiplication

Karatsuba multiplies large integers by splitting each number into high and low parts and reducing four half-size multiplications to three.

### Decomposition and derivation

Let x = a·B + b and y = c·B + d, where B = 10^m (or an appropriate power of the numeric base) and a,b,c,d are the high/low parts.

Then:

xy = ac·B² + (ad+bc)·B + bd.

Compute:

- z2 = ac
- z0 = bd
- z1 = (a+b)(c+d) − z2 − z0

The product is:

z2·B² + z1·B + z0.

### Pseudocode

```text
KARATSUBA(x, y):
    if x or y is small:
        return x * y
    m = ceil(max(number_of_digits(x), number_of_digits(y)) / 2)
    B = 10^m
    a, b = divmod(x, B)
    c, d = divmod(y, B)
    z2 = KARATSUBA(a, c)
    z0 = KARATSUBA(b, d)
    z1 = KARATSUBA(a+b, c+d) - z2 - z0
    return z2*B*B + z1*B + z0
```

### Python implementation and standard baseline

```python
def standard_multiply(x, y):

    return x * y


def karatsuba(x, y, threshold=32):

    if x < 0 or y < 0:
        sign = -1 if (x < 0) != (y < 0) else 1
        return sign * karatsuba(abs(x), abs(y), threshold)

    if x < 10**threshold or y < 10**threshold:
        return x * y

    m = max(len(str(x)), len(str(y))) // 2

    B = 10**m

    a, b = divmod(x, B)
    c, d = divmod(y, B)

    z2 = karatsuba(a, c, threshold)
    z0 = karatsuba(b, d, threshold)
    z1 = karatsuba(a + b, c + d, threshold) - z2 - z0

    return z2 * B * B + z1 * B + z0


# Getting input from the user
x = int(input("Enter the first number: "))
y = int(input("Enter the second number: "))

threshold = int(input("Enter the threshold value (default 32): "))

if threshold <= 0:
    print("Please enter a positive threshold value.")
else:
    result1 = standard_multiply(x, y)
    result2 = karatsuba(x, y, threshold)

    print("Standard Multiplication Result:", result1)
    print("Karatsuba Multiplication Result:", result2)

    if result1 == result2:
        print("Both multiplication results are equal.")
    else:
        print("The multiplication results are not equal.")
```

**OUTPUT:**


<img width="1035" height="513" alt="image" src="https://github.com/user-attachments/assets/56ec2c2d-8810-4096-935f-404a5168bc52" />


The standard Python integer multiplication operator is a baseline, not necessarily the elementary school O(n²) algorithm; the Python runtime may already use optimized multiplication internally. For a fair algorithmic comparison, implement grade-school multiplication explicitly or state the runtime's built-in implementation as the baseline.

### Recurrence and solution

Karatsuba performs three recursive multiplications on roughly n/2-digit numbers and linear work for additions, subtraction and splitting:

T(n) = 3T(n/2) + Θ(n).

The Master Theorem gives:

T(n) = Θ(n^(log₂3)) ≈ Θ(n^1.585).

Conventional grade-school multiplication takes Θ(n²) single-digit operations.

### Crossover experiment

Use operands with 32, 64, 128, 256, 512, 1,024 and 2,048 decimal digits. Generate reproducible random decimal strings without leading zeros. For each size, verify the two products match, repeat each timing at least 5–10 times, and report the median.

Record recursive multiplication calls or a counter if you instrument the implementation. Determine the crossover from the measured data; it depends on language, hardware and threshold.

| Operand digits | Standard multiplication time | Karatsuba time | Winner |
|---:|---|---|---|
| 32 | Measure locally | Measure locally | Do not assume |
| 64 | Measure locally | Measure locally | Do not assume |
| 128 | Measure locally | Measure locally | Do not assume |
| 256 | Measure locally | Measure locally | Do not assume |
| 512 | Measure locally | Measure locally | Do not assume |
| 1,024 | Measure locally | Measure locally | Do not assume |

Why Karatsuba may be slower for small inputs: recursion, digit splitting, additions, temporary integer creation and function-call overhead can exceed the savings from reducing one multiplication. The implementation's threshold should be selected experimentally.

### Joint conclusion

Karatsuba Multiplication demonstrates how mathematical decomposition can improve the efficiency of multiplying large integers. The conventional recursive multiplication approach requires four smaller multiplications when two numbers are divided into higher and lower parts. Karatsuba reduces these recursive multiplications from four to three by calculating three intermediate products and combining them using mathematical operations.

Its recurrence relation is T(n) = 3T(n/2) + O(n), resulting in an approximate time complexity of Θ(n^1.585). This is theoretically more efficient than the conventional recursive multiplication approach.

The implementation compares the result of Karatsuba multiplication with standard multiplication to verify the correctness of the output. Although the algorithm reduces the number of recursive multiplications, additional calculations and recursion overhead can affect its practical performance for smaller inputs. It becomes particularly useful when multiplying sufficiently large integers. This algorithm provides an understanding of how reducing expensive operations through mathematical techniques can improve computational efficiency.


## Q4 – The Reality of Strassen's Matrix Multiplication

### Introduction

Strassen's Matrix Multiplication is an efficient Divide and Conquer algorithm used to multiply two square matrices. Conventional matrix multiplication divides the matrices into four blocks and performs eight recursive block multiplications. Strassen's algorithm reduces these eight multiplications to seven, improving the asymptotic time complexity.

### Algorithm Design and Decomposition

- Divide each input matrix into four equal-sized submatrices.
- Apply the Strassen transformation to calculate seven intermediate products.
- Combine the seven products to construct the four blocks of the result matrix.
- If the matrix size is not a power of two, pad the matrices with zeros to the next power of two.
- Remove the additional padded rows and columns from the final result.

### Conventional Block Matrix Multiplication

Let two matrices be divided into four blocks:

```text
A = | A11  A12 |       B = | B11  B12 |
    | A21  A22 |           | B21  B22 |
```

Conventional block multiplication uses eight block multiplications:

```text
C11 = A11*B11 + A12*B21
C12 = A11*B12 + A12*B22
C21 = A21*B11 + A22*B21
C22 = A21*B12 + A22*B22
```

### Strassen's Seven Multiplications

Strassen's algorithm calculates seven products instead of eight:

```text
M1 = (A11 + A22) * (B11 + B22)

M2 = (A21 + A22) * B11

M3 = A11 * (B12 - B22)

M4 = A22 * (B21 - B11)

M5 = (A11 + A12) * B22

M6 = (A21 - A11) * (B11 + B12)

M7 = (A12 - A22) * (B21 + B22)
```

The four result blocks are reconstructed as follows:

```text
C11 = M1 + M4 - M5 + M7

C12 = M3 + M5

C21 = M2 + M4

C22 = M1 - M2 + M3 + M6
```

### Pseudocode

```text
STRASSEN(A, B):
    if matrix size is small:
        return conventional multiplication

    divide A into A11, A12, A21, A22
    divide B into B11, B12, B21, B22

    calculate M1, M2, M3, M4, M5, M6 and M7

    C11 = M1 + M4 - M5 + M7
    C12 = M3 + M5
    C21 = M2 + M4
    C22 = M1 - M2 + M3 + M6

    combine C11, C12, C21 and C22

    return C
```

### Padding Strategy

- Strassen's algorithm works most conveniently when the matrix size is a power of two.
- If the matrix size is not a power of two, zero-padding is applied.
- Both matrices are expanded to the next power-of-two size.
- After multiplication, the padded rows and columns are removed.
- This ensures that the final result has the required dimensions.

### Recurrence and Complexity Analysis

The recurrence relation for Strassen's algorithm is:

```text
T(n) = 7T(n/2) + Θ(n²)
```

Where:

- Seven recursive multiplications are performed.
- Each multiplication operates on matrices of size n/2.
- Matrix additions and subtractions require Θ(n²) time.

Using the Master Theorem:

```text
T(n) = Θ(n^log₂7)
     ≈ Θ(n^2.807)
```

Therefore, Strassen's algorithm has better asymptotic time complexity than conventional matrix multiplication, which requires Θ(n³) time.

### Experimental Design

Test both conventional and Strassen matrix multiplication using the following matrix sizes:

| Matrix Size | Conventional Scalar Multiplications | Strassen Recursive Products |
|---|---:|---:|
| 8 × 8 | 512 | 7³ = 343 |
| 16 × 16 | 4,096 | 7⁴ = 2,401 |
| 32 × 32 | 32,768 | 7⁵ = 16,807 |
| 64 × 64 | 262,144 | 7⁶ = 117,649 |
| 128 × 128 | 2,097,152 | 7⁷ = 823,543 |

**Note:** The Strassen product counts shown are for a fully recursive algorithm down to 1 × 1 matrices. Actual execution time must be measured by running the implementations.

### Performance Analysis

- Conventional multiplication performs eight block multiplications at every recursive level.
- Strassen's algorithm reduces the number of recursive multiplications to seven.
- Strassen requires additional matrix additions and subtractions.
- Recursion and temporary matrix storage introduce extra overhead.
- Padding may increase the amount of computation for certain matrix sizes.
- Memory usage and cache behaviour can also affect practical performance.

### Joint Engineering Decision

Conventional matrix multiplication may be preferred under the following conditions:

- When matrices are small.
- When padding creates unnecessary additional computation.
- When memory availability is limited.
- When recursion and temporary matrix creation introduce significant overhead.
- When measured execution time shows that conventional multiplication is faster.

Strassen's algorithm is more suitable for sufficiently large dense matrices when experimental results demonstrate a practical performance improvement.

### Conclusion

Strassen's Matrix Multiplication demonstrates how Divide and Conquer can improve the efficiency of matrix multiplication by reducing the number of recursive multiplication operations from eight to seven. It divides the matrices into smaller blocks, calculates seven intermediate products, and combines them to obtain the final result. Its time complexity is approximately Θ(n²·⁸⁰⁷), which is better than the Θ(n³) complexity of conventional matrix multiplication. However, additional additions, subtractions, recursion, padding, and memory requirements can affect its practical performance. Therefore, experimental comparison is important when deciding which method should be used for a particular matrix size.

---

## Q5 – Upgrading Closest Pair Using Divide and Conquer

### Introduction

The Closest Pair of Points problem involves finding two points with the minimum Euclidean distance among a given set of two-dimensional points.

The Brute Force approach checks every possible pair of points and requires Θ(n²) time. The Divide and Conquer approach improves the efficiency by dividing the points into smaller groups, solving each group recursively, and combining the results.

### Algorithm Design and Decomposition

The Divide and Conquer Closest Pair algorithm follows these steps:

1. Sort the points based on their X-coordinates and Y-coordinates.
2. Divide the points into two approximately equal groups using the middle X-coordinate.
3. Recursively find the closest pair in the left half.
4. Recursively find the closest pair in the right half.
5. Find the smaller distance from the two recursive results.
6. Create a strip around the dividing boundary.
7. Check the points inside the strip to identify a closer pair that may cross the boundary.
8. Return the minimum distance and the corresponding pair of points.

### Base Case

- If the number of points is two or three, calculate all possible pairwise distances directly.
- Return the pair having the minimum distance.

### Euclidean Distance Formula

For two points:

```text
P1 = (x1, y1)
P2 = (x2, y2)
```

The Euclidean distance is:

```text
d = √((x2 - x1)² + (y2 - y1)²)
```

### Pseudocode

```text
CLOSEST-PAIR(P):
    sort points by X-coordinate
    sort points by Y-coordinate

    return CLOSEST(Px, Py)


CLOSEST(Px, Py):
    if number of points <= 3:
        calculate all pairwise distances
        return the minimum distance and pair

    divide points into left and right halves

    leftResult = CLOSEST(left points)
    rightResult = CLOSEST(right points)

    δ = minimum distance from leftResult and rightResult

    create a strip containing points within δ
    of the dividing line

    check neighbouring points in the strip

    return the smallest distance and corresponding pair
```

### Combine Step and Boundary Handling

The combine step is important because the closest pair may contain one point from the left half and another point from the right half.

- First, calculate the minimum distance from the left and right halves.
- Let the smaller distance be δ.
- Construct a vertical strip around the dividing line with width 2δ.
- Examine the points inside the strip in increasing Y-coordinate order.
- Compare only a bounded number of neighbouring points rather than comparing every point with every other point.
- Update the minimum distance if a closer pair is found.

The strip requires special treatment because a pair crossing the dividing boundary may be closer than the pairs found independently in the two halves.

### Complexity Analysis

| Approach | Time Complexity | Explanation |
|---|---|---|
| Brute Force | Θ(n²) | Checks every possible pair of points |
| Divide and Conquer | Θ(n log n) | Uses sorting, recursive division and an efficient strip check |

The recurrence relation is:

```text
T(n) = 2T(n/2) + Θ(n)
```

Where:

- Two recursive calls process the left and right halves.
- The combine step takes linear time when the points are maintained in the required sorted order.

Using the Master Theorem:

```text
T(n) = Θ(n log n)
```

### Experimental Comparison

Both Brute Force and Divide and Conquer approaches should be tested using equivalent datasets.

Suggested dataset sizes:

| Number of Points | Brute Force Approach | Divide and Conquer Approach |
|---:|---|---|
| 100 | Record execution time and distance calculations | Record execution time and distance calculations |
| 500 | Record execution time and distance calculations | Record execution time and distance calculations |
| 1,000 | Record execution time and distance calculations | Record execution time and distance calculations |
| 2,000 | Record execution time and distance calculations | Record execution time and distance calculations |
| 5,000 | Record execution time and distance calculations | Record execution time and distance calculations |

**Note:** Run both implementations and enter the actual measured execution times and operation counts. Do not use estimated values as experimental results.

### Performance Analysis

- Brute Force checks every possible pair of points.
- The number of pairwise comparisons increases quadratically as the input size grows.
- Divide and Conquer reduces the problem into smaller subproblems.
- The strip stage checks only a bounded number of neighbouring points.
- The Divide and Conquer approach becomes practically advantageous when the input size is sufficiently large, depending on implementation and hardware.
- Both approaches should produce the same minimum distance for the same dataset.

### Conclusion

The Closest Pair of Points problem demonstrates how geometric problems can be solved efficiently using the Divide and Conquer approach. The algorithm sorts the points based on their X and Y coordinates and divides them into two approximately equal groups. The closest pair is calculated independently in both groups, and the smaller distance is selected. A narrow strip around the dividing line is then examined because a closer pair may contain points from different groups. By checking only a bounded number of neighbouring points in the strip, unnecessary distance calculations are reduced. The algorithm achieves Θ(n log n) time complexity, whereas the Brute Force approach requires Θ(n²) time because it checks every possible pair. The implementation compares the results of both approaches to verify the correctness of the calculated minimum distance. This problem provides practical understanding of geometric computation, sorting, recursive decomposition, and efficient combination of results.


## Q6 – Advanced Divide-and-Conquer Mini-Investigations

### Student A – Median of Medians

#### Introduction

Median of Medians is a selection algorithm used to find the Kth smallest element in an unsorted array without sorting the entire array. It uses the Divide and Conquer technique to select a good pivot and guarantees worst-case linear time complexity.

#### Grouping and Pivot Selection

The algorithm follows these steps:

1. Divide the input array into groups of five elements.
2. Sort each small group and find its median.
3. Collect all the medians into a separate array.
4. Recursively find the median of these medians.
5. Select this value as the pivot.
6. Partition the original array into three groups:
   - Elements smaller than the pivot.
   - Elements equal to the pivot.
   - Elements greater than the pivot.
7. Recursively search only the group containing the required Kth position.
8. Return the pivot if the required position belongs to the equal group.

#### Pseudocode

```text
SELECT(A, k):
    if length(A) <= 5:
        sort A
        return A[k-1]

    divide A into groups of at most 5

    medians = median of each sorted group

    pivot = SELECT(medians, ceil(length(medians)/2))

    partition A into:
        L (< pivot)
        E (= pivot)
        G (> pivot)

    if k <= length(L):
        return SELECT(L, k)

    if k <= length(L) + length(E):
        return pivot

    return SELECT(G, k - length(L) - length(E))
```

#### Python Implementation

```python
def median_of_medians_select(a, k):
    if not 1 <= k <= len(a):
        raise ValueError("k must be between 1 and n")

    if len(a) <= 5:
        return sorted(a)[k - 1]

    groups = [a[i:i + 5] for i in range(0, len(a), 5)]

    medians = [sorted(g)[len(g) // 2] for g in groups]

    pivot = median_of_medians_select(
        medians, (len(medians) + 1) // 2
    )

    low = [x for x in a if x < pivot]
    equal = [x for x in a if x == pivot]
    high = [x for x in a if x > pivot]

    if k <= len(low):
        return median_of_medians_select(low, k)

    if k <= len(low) + len(equal):
        return pivot

    return median_of_medians_select(
        high, k - len(low) - len(equal)
    )


# Getting input from the user
n = int(input("Enter the number of elements: "))

if n <= 0:
    print("Please enter a valid number of elements.")
else:
    data = list(map(int, input("Enter the elements: ").split()))

    if len(data) != n:
        print("Please enter exactly", n, "elements.")
    else:
        k = int(input("Enter the value of K: "))

        if 1 <= k <= n:
            result = median_of_medians_select(data, k)
            print("The", k, "th smallest element is:", result)
        else:
            print("Please enter K between 1 and", n)
```

#### Output


<img width="1035" height="508" alt="image" src="https://github.com/user-attachments/assets/cd0ddc44-13ba-4486-849e-7453cba08f3c" />


#### Worst-Case Guarantee and Recurrence

The pivot construction guarantees that a constant fraction of elements is discarded in the worst case.

The recurrence relation is:

```text
T(n) ≤ T(⌈n/5⌉) + T(7n/10 + O(1)) + O(n)
```

This recurrence gives:

```text
T(n) = O(n)
```

Therefore, Median of Medians provides worst-case linear time complexity.

#### Comparison with QuickSelect

| Selection Method | Pivot Choice | Expected / Worst-Case Time | Comment |
|---|---|---|---|
| QuickSelect (random pivot) | Random element | Expected O(n); worst O(n²) | Usually simple and fast; randomisation reduces risk but does not eliminate a bad run |
| Deterministic poor pivot | First/last element under adversarial order | Can be O(n²) | Repeatedly leaves nearly all elements on one side |
| Median of Medians | Median of group medians | Worst-case O(n) | More work per pivot, but guarantees progress |

Pivot quality is important because it determines how much of the array is discarded after each partition. A balanced pivot reduces the remaining problem substantially, while a poor pivot can leave almost the entire input for the next recursive call.

#### Experimental Design

Test the algorithm using the following datasets:

- Random arrays.
- Sorted arrays.
- Reverse-sorted arrays.
- Adversarial arrays.

Suggested input sizes:

| Input Size (n) | Dataset |
|---:|---|
| 100 | Random, sorted and reverse-sorted |
| 500 | Random, sorted and reverse-sorted |
| 1,000 | Random, sorted and reverse-sorted |
| 5,000 | Random, sorted and reverse-sorted |
| 10,000 | Random, sorted and reverse-sorted |

Compare the selected value against:

```python
sorted(A)[k - 1]
```

Record partition sizes, comparisons and recursion depth. Compare deterministic first-element QuickSelect, randomized QuickSelect and Median of Medians.

Randomisation reduces the likelihood of repeated poor partitions but cannot provide a deterministic worst-case guarantee.

---

### Student B – Meet-in-the-Middle Subset Sum

#### Introduction

Meet-in-the-Middle is a technique used to solve problems involving subsets and combinations. It is useful for the Subset Sum problem, where the objective is to determine whether any subset of the given numbers produces a specified target sum.

Straightforward enumeration considers all possible subsets and requires O(2ⁿ) time. Meet-in-the-Middle reduces the search effort by dividing the input into two approximately equal halves.

#### Decomposition and Combine Strategy

The algorithm follows these steps:

1. Divide the input array into two halves, L and R.
2. Generate all possible subset sums of the left half.
3. Generate all possible subset sums of the right half.
4. Store the right-side subset sums in a hash set.
5. For every left-side sum x, calculate the required complementary sum S − x.
6. Check whether S − x exists in the right-side hash set.
7. If a matching sum is found, return TRUE.
8. Otherwise, return FALSE after checking all left-side sums.

#### Pseudocode

```text
SUBSET-SUM-MITM(A, target):

    split A into L and R

    leftSums = all subset sums of L

    rightSums = all subset sums of R

    store rightSums in a hash set

    for x in leftSums:

        if target - x is in rightSums:
            return TRUE

    return FALSE
```

#### Python Implementation

```python
def subset_sums(values):
    sums = [0]

    for v in values:
        sums += [x + v for x in sums]

    return sums


def subset_sum_mitm(a, target):
    mid = len(a) // 2

    left_sums = subset_sums(a[:mid])

    right_sums = set(subset_sums(a[mid:]))

    for x in left_sums:
        if target - x in right_sums:
            return True

    return False


# Getting input from the user
n = int(input("Enter the number of elements: "))

if n <= 0:
    print("Please enter a valid number of elements.")
else:
    data = list(map(int, input("Enter the elements: ").split()))

    if len(data) != n:
        print("Please enter exactly", n, "elements.")
    else:
        target = int(input("Enter the target sum: "))

        result = subset_sum_mitm(data, target)

        if result:
            print("Subset with the given target sum exists.")
        else:
            print("Subset with the given target sum does not exist.")
```

#### Output


<img width="1035" height="478" alt="image" src="https://github.com/user-attachments/assets/c9c1ce20-b798-4a10-a675-dbceec82f033" />


#### Search-Space and Complexity Analysis

Each half contains approximately n/2 elements. Therefore, each half has approximately 2^(n/2) possible subsets.

- Generating subset sums takes approximately O(2^(n/2)) time.
- Searching for complementary sums takes expected O(2^(n/2)) time using hashing.
- Additional memory required is O(2^(n/2)).
- Sorting one list of sums and using binary search is an alternative approach, with O(2^(n/2) log 2^(n/2)) sorting and search work.

#### Comparison of Search Space

| n | Straight Enumeration 2ⁿ | MITM Sums per Half ≈ 2^(n/2) | Memory Trend |
|---:|---:|---:|---|
| 20 | 1,048,576 | 1,024 | Manageable |
| 30 | 1,073,741,824 | 32,768 | Higher |
| 40 | 1,099,511,627,776 | 1,048,576 | Substantial |
| 50 | 1,125,899,906,842,624 | 33,554,432 | Very high |

Meet-in-the-Middle reduces computational work by replacing one search over 2ⁿ combinations with two lists of approximately 2^(n/2) partial results. The trade-off is memory because storing these partial sums can become the limiting factor.

### Conclusion

Median of Medians and Meet-in-the-Middle introduce advanced techniques for solving selection and subset-based problems efficiently. Median of Medians is used to identify the Kth smallest element in an unsorted array. It divides the array into smaller groups, usually containing five elements each, calculates the median of every group, and selects the median of these medians as a pivot. The original array is partitioned based on this pivot, and the required partition is processed recursively until the Kth smallest element is found. This technique guarantees worst-case linear time complexity of O(n).

Meet-in-the-Middle is used to solve problems involving subsets and combinations, particularly the Subset Sum problem. It divides the input array into two approximately equal halves and generates all possible subset sums independently for both halves. The generated results are stored and compared to determine whether a combination of subset sums produces the required target value. This reduces the search effort to approximately O(2^(n/2)) time with comparable memory requirements for the standard subset-generation approach. These techniques demonstrate how selecting an appropriate strategy for a particular problem can reduce computational effort and improve efficiency.

---

## Q7 – Day-4 Design Challenge: Design Divide and Conquer from First Principles

### Chosen Challenge Problem: Count Inversions in an Array

**Note:** The supplied assignment brief describes the six design stages but does not name the actual Day-4 challenge problem. This report uses Counting Inversions as the proposed challenge. Confirm with the faculty that this is the intended problem before submission if a different challenge was announced.

An inversion is a pair of indices (i, j) such that:

```text
i < j and A[i] > A[j]
```

**Example:**

For the array:

```text
A = [2, 4, 1, 3, 5]
```

The inversions are:

- (2, 1)
- (4, 1)
- (4, 3)

Therefore, the total number of inversions is **3**.

### Stage 1 – Independent Design Proposals

#### Student A – Initial Proposal (Independent)

- **Decomposition:** Split the array into left and right halves until each part contains one element.
- **Base Case:** An array of size zero or one has zero inversions.
- **Subproblem Information:** Each recursive call returns a sorted version of its section and the number of inversions within that section.
- **Combine Strategy:** Merge the two sorted halves and count cross-inversions when an element from the right half is placed before the remaining elements in the left half.

#### Student B – Initial Proposal (Independent)

- **Decomposition:** Divide the index range into two contiguous halves so pairs are either fully in the left half, fully in the right half, or cross the split.
- **Base Case:** One item cannot form an inversion.
- **Subproblem Information:** Return the sorted values and the inversion count for that half.
- **Combine Strategy:** Use a two-pointer merge. When the next right value is smaller than the next left value, add the number of unmerged left values to the cross-inversion count.

**Important:** The above are proposed example records. Before submitting, each student should edit this section to reflect the design they actually wrote independently before discussion. Do not claim these were independently produced if the process did not occur.

### Stage 2 – Compare the Two Designs

| Comparison Point | Student A Proposal | Student B Proposal | Joint Decision |
|---|---|---|---|
| Decomposition | Split array recursively | Split contiguous index ranges | Same recursive split is retained |
| Base Case | 0 or 1 item | One item | Use length ≤ 1 |
| Returned Information | Sorted subarray and internal count | Sorted subarray and internal count | Retain both |
| Combine | Count while merging | Add remaining-left count when right item is smaller | Use two-pointer merge counting |
| Strength | Connects counting to merge operation | Clearly explains cross-half pairs | Combine both explanations |
| Potential Issue | Must count all remaining left values, not just one | Equal values must not count as inversions | Use strict comparison: left > right |

### Stage 3 – Joint Final Design

The final design uses the Divide and Conquer technique:

1. Divide the array into two halves.
2. Recursively count inversions in each half.
3. Return each half in sorted order.
4. Merge the two sorted halves.
5. During merging, if the current right element is smaller than the current left element, add the number of remaining elements in the left half to the inversion count.
6. Add the left, right and cross-inversion counts to obtain the final result.

#### Pseudocode

```text
COUNT-INVERSIONS(A):

    if length(A) <= 1:
        return (A, 0)

    mid = floor(length(A)/2)

    (Lsorted, leftCount) =
        COUNT-INVERSIONS(A[0:mid])

    (Rsorted, rightCount) =
        COUNT-INVERSIONS(A[mid:])

    (merged, crossCount) =
        MERGE-COUNT(Lsorted, Rsorted)

    return (
        merged,
        leftCount + rightCount + crossCount
    )


MERGE-COUNT(L, R):

    i = 0
    j = 0
    count = 0
    output = []

    while i < length(L) and j < length(R):

        if L[i] <= R[j]:
            append L[i]
            i = i + 1

        else:
            append R[j]
            count = count + (length(L) - i)
            j = j + 1

    append remaining elements of L and R

    return (output, count)
```

#### Python Implementation and Brute-Force Baseline

```python
def merge_count(L, R):
    i = 0
    j = 0
    count = 0
    output = []

    while i < len(L) and j < len(R):

        if L[i] <= R[j]:
            output.append(L[i])
            i += 1

        else:
            output.append(R[j])
            count += len(L) - i
            j += 1

    output.extend(L[i:])
    output.extend(R[j:])

    return output, count


def count_inversions(A):
    if len(A) <= 1:
        return A, 0

    mid = len(A) // 2

    Lsorted, leftCount = count_inversions(A[:mid])

    Rsorted, rightCount = count_inversions(A[mid:])

    merged, crossCount = merge_count(Lsorted, Rsorted)

    return merged, leftCount + rightCount + crossCount


# Getting input from the user
n = int(input("Enter the number of elements: "))

if n <= 0:
    print("Please enter a valid number of elements.")

else:
    data = list(map(int, input("Enter the elements: ").split()))

    if len(data) != n:
        print("Please enter exactly", n, "elements.")

    else:
        sorted_data, inversions = count_inversions(data)

        print("Original array:", data)
        print("Sorted array:", sorted_data)
        print("Total number of inversions:", inversions)
```

#### Output


<img width="1035" height="489" alt="image" src="https://github.com/user-attachments/assets/2079813a-30b6-466d-b874-8876e66a6a7b" />


### Stage 4 – Mathematical Validation (Student A Primary)

The recurrence relation is:

```text
T(n) = 2T(n/2) + Θ(n)
```

Explanation:

- Two recursive calls process halves of size n/2.
- The merge-and-count operation scans each element at most once.
- Therefore, the merging operation takes Θ(n) time.

Using the Master Theorem:

```text
T(n) = Θ(n log n)
```

The Brute Force baseline checks all index pairs and takes Θ(n²) time.

### Stage 4 – Experimental Validation (Student B Primary)

Test arrays of different lengths and include different input patterns.

Suggested input sizes:

- 10
- 100
- 500
- 1,000
- 5,000
- 10,000

Test the following cases:

- Sorted ascending arrays.
- Reverse-sorted arrays.
- Random arrays.
- Arrays containing duplicate values.
- Empty arrays.
- Single-element arrays.
- Arrays containing negative values.

For every test, verify that the Divide and Conquer count equals the Brute Force count for sizes small enough to run the baseline.

#### Test Cases and Expected Results

| Test Case | Input Example / Pattern | Expected Inversion Count |
|---|---|---:|
| Already Sorted | `[1,2,3,4,5]` | 0 |
| Reverse Sorted | `[5,4,3,2,1]` | 10 |
| Mixed | `[2,4,1,3,5]` | 3 |
| Duplicates | `[2,2,1]` | 2 |
| Single Element | `[7]` | 0 |
| Empty | `[]` | 0 |

### Stage 5 – Cross-Defence

**Student A should explain the experimental evidence:**

- Correctness matches the Brute Force baseline on all small test cases.
- Comparison and execution-time growth is much slower for the quadratic baseline as n increases.
- Divide and Conquer reduces unnecessary pairwise comparisons.

**Student B should explain the recurrence:**

- Two recursive calls operate on arrays of size n/2.
- One linear merge-and-count operation combines the results.
- Therefore, the recurrence is `2T(n/2) + Θ(n)`.

### Stage 6 – Joint Evaluation

- **Why suitable for Divide and Conquer:** Every inversion belongs entirely to the left half, entirely to the right half, or crosses the split. These categories can be counted without double-counting.
- **Work reduced:** Pairwise comparison of all index pairs is replaced by recursive sorting and a linear merge pass.
- **Additional costs:** Recursion stack and temporary merge arrays require O(n) auxiliary storage.
- **When D&C may not be appropriate:** For very small arrays, the simple Brute Force method may be easier and have lower overhead. Streaming inputs or strict memory limits may also favour another design.
- **Algorithm-selection lesson:** Look for independent smaller subproblems, a base case, a way to combine compact summaries, and a combine step whose cost does not erase the benefit of decomposition.

### Conclusion

Counting Inversions demonstrates how the Divide and Conquer technique can be applied to solve a problem involving the identification of incorrectly ordered element pairs in an array. An inversion is a pair of elements in which the earlier element is greater than the later element. The Brute Force method checks every possible pair to calculate the total number of inversions, resulting in Θ(n²) time complexity. The Divide and Conquer approach improves this process by dividing the array into two smaller subarrays and recursively counting inversions within each subarray. The sorted subarrays are then merged while counting cross inversions between them. Whenever an element from the right subarray is smaller than the current element in the left subarray, all the remaining elements in the left subarray form inversions with that element. This allows multiple inversions to be counted efficiently during the merging process. The recurrence relation is T(n) = 2T(n/2) + O(n), resulting in an overall time complexity of Θ(n log n). The implementation also produces the sorted array along with the total inversion count. This problem demonstrates how the Merge Sort technique can be extended to solve additional computational problems and how efficient algorithm design reduces unnecessary operations.

---

## Student Contribution Record

The following primary responsibilities are taken from the assignment brief. The shared-work column must be completed to reflect the actual joint work. Both students remain responsible for understanding the entire assignment.

| Question | Student A – Primary Contribution | Student B – Primary Contribution | Joint Work |
|---|---|---|---|
| Q1 | Max/Min decomposition, combine logic and comparison analysis; Binary Search experiments | Max/Min datasets and comparison instrumentation; Binary Search elimination logic | Design, implement and test both algorithms |
| Q2 | Quick Sort balanced/unbalanced experiments, partitions and recursion depth | Merge Sort analysis and comparison with Quick Sort | Implement both sorts, choose pivot strategy, run experiments and answer joint design question |
| Q3 | Karatsuba derivation, recurrence and asymptotic analysis | Crossover experiment, timings, multiplication counts and overhead analysis | Implement standard and Karatsuba multiplication; correctness and joint conclusion |
| Q4 | Matrix-size experiments, multiplication counts, timings and engineering analysis | Block algebra, seven products, correctness and padding explanation | Implement and verify conventional and Strassen multiplication; decide practical use |
| Q5 | D&C decomposition, recursive returns, combine and boundary explanation | Equivalent datasets, distance counts, runtime comparison and crossover investigation | Implement and compare Brute Force and D&C algorithms |
| Q6 | Median of Medians implementation, grouping, pivot and worst-case guarantee; MITM verification | Meet-in-the-Middle implementation, subset sums, time-memory analysis; pivot-quality verification | Review both investigations and cross-explain |
| Q7 | Independent proposal; recurrence formulation, solution and mathematical validation | Independent proposal; implementation, correctness tests and experimental validation | Compare proposals, create final design, cross-defend and jointly evaluate |

