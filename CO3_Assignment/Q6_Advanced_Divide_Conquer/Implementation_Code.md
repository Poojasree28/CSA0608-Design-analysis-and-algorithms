## Part A – Median of Medians

### Python code
```python
def median_of_medians_select(a, k):

    if not 1 <= k <= len(a):
        raise ValueError("k must be between 1 and n")

    if len(a) <= 5:
        return sorted(a)[k - 1]

    groups = [a[i:i + 5] for i in range(0, len(a), 5)]

    medians = [sorted(g)[len(g) // 2] for g in groups]

    pivot = median_of_medians_select(medians, (len(medians) + 1) // 2)

    low = [x for x in a if x < pivot]

    equal = [x for x in a if x == pivot]

    high = [x for x in a if x > pivot]

    if k <= len(low):
        return median_of_medians_select(low, k)

    if k <= len(low) + len(equal):
        return pivot

    return median_of_medians_select(high, k - len(low) - len(equal))


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

---

## Part B – Meet-in-the-Middle Subset Sum

### Python code

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
