## Q2 – Merge Sort and Quick Sort

### Part A – Merge Sort

#### Python Code

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

### Part B – Quick Sort

#### Python Code

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

