## Q1 – Part A: Finding Maximum and Minimum Using Divide and Conquer

### Python Code

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


## Part B – Binary Search

### Python Code

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

Maximum element: 14
Number of comparisons: 11
```
