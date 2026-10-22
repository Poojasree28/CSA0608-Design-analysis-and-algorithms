# TASK 1 – DESIGN THE ALGORITHM 

## 1.1 Introduction

A university maintains a large database containing student records. Each student has a unique registration number. Searching algorithms help faculty and administrative staff find student records efficiently.

The three algorithms selected are:

1. Linear Search
2. Iterative Binary Search
3. Recursive Binary Search

## 1.2 Algorithm 1: Linear Search

**Basic Idea:**

Linear Search checks each registration number one by one until the required number is found or the list ends.

**Design Strategy:** Iterative searching.

**Preprocessing Required:** No sorting is required.

**Pseudocode:**

```text
Algorithm LinearSearch(A, n, key)

1. Start
2. For i = 0 to n - 1
3.     If A[i] == key
4.         Return i
5. Return -1
6. Stop
```

**Explanation:**

The algorithm starts from the first element and compares each registration number with the required number. If a match is found, its index is returned. Otherwise, it returns -1, indicating that the registration number is not present.

**Justification:**

Linear Search is simple and works with both sorted and unsorted data.

## 1.3 Algorithm 2: Iterative Binary Search

**Basic Idea:**

Binary Search compares the required registration number with the middle element of a sorted list. It eliminates half of the remaining elements after each comparison.

**Design Strategy:** Iterative divide-and-conquer searching.

**Preprocessing Required:** The registration numbers must be sorted in ascending order.

**Pseudocode:**

```text
Algorithm BinarySearch(A, n, key)

1. Start
2. low = 0
3. high = n - 1
4. While low <= high
5.     mid = (low + high) // 2
6.     If A[mid] == key
7.         Return mid
8.     Else if key < A[mid]
9.         high = mid - 1
10.    Else
11.        low = mid + 1
12. Return -1
13. Stop
```

**Explanation:**

The algorithm checks the middle element and continues searching only in the half that may contain the required registration number. This process repeats until the number is found or the search interval becomes empty.

**Justification:**

Binary Search is efficient for large, sorted datasets because it reduces the search space by approximately half after each comparison.

## 1.4 Algorithm 3: Recursive Binary Search

**Basic Idea:**

Recursive Binary Search uses recursion to search smaller portions of a sorted list.

**Design Strategy:** Recursive divide-and-conquer searching.

**Preprocessing Required:** The registration numbers must be sorted in ascending order.

**Pseudocode:**

```text
Algorithm RecursiveBinarySearch(A, low, high, key)

1. If low > high
2.     Return -1
3. mid = (low + high) // 2
4. If A[mid] == key
5.     Return mid
6. Else if key < A[mid]
7.     Return RecursiveBinarySearch(A, low, mid - 1, key)
8. Else
9.     Return RecursiveBinarySearch(A, mid + 1, high, key)
```

**Explanation:**

The algorithm checks the middle element. If the required number is not found, it calls itself to search either the left half or the right half. The process continues until the number is found or the search interval becomes empty.

**Justification:**

Recursive Binary Search demonstrates recursion and divide-and-conquer techniques. Its performance can be compared with the iterative version.

## 1.5 Conclusion

Linear Search is suitable for small or unsorted datasets. Iterative and Recursive Binary Search are suitable for large, sorted datasets. Both Binary Search approaches have logarithmic time complexity, but they differ in implementation. Iterative Binary Search uses loops, whereas Recursive Binary Search uses function calls.
