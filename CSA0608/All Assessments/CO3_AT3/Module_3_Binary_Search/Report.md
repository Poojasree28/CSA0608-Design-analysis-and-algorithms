# MODULE 3 – BINARY SEARCH FOR ORDER LOOKUP

## 1. Aim

To implement Binary Search using the Divide-and-Conquer technique to locate an order by its timestamp in a sorted order list and modify the algorithm to return the first occurrence when multiple orders have the same timestamp.

## 2. Problem Statement

KartIQ customer-support staff need to locate orders using their timestamps.

The consolidated order list produced by Module 1 is already sorted in ascending order.

However, several orders may share the same timestamp. Therefore, the search algorithm must return the first order having the requested timestamp.

### Sample Dataset

| Timestamp | Order ID |
|---|---|
| 101 | O4 |
| 102 | O2 |
| 102 | O5 |
| 103 | O6 |
| 105 | O1 |
| 105 | O3 |

**Search Key:** `102`

**Expected Result:**

| Timestamp | Order ID |
|---|---|
| 102 | O2 |

The algorithm must return O2 instead of O5 because O2 is the first matching order.

## 3. Algorithm Explanation

Binary Search is a Divide-and-Conquer searching algorithm that works on sorted data.

It repeatedly divides the search interval into two halves.

### Three Main Operations

**1. Divide**

- Find the middle position of the current search interval.
- Divide the array into left and right sections.

**2. Conquer**

- If the middle timestamp is greater than the search key, search the left half.
- If the middle timestamp is smaller than the search key, search the right half.
- If it matches, record the position and continue searching towards the left to find the first occurrence.

**3. Combine**

- Return the first matching order.
- If the timestamp does not exist, display an appropriate message.

## 4. Pseudocode

**Algorithm: FIRST_OCCURRENCE_BINARY_SEARCH**

```text
FIRST_OCCURRENCE_BINARY_SEARCH(A, n, key)

    low = 0
    high = n - 1
    result = -1

    WHILE low <= high

        mid = low + (high - low) / 2

        IF A[mid].timestamp == key THEN

            result = mid
            high = mid - 1

        ELSE IF A[mid].timestamp < key THEN

            low = mid + 1

        ELSE

            high = mid - 1

        END IF

    END WHILE

    RETURN result

END
```

## 5. Flowchart

The flowchart follows these steps:

1. START
2. Read sorted orders.
3. Enter search timestamp.
4. Initialize `low = 0`, `high = n - 1`, and `result = -1`.
5. Check whether `low <= high`.
6. If YES, find the middle position.
7. Compare the middle timestamp with the search timestamp.
8. If equal, update `result = mid` and `high = mid - 1`.
9. If smaller, update `low = mid + 1`.
10. If greater, update `high = mid - 1`.
11. Repeat the search.
12. If the loop terminates, check whether `result == -1`.
13. If YES, display Not Found.
14. Otherwise, display the first matching order.
15. STOP.

## 6. Complete C Program

**File name:** `binary_search.c`

```c
#include <stdio.h>
#include <stdlib.h>

struct Order
{
    int timestamp;
    char orderID[20];
};

int firstOccurrence(struct Order a[], int n, int key)
{
    int low = 0;
    int high = n - 1;
    int result = -1;

    while (low <= high)
    {
        int mid = low + (high - low) / 2;

        if (a[mid].timestamp == key)
        {
            result = mid;

            /* Continue searching on the left */
            high = mid - 1;
        }
        else if (a[mid].timestamp < key)
        {
            low = mid + 1;
        }
        else
        {
            high = mid - 1;
        }
    }

    return result;
}

int main()
{
    int n, i, key;

    printf("ORDER LOOKUP USING BINARY SEARCH\n");

    printf("Enter number of sorted orders: ");
    scanf("%d", &n);

    if (n <= 0)
    {
        printf("Invalid number of orders.\n");
        return 1;
    }

    struct Order *orders =
        (struct Order *)malloc(n * sizeof(struct Order));

    if (orders == NULL)
    {
        printf("Memory allocation failed.\n");
        return 1;
    }

    printf("\nEnter orders in ascending timestamp order:\n");

    for (i = 0; i < n; i++)
    {
        printf("Order %d: ", i + 1);

        scanf("%d %19s",
              &orders[i].timestamp,
              orders[i].orderID);

        if (i > 0 &&
            orders[i].timestamp < orders[i - 1].timestamp)
        {
            printf("Error: Orders must be sorted.\n");
            free(orders);
            return 1;
        }
    }

    printf("\nEnter timestamp to search: ");
    scanf("%d", &key);

    int position = firstOccurrence(orders, n, key);

    if (position != -1)
    {
        printf("\nORDER FOUND\n");

        printf("Timestamp: %d\n",
               orders[position].timestamp);

        printf("Order ID: %s\n",
               orders[position].orderID);

        printf("First matching position: %d\n",
               position + 1);
    }
    else
    {
        printf("\nOrder with timestamp %d not found.\n", key);
    }

    free(orders);

    return 0;
}
```

## 7. Sample Input

```text
6
101 O4
102 O2
102 O5
103 O6
105 O1
105 O3
102
```

## 8. Expected Output

```text
ORDER LOOKUP USING BINARY SEARCH

Enter number of sorted orders: 6

Enter orders in ascending timestamp order:
Order 1: 101 O4
Order 2: 102 O2
Order 3: 102 O5
Order 4: 103 O6
Order 5: 105 O1
Order 6: 105 O3

Enter timestamp to search: 102

ORDER FOUND
Timestamp: 102
Order ID: O2
First matching position: 2
```

## 9. Execution Trace

**Search key = 102**

### Initial Sorted Array

| Index | Timestamp | Order ID |
|---|---|---|
| 0 | 101 | O4 |
| 1 | 102 | O2 |
| 2 | 102 | O5 |
| 3 | 103 | O6 |
| 4 | 105 | O1 |
| 5 | 105 | O3 |

### Iteration 1

```text
low = 0
high = 5

mid = (0 + 5) / 2 = 2

A[2] = 102
```

The timestamp matches the search key.

Save the current position:

```text
result = 2
```

Continue searching on the left side:

```text
high = mid - 1 = 1
```

### Iteration 2

```text
low = 0
high = 1

mid = (0 + 1) / 2 = 0

A[0] = 101
```

Since 101 is smaller than 102:

```text
low = mid + 1 = 1
```

### Iteration 3

```text
low = 1
high = 1

mid = (1 + 1) / 2 = 1

A[1] = 102
```

The timestamp matches again.

Update:

```text
result = 1
high = mid - 1 = 0
```

### Termination

```text
low = 1
high = 0
```

Since low is greater than high, the loop terminates.

### Final Result

```text
Position = 1 (zero-based)
Order ID = O2
Timestamp = 102
```

Therefore, the first matching order is O2.

## 10. Importance of Sorted Data

Binary Search works correctly only when the input list is sorted.

Module 1 produces the sorted order list using stable Merge Sort.

The output of Module 1 becomes the input of Module 3.

If the order list is unsorted, Binary Search may eliminate the wrong half of the array and return an incorrect result.

Therefore, both modules are directly connected.

## 11. Recurrence Relation

Binary Search reduces the search space to half after each comparison.

The recurrence relation is:

\[
T(n) = T(n/2) + O(1)
\]

**Where:**

- T(n/2) represents searching the remaining half.
- O(1) represents the middle-element comparison and interval update.

### Expanding

\[
T(n) = T(n/4) + 2O(1)
\]

\[
T(n) = T(n/8) + 3O(1)
\]

After k levels:

\[
\frac{n}{2^k} = 1
\]

Therefore:

\[
k = \log_2 n
\]

**Final Complexity:**

\[
T(n) = O(\log n)
\]

For the modified first-occurrence search, the same logarithmic complexity is maintained.

## 12. Production Workload Calculation

**Number of orders:**

\[
n = 10,000,000
\]

Maximum iterations of the inclusive binary-search loop:

\[
\lfloor \log_2 n \rfloor + 1
\]

\[
= \lfloor \log_2 10,000,000 \rfloor + 1
\]

\[
= 23 + 1
\]

\[
= 24 \text{ iterations}
\]

Thus, the maximum number of loop iterations is 24.

A separate equality check after the search may add one comparison. The code above instead records matches inside the loop, so the loop comparison bound is 24.

## 13. Complexity Analysis

| Case | Time Complexity |
|---|---|
| Best Case | O(1) |
| Average Case | O(log n) |
| Worst Case | O(log n) |

### Auxiliary Space

\[
O(1)
\]

The algorithm uses only a few variables:

- low
- high
- mid
- result

Therefore, it does not require an additional array.

## 14. Advantages

- Fast searching in large sorted datasets.
- Requires only logarithmic comparisons.
- Uses constant auxiliary memory.
- Can return the first matching timestamp.
- Suitable for customer-support order lookups.

## 15. Limitations

- Requires sorted input.
- Does not directly work on an unsorted list.
- Maintaining sorted data requires an additional sorting or update process.
- Duplicate timestamps require a modified search algorithm to identify the first occurrence.

## 16. Optimisation Recommendation

KartIQ should use modified Binary Search to locate the first occurrence of a timestamp.

The consolidated order list should be maintained in sorted order using Module 1.

For frequently changing order records, the platform can maintain a sorted index based on timestamps. This avoids repeatedly sorting the entire order collection before every lookup.

## Conclusion

Modified Binary Search is an efficient solution for KartIQ because it can search 10 million sorted orders using at most 24 loop iterations and correctly return the first order when timestamps are duplicated.
