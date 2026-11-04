##  Counting Inversions

### Python code

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
